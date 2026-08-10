# VKS MCP Tools

VKS MCP Server provides tools to manage and automate **VKS — GreenNode Kubernetes Service** resources: clusters, node groups, and the Kubernetes resources _inside_ a cluster. Every operation is exposed as a **tool with argument-based input** — no resource URIs are used.

### Tool groups

| Group           | Purpose                                                                                                                 |
| --------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Cluster (13)    | List/inspect/create/update/delete clusters, view events, fetch the kubeconfig, configure auto-upgrade and auto-healing. |
| Node group (10) | Create/update/delete node groups, change node count, autoscale, upgrade version, list nodes.                            |
| Kubernetes (7)  | Work with resources inside a cluster: list/CRUD, apply YAML, pod logs, events, API versions.                            |
| Version (1)     | Kubernetes versions available for create/upgrade.                                                                       |

### Conventions

* **`verb_noun` naming** (EKS style), mapping 1:1 to greennode-cli (`list-clusters` ↔ `list_clusters`).
* **Access** is noted at the end of each tool description:
  * `read` — always available. Default read-only mode registers **29 tools**.
  * `write` — requires the `--allow-write` flag. 12 cluster/node-group tools are **not registered** without it, so the agent cannot see them. `apply_yaml` and `manage_k8s_resource` are the exception: always listed, but refused at call time.
  * `read, sensitive` — requires the `--allow-sensitive-data-access` flag. These tools are **always listed**; without the flag the call returns an error.
* **`region`** (`Literal["HCM-3", "HAN"]`, default `HCM-3`) is an optional parameter on **most** tools and is not repeated below. Tools that take no `region`: `list_flavors`, `list_volume_types` (derived from the cluster), `get_creation_guide`, `generate_app_manifest`, `get_access_token`. `list_*` output echoes back the region it queried.
* **`refresh`** (bool, default `false`) on discovery tools: these tools briefly cache results for speed, so set `refresh=true` to bypass the cache and pull fresh data from vServer — use it right after creating or deleting a resource in the console.
* **Annotations**: every tool declares `readOnlyHint` / `destructiveHint` so clients can auto-approve reads and warn before destructive calls. `destructiveHint=true` on `delete_cluster`, `delete_nodegroup`, `delete_auto_upgrade`, `upgrade_nodegroup_version`, `manage_k8s_resource`.

***

### Supported Tools

#### Cluster (13)

* **`list_clusters`** — List every cluster in a region (all pages fetched automatically). _(read)_
  * No required parameters. Clusters are region-scoped — if one is missing, try the other region.
* **`get_cluster`** — Full detail of one cluster (structured). _(read)_
  * `cluster_id` (required, string): Cluster ID — resolve it from a name via `list_clusters`.
* **`get_cluster_kubeconfig`** — Kubeconfig YAML (cluster-admin credentials). For a new cluster, run `generate_kubeconfig` first. _(read, sensitive)_
  * `cluster_id` (required, string): Cluster ID.
* **`get_cluster_events`** — Cluster events table. _(read)_
  * `cluster_id` (required, string): Cluster ID.
  * `page` (optional, int ≥0): Page number (starts at 0).
  * `pageSize` (optional, int ≥1): Items per page (default 20).
* **`validate_cluster_create`** — Validate a create body without actually creating. _(read)_
  * `body` (required, object `CreateClusterComboDto`): The body you intend to send to `create_cluster` (same structure — see fields below).
* **`delete_cluster_dryrun`** — Preview a cluster deletion (including its node groups). _(read)_
  * `cluster_id` (required, string): Cluster ID.
