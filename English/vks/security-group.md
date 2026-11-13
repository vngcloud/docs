# Security Group

A Security Group (SG) acts as a firewall that controls traffic going in and out of a server (VM). When you create a cluster and expose applications through a load balancer, VKS automatically creates and attaches certain SGs to worker nodes so the cluster can operate. This page describes those SGs, the rules inside them, and what VKS automatically restores if you make changes.

A worker node typically has the following SGs:

| SG | Created by | Name format | Quantity |
|---|---|---|---|
| Cluster node SG | VKS, when the cluster is created | `vks-user-<user ID>-k8s-<cluster ID>-<random string>` | 1 SG per cluster |
| Load balancer SG | GreenNode LoadBalancer Controller, when a `LoadBalancer` Service or Ingress is created | `vks-<shortened cluster ID>-<namespace>-<Service/Ingress name>-<hash>` | 1 SG per `LoadBalancer` Service / Ingress |
| SG attached by you | You | Any name you choose | Up to you |

{% hint style="info" %}
**Notes:**

* Traffic is allowed if **any** SG attached to the VM allows it.
* SGs are stateful: return traffic of an allowed connection is automatically allowed, without a rule in the reverse direction.
* Every newly created SG comes with 2 outbound allow-all rules: `any → 0.0.0.0/0` (IPv4) and `any → ::/0` (IPv6).
* A VM can only have a limited number of SGs attached, according to the project quota. Each `LoadBalancer` Service / Ingress attaches 1 more SG to the node; if the quota is reached, the controller cannot attach new SGs. Share an SG across Services via the annotation `vks.vngcloud.vn/security-groups` to avoid exceeding the quota (see below).
{% endhint %}

## Cluster node SG

Each cluster has one node SG, created together with the cluster and attached to all worker nodes of every node group, including nodes created later. The SG description is: `Default worker security group for VKS cluster <cluster name>. Please DO NOT DELETE it.`

In the tables below, **`<Subnet CIDR>`** is the CIDR of the subnet used by the node group. If the node groups use multiple subnets, each rule is created repeatedly for each subnet CIDR.

### Inbound — applied to all CNIs

| Protocol | Ether type | Port range | Source | Meaning |
|---|---|---|---|---|
| TCP | IPv4 | 30000-32767 | `<Subnet CIDR>` | NodePort Service (TCP) |
| UDP | IPv4 | 30000-32767 | `<Subnet CIDR>` | NodePort Service (UDP) |
| TCP | IPv4 | 10250 | `<Subnet CIDR>` | Kubelet API |
| TCP | IPv4 | 10250 | `<control plane endpoint IP>/32` | Kubelet API from the control plane. Only present when the cluster's control plane endpoint is an IP address |

### Inbound — additional rules per CNI

**Calico Overlay**

| Protocol | Ether type | Port range | Source | Meaning |
|---|---|---|---|---|
| TCP | IPv4 | 179 | `<Subnet CIDR>` | Calico BGP |
| 4 (IP-in-IP) | IPv4 | 1-65535 | `<Subnet CIDR>` | Calico IP-in-IP |
| TCP | IPv4 | 5473 | `<Subnet CIDR>` | Calico Typha |

**Cilium Overlay**

| Protocol | Ether type | Port range | Source | Meaning |
|---|---|---|---|---|
| UDP | IPv4 | 8472 | `<Subnet CIDR>` | Cilium VXLAN overlay |
| TCP | IPv4 | 4240 | `<Subnet CIDR>` | Cilium health check (TCP) |
| ICMP | IPv4 | 1-255 | `<Subnet CIDR>` | Cilium health check (ICMP) |

**Cilium VPC Native Routing**

| Protocol | Ether type | Port range | Source | Meaning |
|---|---|---|---|---|
| UDP | IPv4 | 8472 | `<Subnet CIDR>` | Cilium VXLAN |
| TCP | IPv4 | 4240 | `<Subnet CIDR>` | Cilium health check (TCP) |
| ICMP | IPv4 | 1-255 | `<Subnet CIDR>` | Cilium health check (ICMP) |
| TCP | IPv4 | 53 | `<Subnet CIDR>` | DNS (TCP) |
| UDP | IPv4 | 53 | `<Subnet CIDR>` | DNS (UDP) |

### Outbound

| Protocol | Ether type | Port range | Destination | Meaning |
|---|---|---|---|---|
| ANY | IPv4 | 0-65535 | 0.0.0.0/0 | Default rule of every SG |
| ANY | IPv6 | 0-65535 | ::/0 | Default rule of every SG |

### What VKS automatically restores

VKS periodically checks the node SG:

* **Inbound rules in the tables above deleted or modified:** VKS recreates the missing rules.
* **Rules you added yourself** (inbound or outbound): VKS leaves them untouched.
* **Default outbound rules:** VKS does not manage them. If you delete them, VKS will not recreate them. See [Limit outbound traffic for VKS worker nodes](security-group/limit-outbound-traffic-for-worker-nodes.md) before deleting.
* **The entire node SG deleted:** VKS creates a new node SG (with the 2 default outbound allow-all rules) and attaches it to the nodes. Any rules you added to the old SG, including a restricted outbound rule set, are lost and must be reconfigured on the new SG.

