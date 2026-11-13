# Limit outbound traffic for VKS worker nodes

By default, worker nodes of a VKS cluster are allowed outbound access to every destination. This guide shows how to configure an outbound rule set that is **the minimum for a VKS cluster to operate stably**. Destinations that your applications access are out of scope of this rule set; you must add them yourself (see the note in Step 2).

- **Scope:** **private clusters** using the Cilium overlay CNI. With Calico or Cilium native routing, the steps still apply; only the inter-node ports in Step 2 differ (how to determine them is described there).
- **Not applicable to public clusters:** nodes access VNG Cloud services via public domains whose IP addresses can change at any time, so they cannot be filtered with Security Groups.
- **Only need to restrict pod egress:** use a `CiliumNetworkPolicy` egress. This option supports domain (FQDN) filtering and does not affect system components.
- **Responsibility:** you are responsible for managing and maintaining the outbound rule set. Missing rules can prevent new nodes from joining the cluster, pulling images, or creating volumes or load balancers.

## What you need to know

- A node's outbound traffic is allowed if **any** Security Group (SG) attached to the VM allows it. Therefore you must remove the outbound allow-all rules on **all** SGs attached to the node, not just the cluster SG.
- SGs are stateful: you only need outbound rules; return traffic is automatically allowed.
- Every newly created SG comes with 2 default outbound allow-all rules: `any → 0.0.0.0/0` and `any → ::/0`.

SGs typically attached to a VKS node:

| SG | Name format | Action required |
| --- | --- | --- |
| Cluster node SG | `vks-user-<user ID>-k8s-<cluster ID>-…` | Add allow rules, delete the 2 default rules (Steps 2–3) |
| Load balancer SG | `vks-<shortened cluster ID>-<namespace>-<Service/Ingress name>-…` | Disable outbound via annotation (next section) |
| SG attached by you | Any name you choose | Delete the 2 default rules |

## Disable outbound on the load balancer SG

The GreenNode LoadBalancer Controller creates one SG per `LoadBalancer` Service and Ingress, then attaches this SG to the nodes. By default, this SG allows all outbound traffic; if you delete the rules manually, the controller recreates them. To disable them, add the following annotation to **all** `LoadBalancer` Services and Ingresses:

```yaml
metadata:
  annotations:
    vks.vngcloud.vn/enable-default-egress: "false"
```

The controller removes the 2 outbound rules from the corresponding SG without causing downtime for the load balancer. When you remove the annotation, the 2 rules are recreated.

> **Do not delete outbound rules directly on the portal** for SGs managed by the controller: the controller will recreate these rules at the next periodic sync. Always use the annotation.

The annotation requires GreenNode LoadBalancer Controller version `0.5.0` or later; if your cluster runs an older version, upgrade first. Check the current version:

```bash
kubectl -n kube-system get deploy -l app.kubernetes.io/name=vngcloud-load-balancer-controller \
  -o jsonpath='{.items[0].spec.template.spec.containers[0].image}'; echo
```

**Apply to every Service/Ingress, including resources created later.** A single `LoadBalancer` Service or Ingress missing the annotation reopens outbound for the entire node. List resources missing the annotation (empty output means all are covered):

```bash
kubectl get svc -A -o jsonpath='{range .items[?(@.spec.type=="LoadBalancer")]}{.metadata.namespace}/{.metadata.name} {.metadata.annotations.vks\.vngcloud\.vn/enable-default-egress}{"\n"}{end}' | awk '$2!="false"'
kubectl get ingress -A -o jsonpath='{range .items[*]}{.metadata.namespace}/{.metadata.name} {.spec.ingressClassName}{.metadata.annotations.kubernetes\.io/ingress\.class} {.metadata.annotations.vks\.vngcloud\.vn/enable-default-egress}{"\n"}{end}' | awk '$2=="vngcloud" && $3!="false"'
```

## Step 1: Collect cluster parameters

IP addresses differ between clusters, so you need to collect parameters for each cluster individually. Create a debug pod on a node (requires kubectl 1.28 or later; the command uses the Cilium image already present on the node, because private clusters usually cannot reach Docker Hub):

```bash
NODE=$(kubectl get nodes -o jsonpath='{.items[0].metadata.name}')
IMG=$(kubectl -n kube-system get ds cilium -o jsonpath='{.spec.template.spec.containers[0].image}')
kubectl debug node/$NODE -it --profile=sysadmin --image=$IMG -- chroot /host bash -c '
  echo "## control plane"; grep "server:" /etc/kubernetes/kubelet.conf
  echo "## endpoints"; for h in iamapis.vngcloud.vn hcm-3.api.vngcloud.vn hcm03.vstorage.vngcloud.vn vcr.vngcloud.vn; do
    getent ahosts $h | cut -d" " -f1 | sort -u | sed "s/^/$h /"; done
  echo "## dns";   resolvectl status | grep -E "DNS Servers|Current DNS"
  echo "## ntp";   timedatectl show-timesync -p ServerAddress -p SystemNTPServers
  echo "## dhcp";  networkctl status eth0 | grep "DHCP4 via"'
kubectl get pods -o name | grep node-debugger | xargs kubectl delete
```

