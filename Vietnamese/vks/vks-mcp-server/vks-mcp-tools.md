# VKS MCP Tools



VKS MCP Server cung cấp bộ tool để quản lý và tự động hóa tài nguyên **VKS — GreenNode Kubernetes Service**: cluster, node group, và các Kubernetes resource _bên trong_ cluster. Mọi thao tác đều expose dưới dạng **tool với input theo parameter** — không dùng resource URI.

### Tool groups

| Nhóm            | Mục đích                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------ |
| Cluster (13)    | List/xem/tạo/sửa/xóa cluster, xem events, lấy kubeconfig, cấu hình auto-upgrade và auto-healing. |
| Node group (10) | Tạo/sửa/xóa node group, đổi số node, autoscale, upgrade version, list node.                      |
| Kubernetes (7)  | Thao tác resource bên trong cluster: list/CRUD, apply YAML, pod log, event, API version.         |
| Version (1)     | Các Kubernetes version khả dụng để create/upgrade.                                               |

### Conventions

* **Naming `verb_noun`** (kiểu EKS), map 1:1 với greennode-cli (`list-clusters` ↔ `list_clusters`).
* **Access** ghi ở cuối mỗi dòng mô tả:
  * `read` — luôn khả dụng. Read-only mode mặc định đăng ký **29 tool**.
  * `write` — cần flag `--allow-write`. 12 tool cluster/node group **không được đăng ký** khi thiếu flag, agent không nhìn thấy chúng. Riêng `apply_yaml` và `manage_k8s_resource` luôn xuất hiện nhưng từ chối lúc gọi.
  * `read, sensitive` — cần flag `--allow-sensitive-data-access`. Nhóm này **luôn xuất hiện** trong tool list; thiếu flag thì báo lỗi khi gọi.
* **`region`** (`Literal["HCM-3", "HAN"]`, default `HCM-3`) là parameter optional của **hầu hết** tool — không liệt kê lại bên dưới. Không nhận `region`: `list_flavors`, `list_volume_types` (tự suy từ cluster), `get_creation_guide`, `generate_app_manifest`, `get_access_token`. Output `list_*` echo lại region đã query.
* **`refresh`** (bool, default `false`) trên các discovery tool: các tool này lưu tạm kết quả trong thời gian ngắn để phản hồi nhanh, nên đặt `refresh=true` để bỏ qua bản lưu tạm và lấy dữ liệu mới từ vServer — dùng khi vừa tạo/xóa resource trong console và muốn thấy ngay.
* **Annotations**: mỗi tool khai báo `readOnlyHint` / `destructiveHint` để client auto-approve read và cảnh báo trước destructive call. `destructiveHint=true` ở `delete_cluster`, `delete_nodegroup`, `delete_auto_upgrade`, `upgrade_nodegroup_version`, `manage_k8s_resource`.

***

### Supported Tools

#### Cluster (13)

* **`list_clusters`** — List mọi cluster trong một region (tự lấy hết mọi trang). _(read)_
  * Không parameter bắt buộc. Cluster là region-scoped — không thấy thì thử region còn lại.
* **`get_cluster`** — Chi tiết đầy đủ một cluster (structured). _(read)_
  * `cluster_id` (required, string): Cluster ID — resolve từ name qua `list_clusters`.
* **`get_cluster_kubeconfig`** — Kubeconfig YAML (quyền cluster-admin). Cluster mới: chạy `generate_kubeconfig` trước. _(read, sensitive)_
  * `cluster_id` (required, string): Cluster ID.
* **`get_cluster_events`** — Bảng events của cluster. _(read)_
  * `cluster_id` (required, string): Cluster ID.
  * `page` (optional, int ≥0): Số trang (bắt đầu từ 0).
  * `pageSize` (optional, int ≥1): Số item mỗi trang (default 20).
* **`validate_cluster_create`** — Validate create body mà không thực sự tạo. _(read)_
  * `body` (required, object `CreateClusterComboDto`): Body dự định gửi cho `create_cluster` (cùng cấu trúc — xem field bên dưới).