*   **`create_cluster`** — Create a cluster (control plane only); add workers via `create_nodegroup`. _(write)_

    * `body` (required, object `CreateClusterComboDto`): Cluster configuration.
      * `name` (required, string): Cluster name (5–20 chars: lowercase letters + digits + hyphens; letter/digit at both ends).
      * `version` (required, string): Kubernetes version (from `list_cluster_versions`).
      * `networkType` (required, enum `CILIUM_OVERLAY`|`CILIUM_NATIVE_ROUTING`|`TIGERA`): Network type.
      * `vpcId` (required, string): VPC ID (from `list_vpcs`).
      * `releaseChannel` (optional, enum `RAPID`|`STABLE`, default `STABLE`): Release channel.
      * `enablePrivateCluster` (optional, bool, default `false`): Whether the cluster is private.
      * `enabledLoadBalancerPlugin` (optional, bool, default `true`): Enable the load-balancer plugin.
      * `enabledBlockStoreCsiPlugin` (optional, bool, default `true`): Enable the block-store CSI plugin.
      * `enabledServiceEndpoint` (optional, bool): Private clusters only (default true there); omit for public clusters.
      * `azStrategy` (optional, enum `SINGLE`|`MULTI`, default `SINGLE`): Availability-zone strategy. `MULTI` requires a vDNS-enabled VPC.
      * `description` (optional, string ≤255): Description — ASCII only (letters, digits, spaces and `-_.@`; no accented characters).
      * `subnetId` (optional, string): Subnet ID (from `list_subnets`).
      * `cidr` (optional, string): Required when networkType is `CILIUM_OVERLAY` or `TIGERA`.
      * `listSubnetIds` (optional, string\[]): Subnet IDs for the cluster.
      * `nodeNetmaskSize` (optional, int): Node netmask size.
      * `autoUpgradeConfig` (optional, object): Auto-upgrade schedule.
        * `weekdays` (required, string): Days of week, e.g. `Mon,Wed,Fri`.
        * `time` (required, string): Time as `HH:mm`, e.g. `03:00`.
      * `autoHealingConfig` (optional, object): Auto-healing configuration.
        * `enableAutoHealing` (required, bool): Enable/disable.
        * `maxUnhealthy` (optional, string): e.g. `2` or `40%`.
        * `unhealthyRange` (optional, string): e.g. `[2-5]`.
        * `timeoutUnhealthy` (optional, int 5–180): Minutes before a node counts as unhealthy.
    * `poc` (optional, bool, default `false`): Proof-of-Concept cluster.
    * `autoRenewal` (optional, bool, default `true`): Auto-renew the subscription.

    > Secondary subnets are **not** set on the cluster — each node group declares its own `secondarySubnets` at creation time.
* **`update_cluster`** — Partial update; send only the fields that change (≥1). Name/description/release channel are NOT editable here. _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `body` (required, object `UpdateClusterDto`): At least 1 field.
    * `version` (optional, string): Target version; omit to keep.
    * `whitelistNodeCIDRs` (optional, string\[]): Omit to leave unchanged.
    * `enabledLoadBalancerPlugin` (optional, bool): Toggle the load-balancer plugin.
    * `enabledBlockStoreCsiPlugin` (optional, bool): Toggle the block-store CSI plugin.
* **`delete_cluster`** — Delete a cluster (IRREVERSIBLE; dry-run first). _(write)_
  * `cluster_id` (required, string): Cluster ID.
* **`configure_auto_upgrade`** — Set/change the auto-upgrade schedule (enabling auto-upgrade = calling this tool). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `weekdays` (required, string): Comma-separated days of week, e.g. `Mon,Wed,Fri`.
  * `time` (required, string): Time as `HH:mm`, e.g. `03:00`.
* **`delete_auto_upgrade`** — Turn auto-upgrade off (delete the schedule). _(write)_
  * `cluster_id` (required, string): Cluster ID.
* **`configure_auto_healing`** — Enable/disable/tune node auto-healing (one tool for every change). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `enable_auto_healing` (required, bool): Enable/disable auto-healing.
  * `max_unhealthy` (optional, string): Max count/percentage of unhealthy nodes before remediation, e.g. `2` or `40%`.
  * `unhealthy_range` (optional, string): Allowed range of unhealthy nodes, e.g. `[3-5]`.
  * `timeout_unhealthy` (optional, int 5–180): Minutes before a node counts as unhealthy.
* **`generate_kubeconfig`** — Mint a kubeconfig (async; required once for a new cluster). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `expiration_days` (required, int 1–365): Days until the kubeconfig expires (no default).

#### Node group (10)

* **`list_nodegroups`** — Node groups of a cluster. _(read)_
  * `cluster_id` (required, string): Cluster ID.
* **`get_nodegroup`** — Full node-group detail (subnet, encryption, placement). _(read)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
* **`list_nodes`** — Every node of a node group (all pages fetched automatically). _(read)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
* **`delete_nodegroup_dryrun`** — Preview a node-group deletion. _(read)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
* **`validate_nodegroup_create`** — Validate a create body before creating (free, non-mutating). _(read)_
  * `cluster_id` (required, string): Cluster the node group will join.
  * `body` (required, object `CreateNodeGroupDto`): The body you intend to send to `create_nodegroup` (same structure — see fields below).