Record the following values:

| Parameter | Example | Source |
| --- | --- | --- |
| VPC CIDR | `10.0.0.0/16` | VPC portal (the CIDR of the VPC, not of the subnet) |
| Control plane IP | `10.0.1.3` | `## control plane` section. If it is a hostname, run `getent ahosts <hostname>` on the node and collect all IPs |
| Private endpoint IPs | `10.0.1.6` … `10.0.1.9` | `## endpoints` section: IAM (`iamapis…`), vServer API (`…api…`), vStorage (`…vstorage…`), vCR (`vcr…`). A multi-AZ cluster has one IP per zone — collect all of them. The domains in the command are for the HCM region; for other regions, see the Private Service Endpoint page on the portal |
| DNS resolver | `8.8.8.8` | `## dns` section, collect all IPs |
| NTP server | Internal NTP server IP | `## ntp` section. If it is a public pool (e.g. `ntp.ubuntu.com`), the IP changes constantly: switch to an internal NTP server or allow `UDP 123 → 0.0.0.0/0` |
| DHCP server | `10.0.1.2` | `## dhcp` section |

## Step 2: Create the outbound rule set

Add the rules below to the **node SG**: on the vServer portal, go to **Security Groups**, select the SG named `vks-user-<user ID>-k8s-<cluster ID>-…`, open the **Outbound** rule list and add rules. Take the values in `< >` from Step 1; each IP corresponds to one rule in `/32` form. The "Type" column is the rule type to select on the portal. Note: the **DNS** type on the portal only opens TCP, so you also need a **Custom UDP** rule for DNS.

**Option 1 (recommended): allow all traffic within the VPC, block traffic outside the VPC.**

| # | Type | Port | Destination | Purpose |
| --- | --- | --- | --- | --- |
| 1 | All Traffic | – | `<VPC CIDR>` | Control plane, private endpoints, DHCP, inter-node traffic |
| 2 | HTTP | 80 | `169.254.169.254/32` | Metadata service, used during node bootstrap and when the CSI/LB controllers start |
| 3 | DNS **and** Custom UDP | 53 | `<DNS resolver>/32` | DNS resolution |
| 4 | Custom UDP | 123 | `<NTP server>/32` | Time sync |

Verify that the control plane IP, the 4 private endpoint IPs, and the DHCP server are all within `<VPC CIDR>`. Any IP outside this range needs its own rule per the Option 2 table. If the DNS resolver and NTP server are inside the VPC, rules 3 and 4 are not needed.

<details>
<summary>Option 2: open only the necessary ports (replaces rule 1)</summary>

| Type | Port | Destination | Purpose |
| --- | --- | --- | --- |
| Custom TCP | 6443 | `<Control plane IP>/32` | Kubernetes API server |
| Custom TCP | 8132 | `<Control plane IP>/32` | `kubectl logs/exec`, admission webhook |
| HTTPS | 443 | `<IAM endpoint IP>/32` | Authentication for the CSI and LB controllers |
| HTTPS | 443 | `<vServer API endpoint IP>/32` | Attach volumes, create load balancers |
| HTTPS | 443 | `<vCR endpoint IP>/32` | Pull system images |
| HTTPS | 443 | `<vStorage endpoint IP>/32` | vStorage |
| Custom UDP | 67 | `<DHCP server>/32` | DHCP lease renewal. Without this rule, the node still gets an IP at boot but cannot renew the lease periodically |
| Custom UDP | 8472 | `<VPC CIDR>` | VXLAN tunnel between nodes (pod-to-pod traffic) |
| Custom TCP | 4240 | `<VPC CIDR>` | Cilium health check |
| All ICMP | – | `<VPC CIDR>` | Health check, Path MTU Discovery |
| Custom TCP | 10250 | `<VPC CIDR>` | Kubelet API between nodes |
| Custom TCP | 4244 | `<VPC CIDR>` | Hubble |

The last four rules with destination `<VPC CIDR>` apply to Cilium overlay. For other CNIs, copy the inbound rules VKS created on the node SG to the outbound direction (same protocol, same port, destination `<VPC CIDR>`).

</details>