* **`delete_cluster_dryrun`** — Preview việc xóa cluster (gồm cả node group). _(read)_
  * `cluster_id` (required, string): Cluster ID.
*   **`create_cluster`** — Tạo cluster (chỉ control plane); thêm worker qua `create_nodegroup`. _(write)_

    * `body` (required, object `CreateClusterComboDto`): Cấu hình cluster.
      * `name` (required, string): Tên cluster (5–20 ký tự: chữ thường + số + gạch nối; đầu/cuối là chữ/số).
      * `version` (required, string): Kubernetes version (từ `list_cluster_versions`).
      * `networkType` (required, enum `CILIUM_OVERLAY`|`CILIUM_NATIVE_ROUTING`|`TIGERA`): Network type.
      * `vpcId` (required, string): VPC ID (từ `list_vpcs`).
      * `releaseChannel` (optional, enum `RAPID`|`STABLE`, default `STABLE`): Release channel.
      * `enablePrivateCluster` (optional, bool, default `false`): Cluster private hay không.
      * `enabledLoadBalancerPlugin` (optional, bool, default `true`): Bật load-balancer plugin.
      * `enabledBlockStoreCsiPlugin` (optional, bool, default `true`): Bật block-store CSI plugin.
      * `enabledServiceEndpoint` (optional, bool): Chỉ private cluster (default true ở đó); bỏ với public cluster.
      * `azStrategy` (optional, enum `SINGLE`|`MULTI`, default `SINGLE`): Availability-zone strategy. `MULTI` cần VPC đã bật vDNS.
      * `description` (optional, string ≤255): Mô tả — ASCII only (chữ, số, khoảng trắng và `-_.@`; không dấu tiếng Việt).
      * `subnetId` (optional, string): Subnet ID (từ `list_subnets`).
      * `cidr` (optional, string): Bắt buộc khi networkType là `CILIUM_OVERLAY` hoặc `TIGERA`.
      * `listSubnetIds` (optional, string\[]): Danh sách subnet ID cho cluster.
      * `nodeNetmaskSize` (optional, int): Node netmask size.
      * `autoUpgradeConfig` (optional, object): Lịch auto-upgrade.
        * `weekdays` (required, string): Ngày trong tuần, vd `Mon,Wed,Fri`.
        * `time` (required, string): Giờ `HH:mm`, vd `03:00`.
      * `autoHealingConfig` (optional, object): Cấu hình auto-healing.
        * `enableAutoHealing` (required, bool): Bật/tắt.
        * `maxUnhealthy` (optional, string): vd `2` hoặc `40%`.
        * `unhealthyRange` (optional, string): vd `[2-5]`.
        * `timeoutUnhealthy` (optional, int 5–180): Phút trước khi coi node unhealthy.
    * `poc` (optional, bool, default `false`): Cluster Proof-of-Concept.
    * `autoRenewal` (optional, bool, default `true`): Auto-renew subscription.

    > Secondary subnet **không** đặt ở cluster — mỗi node group tự khai `secondarySubnets` lúc tạo.
* **`update_cluster`** — Partial update; chỉ gửi field thay đổi (≥1). Name/description/release channel KHÔNG sửa ở đây. _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `body` (required, object `UpdateClusterDto`): Ít nhất 1 field.
    * `version` (optional, string): Version đích; bỏ = giữ nguyên.
    * `whitelistNodeCIDRs` (optional, string\[]): Bỏ = giữ nguyên.
    * `enabledLoadBalancerPlugin` (optional, bool): Toggle load-balancer plugin.
    * `enabledBlockStoreCsiPlugin` (optional, bool): Toggle block-store CSI plugin.
* **`delete_cluster`** — Xóa cluster (IRREVERSIBLE; dry-run trước). _(write)_
  * `cluster_id` (required, string): Cluster ID.