* **`create_nodegroup`** — Create a node group (full CLI parity). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `body` (required, object `CreateNodeGroupDto`): Node-group configuration.
    * `name` (required, string): Name (5–15 chars: lowercase letters + digits + hyphens; letter/digit at both ends).
    * `flavorId` (required, string): Flavor ID (from `list_flavors`).
    * `diskSize` (required, int 20–5000): Disk size (GB).
    * `diskType` (required, string): Volume type ID (from `list_volume_types`).
    * `numNodes` (required, int 0–10): Number of nodes.
    * `sshKeyId` (required, string): SSH key ID (from `list_ssh_keys`).
    * `subnetId` (required, string): Subnet the nodes join (from `list_subnets`).
    * `secondarySubnets` (optional, string\[]): CILIUM\_NATIVE\_ROUTING clusters ONLY (required there): the `secondary_subnets` CIDRs of that subnetId, copied verbatim from `list_subnets` (e.g. `['10.5.60.0/22']`). Omit for other network types.
    * `os` (optional, enum `ubuntu`|`linux`|`rocky`, default `ubuntu`): OS image.
    * `enablePrivateNodes` (optional, bool, default `false`): `false` = nodes get public IPs; `true` = private-only.
    * `enabledEncryptionVolume` (optional, bool, default `false`): `true` = encrypt node disks.
    * `securityGroups` (optional, string\[]): Security group IDs (from `list_security_groups`).
    * `labels` (optional, object `key=value`): Node labels.
    * `tags` (optional, object `key=value`): Node tags.
    * `taints` (optional, object\[]): Node taints.
      * `key` (required, string): Taint key.
      * `value` (optional, string, default empty): Taint value.
      * `effect` (required, enum `NoSchedule`|`PreferNoSchedule`|`NoExecute`): Effect.
    * `autoScaleConfig` (optional, object): Autoscaling bounds.
      * `minSize` (required, int ≥0): Minimum number of nodes.
      * `maxSize` (required, int ≥1): Maximum number of nodes.
    * `upgradeConfig` (optional, object, default SURGE 1/0): Upgrade configuration.
      * `maxSurge` (optional, int 1–100, default `1`): Nodes added above the desired count during upgrade.
      * `maxUnavailable` (optional, int 0–100, default `0`): Nodes unavailable during upgrade (0 = rolling).
      * `strategy` (optional, string, default `SURGE`): Upgrade strategy.
    * `placementGroupConfigDto` (optional, object): Placement group.
      * `type` (required, enum `NEW`|`EXISTING`): Use a new or existing group.
      * `placementGroupId` (optional, string): Group ID when type=EXISTING (from `list_placement_groups`).
      * `placementGroupName` (optional, string): Group name when type=NEW.
* **`update_nodegroup`** — Update size / security groups / autoscale / upgrade config. For labels/tags/taints use `update_nodegroup_metadata`. _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
  * `body` (required, object `UpdateNodeGroupDto`): No field is mandatory, but at least one must be set.
    * `numNodes` (optional, int 0–10): Number of nodes.
    * `securityGroups` (optional, string\[]): Security group IDs.
    * `autoScaleConfig` (optional, object): Autoscaling bounds.
      * `minSize` (required, int ≥0): Minimum number of nodes.
      * `maxSize` (required, int ≥1): Maximum number of nodes.
    * `upgradeConfig` (optional, object): Upgrade configuration.
      * `maxSurge` (optional, int 1–100, default `1`): Nodes added above the desired count during upgrade.
      * `maxUnavailable` (optional, int 0–100, default `0`): Nodes unavailable during upgrade (0 = rolling).
      * `strategy` (optional, string, default `SURGE`): Upgrade strategy.
* **`update_nodegroup_metadata`** — Update labels, tags, taints. _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
  * `body` (required, object `UpdateNodeGroupMetadataDto`): At least 1 field.
    * `labels` (optional, object `key=value`): Node labels.
    * `tags` (optional, object `key=value`): Node tags.
    * `taints` (optional, object\[]): Node taints.
      * `key` (required, string): Taint key.
      * `value` (optional, string, default empty): Taint value.
      * `effect` (required, enum `NoSchedule`|`PreferNoSchedule`|`NoExecute`): Effect.
* **`delete_nodegroup`** — Delete a node group (IRREVERSIBLE; dry-run first). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
  * `force_delete` (required, bool): `true` = skip draining the nodes (pods killed immediately — for stuck/ERROR node groups); `false` = drain first.
* **`upgrade_nodegroup_version`** — Upgrade a node group's Kubernetes version (IRREVERSIBLE, no downgrade). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
  * `kubernetes_version` (required, string): Target version — see `list_cluster_versions`.

#### Kubernetes (7)