{% hint style="warning" %}
**Do not delete the cluster node SG.** The node SG is deleted together with the cluster. Deleting it manually causes the cluster to lose connectivity between nodes until VKS creates a new SG, and your custom configuration on the old SG is lost.
{% endhint %}

## Load balancer SG

When you create a Service `type: LoadBalancer` (Network Load Balancer) or an Ingress (Application Load Balancer), the GreenNode LoadBalancer Controller creates a dedicated SG for that Service/Ingress, with the description `Automatically created using VNGCLOUD LoadBalancer Controller`. The SG is attached to all worker nodes (or only the nodes matching the annotation `vks.vngcloud.vn/target-node-labels`), including nodes created later.

In the tables below, **`<LB Subnet CIDR>`** is the CIDR of the subnet the load balancer uses to connect to the nodes (backend subnet).

### Inbound — Service `LoadBalancer`

| Case | Protocol | Port | Source | Meaning |
|---|---|---|---|---|
| Default (target type `instance`) | Follows the protocol of each Service port (TCP/UDP) | NodePort of each port | `<LB Subnet CIDR>` | Load balancer accesses the NodePort |
| Target type `ip` | Follows the protocol of each Service port (TCP/UDP) | `targetPort` of the pod | `<LB Subnet CIDR>` | Load balancer accesses the pod directly |
| Cluster uses Cilium VPC Native Routing | Follows the protocol of each Service port (TCP/UDP) | `targetPort` of the pod | Subnet CIDR of every node in the cluster | Nodes forward traffic to pods on other nodes |
| With annotation `vks.vngcloud.vn/healthcheck-port` | Follows the protocol of the Service port | Declared health check port | `<LB Subnet CIDR>` | Custom health check port |
| Service has a UDP port | ICMP | 1-255 | Same source as the UDP rule | Health check for the UDP port |

### Inbound — Ingress

Same as the Service above, applied to each backend Service of the Ingress (default backend and every path), with the protocol always being TCP.

### Outbound

| Protocol | Ether type | Port range | Destination | Meaning |
|---|---|---|---|---|
| ANY | IPv4 | 0-65535 | 0.0.0.0/0 | Default outbound |
| ANY | IPv6 | 0-65535 | ::/0 | Default outbound |

These 2 outbound rules are disabled with the annotation `vks.vngcloud.vn/enable-default-egress: "false"` on the Service/Ingress (requires GreenNode LoadBalancer Controller version `0.5.0` or later). Details at [Limit outbound traffic for VKS worker nodes](security-group/limit-outbound-traffic-for-worker-nodes.md).

### What VKS automatically restores

The controller manages **all** rules (both inbound and outbound) of this SG:

* Rules modified or deleted manually are restored at the next periodic sync. Rules you add to this SG yourself will be deleted.
* When you modify the Service/Ingress (ports, annotations…), the rules are updated accordingly.
* When the Service/Ingress is deleted, the SG is detached from the nodes and deleted.

Therefore, **do not modify rules directly on the portal** for this SG; always configure via annotations.

### Use your own SG instead of the auto-created one

Add the annotation `vks.vngcloud.vn/security-groups: "<SG ID 1>,<SG ID 2>"` to the Service/Ingress:

* The controller does not create a dedicated SG for that Service/Ingress; any previously auto-created SG is detached from the nodes and deleted.
* The SGs you specify are attached to the worker nodes (including new nodes) — **not** to the load balancer.
* The controller **does not touch** the rules of these SGs: you add the inbound rules for the Service ports yourself (per the table above) and manage outbound yourself. The annotation `enable-default-egress` has no effect in this case.
* You can share one SG across multiple Services/Ingresses to reduce the number of SGs attached to each node.

{% hint style="info" %}
The annotation `vks.vngcloud.vn/inbound-cidrs` (restricting client IPs that can access the load balancer) configures the ACL on the load balancer's listeners; it does not change SG rules.
{% endhint %}

## Frequently asked questions

**I want to block worker node outbound traffic to the internet?**
See [Limit outbound traffic for VKS worker nodes](security-group/limit-outbound-traffic-for-worker-nodes.md). You must handle outbound on **every** SG attached to the node, not just the cluster node SG.

**I want to add an inbound rule for my application (e.g. open a port for another system in the VPC to access the node)?**
Add the rule to the cluster node SG or to a separate SG that you create and attach to the node yourself. Do not add it to the load balancer SG, because the controller will delete that rule.

**Do newly created nodes automatically get all the SGs?**
Yes. The cluster node SG and the load balancer SG are automatically attached to new nodes. SGs you attached to the VM manually are **not** automatically attached to new nodes; use the annotation `vks.vngcloud.vn/security-groups` if you need your SG to follow the nodes.