* **`configure_auto_upgrade`** — Đặt/đổi schedule auto-upgrade (bật auto-upgrade = gọi tool này). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `weekdays` (required, string): Ngày trong tuần, phẩy-ngăn-cách, vd `Mon,Wed,Fri`.
  * `time` (required, string): Giờ dạng `HH:mm`, vd `03:00`.
* **`delete_auto_upgrade`** — Tắt auto-upgrade (xóa schedule). _(write)_
  * `cluster_id` (required, string): Cluster ID.
* **`configure_auto_healing`** — Bật/tắt/tinh chỉnh node auto-healing (một tool cho mọi thay đổi). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `enable_auto_healing` (required, bool): Bật/tắt auto-healing.
  * `max_unhealthy` (optional, string): Số/tỷ lệ node unhealthy tối đa trước remediation, vd `2` hoặc `40%`.
  * `unhealthy_range` (optional, string): Range node unhealthy cho phép, vd `[3-5]`.
  * `timeout_unhealthy` (optional, int 5–180): Số phút trước khi coi node là unhealthy.
* **`generate_kubeconfig`** — Mint kubeconfig (async; bắt buộc một lần cho cluster mới). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `expiration_days` (required, int 1–365): Số ngày kubeconfig hết hạn (không có default).

#### Node group (10)

* **`list_nodegroups`** — Node group của một cluster. _(read)_
  * `cluster_id` (required, string): Cluster ID.
* **`get_nodegroup`** — Chi tiết đầy đủ node group (subnet, encryption, placement). _(read)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
* **`list_nodes`** — Mọi node của một node group (tự lấy hết mọi trang). _(read)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
* **`delete_nodegroup_dryrun`** — Preview việc xóa node group. _(read)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
* **`validate_nodegroup_create`** — Validate create body trước khi tạo (miễn phí, không mutate). _(read)_
  * `cluster_id` (required, string): Cluster node group sẽ join.
  * `body` (required, object `CreateNodeGroupDto`): Body dự định gửi cho `create_nodegroup` (cùng cấu trúc — xem field bên dưới).
* **`create_nodegroup`** — Tạo node group (parity đầy đủ với CLI). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `body` (required, object `CreateNodeGroupDto`): Cấu hình node group.
    * `name` (required, string): Tên (5–15 ký tự: chữ thường + số + gạch nối; đầu/cuối là chữ/số).
    * `flavorId` (required, string): Flavor ID (từ `list_flavors`).
    * `diskSize` (required, int 20–5000): Disk size (GB).
    * `diskType` (required, string): Volume type ID (từ `list_volume_types`).
    * `numNodes` (required, int 0–10): Số node.
    * `sshKeyId` (required, string): SSH key ID (từ `list_ssh_keys`).
    * `subnetId` (required, string): Subnet node join (từ `list_subnets`).
    * `secondarySubnets` (optional, string\[]): CHỈ cluster CILIUM\_NATIVE\_ROUTING (bắt buộc ở đó): các CIDR `secondary_subnets` của subnetId, copy verbatim từ `list_subnets` (vd `['10.5.60.0/22']`). Bỏ với networkType khác.
    * `os` (optional, enum `ubuntu`|`linux`|`rocky`, default `ubuntu`): OS image.
    * `enablePrivateNodes` (optional, bool, default `false`): `false` = node có public IP; `true` = private-only.
    * `enabledEncryptionVolume` (optional, bool, default `false`): `true` = mã hóa disk.
    * `securityGroups` (optional, string\[]): Security group ID (từ `list_security_groups`).
    * `labels` (optional, object `key=value`): Node labels.
    * `tags` (optional, object `key=value`): Node tags.
    * `taints` (optional, object\[]): Node taints.
      * `key` (required, string): Taint key.
      * `value` (optional, string, default rỗng): Taint value.
      * `effect` (required, enum `NoSchedule`|`PreferNoSchedule`|`NoExecute`): Effect.
    * `autoScaleConfig` (optional, object): Autoscaling bounds.
      * `minSize` (required, int ≥0): Số node tối thiểu.
      * `maxSize` (required, int ≥1): Số node tối đa.
    * `upgradeConfig` (optional, object, default SURGE 1/0): Cấu hình upgrade.
      * `maxSurge` (optional, int 1–100, default `1`): Node thêm trên desired khi upgrade.
      * `maxUnavailable` (optional, int 0–100, default `0`): Node unavailable khi upgrade (0 = rolling).
      * `strategy` (optional, string, default `SURGE`): Upgrade strategy.
    * `placementGroupConfigDto` (optional, object): Placement group.
      * `type` (required, enum `NEW`|`EXISTING`): Dùng group mới hay có sẵn.
      * `placementGroupId` (optional, string): Group ID khi type=EXISTING (từ `list_placement_groups`).
      * `placementGroupName` (optional, string): Group name khi type=NEW.