> **Note on application destinations.** The rule set above only covers the needs of the VKS cluster itself. After you delete the default outbound rules, every connection from your applications to a destination **outside the VPC** (with Option 2, also destinations inside the VPC) will be blocked unless it matches a rule — for example: databases or APIs outside the VPC, private or public image registries (Docker Hub, ghcr.io…), Git, logging/monitoring backends, SaaS services. Review and add rules for these destinations before applying.
>
> Destinations served by CDNs (Docker Hub, ghcr.io, quay.io and most SaaS services) change IPs constantly, so IP-based rules will stop working after a short time. We recommend mirroring images to vCR, and accessing SaaS services through a proxy or `CiliumNetworkPolicy` `toFQDNs`.

## Step 3: Apply

Principle: add the allow rules first, delete the allow-all rules last. Rehearse on a dev/staging cluster with the same configuration before applying to production.

1. Back up the current configuration: the SG list of each node VM and all rules of those SGs.
2. Add all rules from Step 2, plus the rules for your application destinations, to the node SG. Do not delete any rules yet.
3. Add the annotation `enable-default-egress: "false"` to all `LoadBalancer` Services and Ingresses (see "Disable outbound on the load balancer SG"). This step must come **after** step 2: if the node SG is still missing rules and the cluster is running on the load balancer SG's outbound, disabling it causes downtime immediately.
4. During a maintenance window (off-peak hours), delete the 2 default outbound rules (`::/0` first, then `0.0.0.0/0`) on the node SG and any SGs you attached yourself.
5. Verify immediately per Step 4. If anything goes wrong, roll back first, then investigate.

Existing connections may keep working; only **new** connections are blocked. Monitor for at least one business cycle. A newly created or recreated cluster gets a new node SG — start again from Step 1.

## Step 4: Verify

- [ ] **Confirm outbound is blocked:** a connection to a destination not in the rules must time out: `kubectl run egresstest --rm -it --restart=Never --image=<image with curl> -- curl -m 5 -sS https://1.1.1.1`. If the VPC has no internet route, this test always times out and proves nothing; instead test against a destination inside the VPC that has no allow rule.
- [ ] All nodes are `Ready`; `kubectl logs` and `kubectl exec` work normally.
- [ ] DNS resolution in pods works for both the cluster's internal domains and the external domains your applications use.
- [ ] New images can be pulled (test with `imagePullPolicy: Always`).
- [ ] Restart the CSI and LB controllers and the pods return to `Running`: `kubectl -n kube-system get deploy,ds -o name | grep -E 'csi|load-balancer' | xargs -n1 kubectl -n kube-system rollout restart`
- [ ] A PVC can be created and mounted to a pod.
- [ ] An annotated `LoadBalancer` Service can be created and receives an external address; repeat the first test: it must still time out.
- [ ] DHCP lease renewal works: in the debug pod from Step 1, run `networkctl renew eth0`; after a few seconds, `ip -4 addr show eth0` shows `valid_lft` back near the full lease time (usually 86400s).
- [ ] Scale the node group up by 1 node: the new node becomes `Ready` within the normal time. Then scale back down.
- [ ] Applications work correctly: database connections, API calls, log and metric shipping, scheduled jobs.

## Rollback

Add the following rule back to the node SG to return the cluster to its original state, without restarting nodes or pods:

| Type | Port | Destination |
| --- | --- | --- |
| All Traffic | – | `0.0.0.0/0` |

Pods that failed while the rule was missing will retry on their own. Nodes created while the rule was missing (e.g. during scaling) do not recover after the rollback rule is added; replace those nodes. Once you have identified and added the missing rules, delete the rollback rule.

## Troubleshooting

| Symptom | Common cause |
| --- | --- |
| New node never becomes `Ready`, keeps being replaced | Missing rule to the metadata service `169.254.169.254`, control plane (6443), vCR or DNS |
| CSI or LB controller in `CrashLoopBackOff` | Missing rule to the metadata service, IAM or vServer API |
| Pods on different nodes cannot reach each other, node `NotReady` | Missing inter-node rules (UDP 8472, TCP 4240, ICMP) |
| `kubectl logs/exec` times out | Missing TCP 8132 rule to the control plane |
| `ImagePullBackOff` | Missing rule to vCR (system images) or the registry holding your application images |
| PVC stuck in `Pending`, `LoadBalancer` Service gets no external address | Missing rule to IAM or the vServer API |
| TLS certificate "not yet valid"/"expired" errors after a few days | Missing rule to the NTP server |
| `networkctl renew eth0` on the node cannot renew the lease | Missing DHCP rule (UDP 67) |
| Rules deleted but the node can still reach the internet | Another SG still allows outbound — usually the SG of a Service/Ingress missing the annotation `enable-default-egress: "false"` |
| Application cannot reach a database, API, registry… outside the VPC | Missing rule for the application's destination (see the note in Step 2) |