Work with Kubernetes resources _inside_ a cluster. The server fetches and caches the kubeconfig from the VKS API automatically — no `kubectl` setup needed.

* **`list_k8s_resources`** — List K8s resources by kind/namespace. _(read)_
  * `cluster_id` (required, string): Cluster ID.
  * `kind` (required, string): Resource kind, e.g. `Pod`, `Service`, `Deployment` (see `list_api_versions`).
  * `api_version` (required, string): e.g. `v1`, `apps/v1`, `networking.k8s.io/v1`.
  * `namespace` (optional, string): Omit = all namespaces.
  * `label_selector` (optional, string): e.g. `app=nginx,tier=frontend`.
  * `field_selector` (optional, string): e.g. `status.phase=Running`.
* **`manage_k8s_resource`** — CRUD a single K8s resource. _(read for `read`; write for create/replace/patch/delete; reading a Secret needs sensitive)_
  * `operation` (required, enum `create`|`replace`|`patch`|`delete`|`read`): Operation.
  * `cluster_id` (required, string): Cluster ID.
  * `kind` (required, string): Resource kind.
  * `api_version` (required, string): API version.
  * `name` (optional, string): Resource name — required for everything except `create`.
  * `namespace` (optional, string): Required for namespaced resources.
  * `body` (optional, object): Resource definition — required for create/replace/patch.
* **`apply_yaml`** — Apply YAML content (multi-document; equivalent to `kubectl apply`). _(write)_
  * `yaml_content` (required, string): The YAML itself, not a path (the server may run remotely).
  * `cluster_id` (required, string): Cluster ID.
  * `namespace` (required, string): Namespace for resources that do not declare one.
  * `force` (optional, bool, default `true`): `true` = update existing resources; `false` = create only.
* **`generate_app_manifest`** — Generate a Deployment + LoadBalancer Service manifest for an app. _(read)_
  * `app_name` (required, string): App name (used for Deployment/Service names and labels).
  * `image_uri` (required, string): Full image URI with tag, e.g. `vcr.vngcloud.vn/<repo>:<tag>`.
  * `port` (optional, int 1–65535, default `80`): Port the app listens on.
  * `replicas` (optional, int ≥1, default `2`): Number of replicas.
  * `cpu` (optional, string, default `100m`): CPU request/limit per container.
  * `memory` (optional, string, default `128Mi`): Memory request/limit per container.
  * `namespace` (optional, string, default `default`): Target namespace.
  * `load_balancer_scheme` (optional, enum `internal`|`internet-facing`, default `internal`): Rendered as the `vks.vngcloud.vn/scheme` annotation.
* **`get_pod_logs`** — Read logs from a pod. _(read, sensitive)_
  * `cluster_id` (required, string): Cluster ID.
  * `namespace` (required, string): The pod's namespace.
  * `pod_name` (required, string): Pod name.
  * `container_name` (optional, string): Required when the pod has multiple containers.
  * `since_seconds` (optional, int ≥0): Only logs newer than N seconds.
  * `tail_lines` (optional, int ≥1, default `100`): Number of trailing lines.
  * `limit_bytes` (optional, int ≥1, default `10240`): Byte limit (10KB).
  * `previous` (optional, bool, default `false`): Logs of the previously terminated container.
* **`get_k8s_events`** — Kubernetes events for one object. _(read, sensitive)_
  * `cluster_id` (required, string): Cluster ID.
  * `kind` (required, string): Kind of the involved object (e.g. `Pod`, `Deployment`).
  * `name` (required, string): Object name.
  * `namespace` (optional, string): Required for namespaced resources.
* **`list_api_versions`** — List the API versions available in the cluster. _(read)_
  * `cluster_id` (required, string): Cluster ID.

#### Version (1)

* **`list_cluster_versions`** — Kubernetes versions available for creating/upgrading a cluster. _(read)_
  * `refresh` (optional, bool): Bypass the cache and fetch fresh from the VKS API.

***

### Usage notes

* **Argument-based input, no resource URIs.** Every operation is a tool.
* **Auto-pagination** on `list_*` tools — no need to pass `page`.
* **Structured JSON output** for data tools — clients parse it directly.
* **Read-only by default** (29 tools). Writes need `--allow-write`; sensitive data needs `--allow-sensitive-data-access` — see Configure Local MCP. On the remote endpoint the access level is fixed by whoever deployed it.
* **Validate before creating.** For creates, call `validate_cluster_create` / `validate_nodegroup_create` (+ `get_quota`) before `create_*`. For deletes, call `*_dryrun` first.