* **`update_nodegroup`** — Update size / security group / autoscale / upgrade config. Labels/tags/taints → dùng `update_nodegroup_metadata`. _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
  * `body` (required, object `UpdateNodeGroupDto`): Không field nào bắt buộc, nhưng phải có ít nhất 1.
    * `numNodes` (optional, int 0–10): Số node.
    * `securityGroups` (optional, string\[]): Security group ID.
    * `autoScaleConfig` (optional, object): Autoscaling bounds.
      * `minSize` (required, int ≥0): Số node tối thiểu.
      * `maxSize` (required, int ≥1): Số node tối đa.
    * `upgradeConfig` (optional, object): Cấu hình upgrade.
      * `maxSurge` (optional, int 1–100, default `1`): Node thêm trên desired khi upgrade.
      * `maxUnavailable` (optional, int 0–100, default `0`): Node unavailable khi upgrade (0 = rolling).
      * `strategy` (optional, string, default `SURGE`): Upgrade strategy.
* **`update_nodegroup_metadata`** — Update labels, tags, taints. _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
  * `body` (required, object `UpdateNodeGroupMetadataDto`): Ít nhất 1 field.
    * `labels` (optional, object `key=value`): Node labels.
    * `tags` (optional, object `key=value`): Node tags.
    * `taints` (optional, object\[]): Node taints.
      * `key` (required, string): Taint key.
      * `value` (optional, string, default rỗng): Taint value.
      * `effect` (required, enum `NoSchedule`|`PreferNoSchedule`|`NoExecute`): Effect.
* **`delete_nodegroup`** — Xóa node group (IRREVERSIBLE; dry-run trước). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
  * `force_delete` (required, bool): `true` = skip drain node (kill pod ngay — cho node group stuck/ERROR); `false` = drain trước.
* **`upgrade_nodegroup_version`** — Upgrade Kubernetes version của node group (IRREVERSIBLE, không downgrade). _(write)_
  * `cluster_id` (required, string): Cluster ID.
  * `nodegroup_id` (required, string): Node Group ID.
  * `kubernetes_version` (required, string): Version đích — xem `list_cluster_versions`.

#### Kubernetes (7)

Thao tác Kubernetes resource _bên trong_ cluster. Server tự lấy và cache kubeconfig từ VKS API — không cần setup `kubectl`.

* **`list_k8s_resources`** — List K8s resource theo kind/namespace. _(read)_
  * `cluster_id` (required, string): Cluster ID.
  * `kind` (required, string): Kind resource, vd `Pod`, `Service`, `Deployment` (xem `list_api_versions`).
  * `api_version` (required, string): vd `v1`, `apps/v1`, `networking.k8s.io/v1`.
  * `namespace` (optional, string): Bỏ trống = mọi namespace.
  * `label_selector` (optional, string): vd `app=nginx,tier=frontend`.
  * `field_selector` (optional, string): vd `status.phase=Running`.
* **`manage_k8s_resource`** — CRUD một K8s resource đơn lẻ. _(read cho `read`; write cho create/replace/patch/delete; đọc Secret cần sensitive)_
  * `operation` (required, enum `create`|`replace`|`patch`|`delete`|`read`): Thao tác.
  * `cluster_id` (required, string): Cluster ID.
  * `kind` (required, string): Kind resource.
  * `api_version` (required, string): API version.
  * `name` (optional, string): Tên resource — bắt buộc trừ `create`.
  * `namespace` (optional, string): Bắt buộc cho namespaced resource.
  * `body` (optional, object): Định nghĩa resource — bắt buộc cho create/replace/patch.
* **`apply_yaml`** — Apply nội dung YAML (multi-doc, tương đương `kubectl apply`). _(write)_
  * `yaml_content` (required, string): Nội dung YAML — truyền content, không phải path (server có thể chạy remote).
  * `cluster_id` (required, string): Cluster ID.
  * `namespace` (required, string): Namespace cho resource không khai báo namespace.
  * `force` (optional, bool, default `true`): `true` = update nếu đã tồn tại; `false` = chỉ tạo mới.
* **`generate_app_manifest`** — Sinh manifest Deployment + LoadBalancer Service cho một app. _(read)_
  * `app_name` (required, string): Tên app (đặt tên/label Deployment/Service).
  * `image_uri` (required, string): Image URI đầy đủ kèm tag, vd `vcr.vngcloud.vn/<repo>:<tag>`.
  * `port` (optional, int 1–65535, default `80`): Port app lắng nghe.
  * `replicas` (optional, int ≥1, default `2`): Số replica.
  * `cpu` (optional, string, default `100m`): CPU request/limit mỗi container.
  * `memory` (optional, string, default `128Mi`): Memory request/limit mỗi container.
  * `namespace` (optional, string, default `default`): Namespace deploy.
  * `load_balancer_scheme` (optional, enum `internal`|`internet-facing`, default `internal`): Render thành annotation `vks.vngcloud.vn/scheme`.
* **`get_pod_logs`** — Lấy log của pod. _(read, sensitive)_
  * `cluster_id` (required, string): Cluster ID.
  * `namespace` (required, string): Namespace của pod.
  * `pod_name` (required, string): Tên pod.
  * `container_name` (optional, string): Bắt buộc nếu pod nhiều container.
  * `since_seconds` (optional, int ≥0): Chỉ log mới hơn N giây.
  * `tail_lines` (optional, int ≥1, default `100`): Số dòng cuối.
  * `limit_bytes` (optional, int ≥1, default `10240`): Giới hạn byte (10KB).
  * `previous` (optional, bool, default `false`): Log của container đã terminate.
* **`get_k8s_events`** — Lấy Kubernetes event của một object. _(read, sensitive)_
  * `cluster_id` (required, string): Cluster ID.
  * `kind` (required, string): Kind của object (vd `Pod`, `Deployment`).
  * `name` (required, string): Tên object.
  * `namespace` (optional, string): Bắt buộc cho namespaced resource.
* **`list_api_versions`** — List các API version khả dụng trong cluster. _(read)_
  * `cluster_id` (required, string): Cluster ID.

#### Version (1)

* **`list_cluster_versions`** — Các Kubernetes version khả dụng để create/upgrade cluster. _(read_
  * `refresh` (optional, bool): Bỏ qua cache, fetch mới từ VKS API.

***

### Usage notes

* **Input theo parameter, không dùng resource URI.** Mọi thao tác là tool.
* **Auto-pagination** cho các `list_*` tool — không cần truyền `page`.
* **Structured JSON output** cho data tool — client parse trực tiếp.
* **Read-only mặc định** (29 tool). Write cần `--allow-write`; sensitive data cần `--allow-sensitive-data-access` — xem Configure Local MCP. Với remote endpoint, access level do phía deploy quyết định.
* **Validate trước khi tạo.** Create: gọi `validate_cluster_create` / `validate_nodegroup_create` (+ `get_quota`) trước `create_*`. Delete: gọi `*_dryrun` trước.
