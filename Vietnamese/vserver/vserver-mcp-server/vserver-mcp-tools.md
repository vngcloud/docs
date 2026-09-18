# vServer MCP Tools

**vServer MCP Server** expose **183 công cụ** với `--allow-write` và **84 công cụ** ở chế độ read-only mặc định. Mọi tool theo convention đặt tên EKS-style `verb_noun` (`list_servers`, `create_volume`, `delete_security_group`) và map 1:1 với tên lệnh greennode-cli khi có.

Mọi tool đều có **ToolAnnotation** MCP:

| Access        | Ý nghĩa                                                                                             |
| ------------- | --------------------------------------------------------------------------------------------------- |
| `read`        | Idempotent, không đổi state. Có sẵn ở read-only mode. Client có thể auto-approve.                   |
| `write`       | Tạo hoặc sửa state. Cần `--allow-write`. Có thể revert (đổi tên có thể đổi lại).                    |
| `destructive` | Xóa state hoặc ghi đè data (rollback, delete). Cần `--allow-write`. Client nên warn trước khi chạy. |

Tool trả về Pydantic model có cấu trúc — FastMCP emit `outputSchema` + `structuredContent` (JSON). Region là `Literal["HCM-3", "HAN"]` cố định; mọi output `list_*` echo lại region đã fetch.

### Guidance

| Tool                | Access | Mô tả                                                                                       |
| ------------------- | ------ | ------------------------------------------------------------------------------------------- |
| `get_feature_guide` | read   | Hướng dẫn từng bước cho một flow nhiều bước — gọi **đầu tiên** trong mọi flow create/manage |

`get_feature_guide` nhận một trong: `getting_started`, `create_server`, `manage_server`, `create_volume`, `create_network`, `secure_server`, `snapshot_and_restore`, `network_acl`, `connect_networks`, `high_availability`. Mỗi guide mô tả một feature — một capability ghép từ nhiều tool — và viết bằng tiếng Việt, giống các GreenNode MCP server khác. Cùng mười guide đó cũng có sẵn dưới dạng MCP prompt với prefix `vserver_`.

### Discovery

| Tool                      | Access | Mô tả                                                        |
| ------------------------- | ------ | ------------------------------------------------------------ |
| `get_access_token`        | read   | IAM token hiện tại, region và endpoint                       |
| `list_zones`              | read   | Các availability zone đang enabled — bước 1 của mọi flow tạo |
| `get_zone`                | read   | Một zone theo id; kiểm tra `enabled` trước khi đặt resource  |
| `list_flavor_families`    | read   | Các family instance (`general-purpose`, `gpu`)               |
| `list_flavor_codes`       | read   | Code nền tảng CPU/GPU                                        |
| `list_flavors`            | read   | Flavor theo family × code, lọc theo zone và capacity         |
| `get_flavor`              | read   | Một flavor theo id — flavor server đang chạy                 |
| `list_images`             | read   | Image OS hoặc GPU có thể boot, có filter theo tên            |
| `list_volume_types`       | read   | Tier IOPS đĩa trong một zone (ưu tiên NVMe, fallback SSD)    |
| `get_volume_type`         | read   | Một tier IOPS theo id                                        |
| `get_default_volume_type` | read   | Tier vServer fallback khi không chỉ định                     |
| `get_quota`               | read   | Quota project và usage hiện tại, theo region                 |

### Servers

| Tool                                           | Access      | Mô tả                                                    |
| ---------------------------------------------- | ----------- | -------------------------------------------------------- |
| `list_servers`                                 | read        | Các instance, kèm private/public IP và zone              |
| `get_server`                                   | read        | Một instance, với full nested detail                     |
| `list_server_interfaces`                       | read        | NIC nội bộ và ngoại của server                           |
| `list_server_security_groups`                  | read        | Group đang attach kèm effective rule inbound/outbound    |
| `list_server_actions`                          | read        | Audit trail các lệnh create, resize, reboot              |
| `list_subnet_servers`                          | read        | Server có interface trong một subnet                     |
| `get_server_console_url`                       | read        | URL console VNC trên trình duyệt, có thời hạn            |
| `get_server_console_log`                       | read        | Output serial-console (tail) — lỗi boot và kernel        |
| `get_server_external_interface`                | read        | Một elastic interface đang attach theo id                |
| `create_server`                                | write       | Tạo instance (các field billing/backup cố tình loại trừ) |
| `start_server`                                 | write       | Bật nguồn                                                |
| `stop_server`                                  | write       | Tắt nguồn                                                |
| `reboot_server`                                | write       | Reboot                                                   |
| `resize_server`                                | write       | Đổi flavor; restart instance                             |
| `rename_server`                                | write       | Đổi display name                                         |
| `update_server_security_groups`                | write       | Thay thế toàn bộ group đang attach                       |
| `create_server_image`                          | write       | Chụp instance thành user image tái sử dụng               |
| `attach_server_internal_interface`             | write       | Thêm NIC private trên subnet cho trước                   |
| `detach_server_internal_interfaces`            | destructive | Gỡ NIC private                                           |
| `attach_server_internal_interface_floating_ip` | write       | Thêm NIC private kèm public IP                           |
| `detach_server_internal_interface_floating_ip` | destructive | Gỡ NIC đó và giải phóng public IP                        |
| `attach_server_external_interface`             | write       | Gắn elastic interface vào                                |
| `detach_server_external_interface`             | destructive | Gỡ elastic interface ra                                  |
| `attach_server_floating_ip`                    | write       | Gắn public IP vào interface                              |
| `detach_server_floating_ip`                    | destructive | Gỡ public IP khỏi interface                              |
| `delete_server`                                | destructive | Xóa instance, tuỳ chọn kèm volume                        |

### Storage

| Tool                       | Access      | Mô tả                                       |
| -------------------------- | ----------- | ------------------------------------------- |
| `list_volumes`             | read        | Các volume block-storage                    |
| `get_volume`               | read        | Một volume                                  |
| `list_server_volumes`      | read        | Volume đang attach vào một server           |
| `get_server_boot_volume`   | read        | Chỉ root disk của server                    |
| `list_volume_history`      | read        | Thay đổi size và IOPS theo vòng đời volume  |
| `list_persistent_volumes`  | read        | Kubernetes PV được back bởi vServer storage |
| `list_user_images`         | read        | Custom image chụp từ server                 |
| `get_user_image`           | read        | Một user image                              |
| `create_volume`            | write       | Tạo volume trong một zone                   |
| `resize_volume`            | write       | Tăng size volume hoặc đổi tier IOPS         |
| `update_volume_type`       | write       | Chỉ chuyển volume sang tier IOPS khác       |
| `rename_volume`            | write       | Đổi display name                            |
| `attach_volume`            | write       | Attach vào server cùng zone                 |
| `detach_volume`            | destructive | Detach (unmount trong guest OS trước)       |
| `delete_volume`            | destructive | Xóa volume đã detach và data của nó         |
| `delete_persistent_volume` | destructive | Xóa Kubernetes PV (nên xóa qua cluster)     |
| `delete_user_image`        | destructive | Xóa user image                              |

### Snapshots

| Tool                            | Access      | Mô tả                                                                         |
| ------------------------------- | ----------- | ----------------------------------------------------------------------------- |
| `list_snapshot_policies`        | read        | Policy schedule (cadence + retention) — nguồn duy nhất của `snapshotPolicyId` |
| `list_server_snapshots`         | read        | Điểm snapshot của server                                                      |
| `list_volume_snapshots`         | read        | Điểm snapshot của volume                                                      |
| `get_server_snapshot_policy`    | read        | Cấu hình auto-snapshot của server (`configured=false` khi chưa set)           |
| `get_volume_snapshot_policy`    | read        | Cấu hình auto-snapshot của volume (IAM-gated)                                 |
| `list_shared_server_snapshots`  | read        | Ai được restore từ snapshot của server này (IAM-gated)                        |
| `create_server_snapshot`        | write       | Chụp server ngay, với retention period                                        |
| `create_volume_snapshot`        | write       | Chụp volume ngay, với retention period                                        |
| `create_server_snapshot_policy` | write       | Cài cấu hình snapshot cho server                                              |
| `update_server_snapshot_policy` | write       | Đổi policy schedule trên server                                               |
| `update_volume_snapshot_policy` | write       | Đổi policy schedule trên volume                                               |
| `enable_server_auto_snapshot`   | write       | Bật schedule server                                                           |
| `disable_server_auto_snapshot`  | write       | Tắt schedule server (điểm vẫn giữ)                                            |
| `enable_volume_auto_snapshot`   | write       | Bật schedule volume (cần server id đang attach)                               |
| `disable_volume_auto_snapshot`  | write       | Tắt schedule volume (điểm vẫn giữ)                                            |
| `rollback_server_snapshot`      | destructive | Revert server về một điểm — **phá hủy mọi thứ ghi sau đó**                    |
| `rollback_volume_snapshot`      | destructive | Revert volume về một điểm — **phá hủy mọi thứ ghi sau đó**                    |
| `delete_server_snapshot`        | destructive | Xóa một điểm recovery server                                                  |
| `delete_volume_snapshot`        | destructive | Xóa một điểm recovery volume                                                  |
| `delete_server_snapshot_policy` | destructive | Xóa cấu hình **và mọi điểm dưới nó**                                          |
| `delete_volume_snapshot_policy` | destructive | Xóa cấu hình **và mọi điểm dưới nó**                                          |
| `delete_shared_server_snapshot` | destructive | Thu hồi grant share                                                           |

### Networking

| Tool                               | Access      | Mô tả                                                    |
| ---------------------------------- | ----------- | -------------------------------------------------------- |
| `list_vpcs`                        | read        | VPC trong project                                        |
| `get_vpc`                          | read        | Một VPC                                                  |
| `list_active_vpcs`                 | read        | View của API về VPC nào dùng được (IAM-gated)            |
| `create_vpc`                       | write       | Tạo VPC                                                  |
| `update_vpc`                       | write       | Đổi tên VPC                                              |
| `delete_vpc`                       | destructive | Xóa VPC                                                  |
| `enable_vpc_dns`                   | write       | Bật private DNS trong VPC (one-way — không có disable)   |
| `list_subnets`                     | read        | Subnet của VPC (subnet pin zone của server)              |
| `get_subnet`                       | read        | Một subnet                                               |
| `create_subnet`                    | write       | Tạo subnet                                               |
| `update_subnet`                    | write       | Update subnet (name bắt buộc mỗi call)                   |
| `delete_subnet`                    | destructive | Xóa subnet                                               |
| `create_secondary_subnet`          | write       | Thêm CIDR phụ vào subnet                                 |
| `delete_secondary_subnet`          | destructive | Xóa CIDR phụ                                             |
| `list_security_groups`             | read        | Security group; `system=true` = platform-managed         |
| `get_security_group`               | read        | Một security group                                       |
| `list_security_group_servers`      | read        | Server đang attach group — blast radius                  |
| `create_security_group`            | write       | Tạo security group                                       |
| `update_security_group`            | write       | Update group (name bắt buộc mỗi call)                    |
| `delete_security_group`            | destructive | Xóa security group                                       |
| `list_security_group_rules`        | read        | Rule của group                                           |
| `get_security_group_rule`          | read        | Một rule                                                 |
| `list_security_group_rule_samples` | read        | 30 preset có tên của API (SSH, All TCP, All ICMP …)      |
| `create_security_group_rule`       | write       | Thêm rule (allow-only, stateful)                         |
| `update_security_group_rule`       | write       | Sửa description và tag (protocol / port / CIDR bất biến) |
| `delete_security_group_rule`       | destructive | Xóa rule                                                 |
| `list_floating_ips`                | read        | Public WAN IP và trạng thái attach                       |
| `list_elastic_ips`                 | read        | View console của public address (IAM-gated)              |
| `delete_floating_ip`               | destructive | Trả address về pool                                      |
| `list_network_interfaces`          | read        | Elastic network interface                                |
| `get_network_interface`            | read        | Một elastic network interface                            |
| `create_network_interface`         | write       | Tạo elastic network interface                            |
| `rename_network_interface`         | write       | Đổi display name                                         |
| `update_network_interface_tags`    | write       | Thay thế tag set                                         |
| `delete_network_interface`         | destructive | Xóa elastic network interface                            |
| `list_dhcp_options`                | read        | DHCP option set                                          |
| `get_dhcp_option`                  | read        | Một DHCP option set                                      |
| `list_dhcp_option_vpcs`            | read        | VPC bind với DHCP option set                             |
| `create_dhcp_option`               | write       | Tạo DHCP option set (2 DNS platform kèm; tối đa 4)       |
| `update_vpc_dhcp_option`           | write       | Bind/unbind set vào VPC                                  |
| `delete_dhcp_option`               | destructive | Xóa DHCP option set                                      |

Image hệ thống GreenNode chuyển remote admin khỏi port mặc định: SSH nghe trên **234** và RDP trên **3490**. `list_security_group_rule_samples` trả cả preset chuẩn (`SSH` 22, `RDP` 3389) và preset GreenNode (`SSH VNG` 234, `RDP VNG` 3490) — chọn theo image, không theo thói quen.

### Network ACL, route table và peering

| Tool                         | Access      | Mô tả                                                             |
| ---------------------------- | ----------- | ----------------------------------------------------------------- |
| `list_network_acls`          | read        | Firewall subnet-level; `is_default` không xóa được                |
| `get_network_acl`            | read        | Một ACL                                                           |
| `list_network_acl_rules`     | read        | Rule chia theo direction, theo thứ tự eval                        |
| `create_network_acl`         | write       | Tạo ACL trong VPC                                                 |
| `update_network_acl_rules`   | write       | Thay thế **toàn bộ** rule set — ACL stateless, cần cả 2 direction |
| `update_network_acl_subnets` | write       | Set subnet nào ACL quản (full replacement)                        |
| `delete_network_acl`         | destructive | Xóa ACL — subnet fallback về allow-all                            |
| `list_route_tables`          | read        | Route table của VPC                                               |
| `get_route_table`            | read        | Một route table                                                   |
| `list_route_table_routes`    | read        | Static route trong route table                                    |
| `create_route_table`         | write       | Tạo route table (name 5–50 ký tự)                                 |
| `update_route_table_routes`  | write       | Thay thế **toàn bộ** route set                                    |
| `delete_route_table`         | destructive | Xóa route table                                                   |
| `list_peerings`              | read        | VPC peering — **tạo phải qua GreenNode support**                  |
| `delete_peering`             | destructive | Gỡ peering (tạo lại cần support request)                          |

### Interconnect

| Tool                              | Access      | Mô tả                                                   |
| --------------------------------- | ----------- | ------------------------------------------------------- |
| `list_interconnects`              | read        | Circuit private tới on-prem, cloud khác hoặc region kia |
| `get_interconnect`                | read        | Một circuit                                             |
| `list_interconnect_packages`      | read        | Catalogue bandwidth package                             |
| `list_interconnect_circuit_types` | read        | Catalogue circuit type (IAM-gated)                      |
| `list_interconnect_connections`   | read        | VPC attachment trên circuit                             |
| `get_interconnect_connection`     | read        | Một VPC attachment                                      |
| `create_interconnect`             | write       | Đặt circuit — **có hợp đồng, tính phí monthly**         |
| `update_interconnect`             | write       | Description, tag, redundancy gateway-2                  |
| `update_interconnect_package`     | write       | Đổi bandwidth cam kết — **đổi giá**                     |
| `create_interconnect_connection`  | write       | Attach VPC vào circuit                                  |
| `update_interconnect_connection`  | write       | Đổi remote CIDR (full replacement)                      |
| `ping_interconnect`               | write       | Test chẩn đoán reachability (không đổi gì)              |
| `delete_interconnect_connection`  | destructive | Detach VPC khỏi circuit                                 |
| `delete_interconnect`             | destructive | Gỡ circuit                                              |

### Virtual IP

| Tool                                          | Access      | Mô tả                                          |
| --------------------------------------------- | ----------- | ---------------------------------------------- |
| `list_virtual_ips`                            | read        | Address chia sẻ cho HA pair, private và public |
| `get_virtual_ip`                              | read        | Một virtual IP                                 |
| `list_virtual_ip_address_pairs`               | read        | Interface nào answer cho private VIP           |
| `get_virtual_ip_address_pair`                 | read        | Một address pair                               |
| `list_virtual_ip_candidate_interfaces`        | read        | Interface nội bộ eligible join private VIP     |
| `list_public_virtual_ip_candidate_interfaces` | read        | Interface ngoại eligible join public VIP       |
| `list_secondary_subnet_address_pairs`         | read        | Interface bind với secondary subnet            |
| `create_virtual_ip`                           | write       | Tạo private VIP                                |
| `update_virtual_ip`                           | write       | Đổi tên hoặc mode private VIP                  |
| `create_public_virtual_ip`                    | write       | Tạo public VIP (tiêu public IP)                |
| `create_virtual_ip_address_pair`              | write       | Bind interface instance vào private VIP        |
| `create_public_virtual_ip_address_pair`       | write       | Bind interface ngoại vào public VIP            |
| `create_secondary_subnet_address_pair`        | write       | Bind interface vào secondary subnet            |
| `delete_virtual_ip_address_pair`              | destructive | Unbind interface khỏi private VIP              |
| `delete_public_virtual_ip_address_pair`       | destructive | Unbind interface ngoại khỏi public VIP         |
| `delete_secondary_subnet_address_pair`        | destructive | Unbind khỏi secondary subnet                   |
| `delete_virtual_ip`                           | destructive | Giải phóng address private chia sẻ             |
| `delete_public_virtual_ip`                    | destructive | Giải phóng address public chia sẻ              |

### Key, placement và tag

| Tool                            | Access      | Mô tả                                                 |
| ------------------------------- | ----------- | ----------------------------------------------------- |
| `list_ssh_keys`                 | read        | SSH key trong project                                 |
| `get_ssh_key`                   | read        | Một SSH key                                           |
| `create_ssh_key`                | write       | Generate pair; private key trả **một lần**            |
| `import_ssh_key`                | write       | Register public key có sẵn (ưu tiên)                  |
| `delete_ssh_key`                | destructive | Xóa key                                               |
| `list_placement_groups`         | read        | Placement group và server trong đó                    |
| `get_placement_group`           | read        | Một placement group                                   |
| `list_placement_group_policies` | read        | Policy affinity / anti-affinity                       |
| `create_placement_group`        | write       | Tạo placement group                                   |
| `update_placement_group`        | write       | Đổi tên hoặc policy                                   |
| `delete_placement_group`        | destructive | Xóa placement group rỗng                              |
| `list_tag_keys`                 | read        | Tag key trong project                                 |
| `list_tag_values`               | read        | Value dùng với một tag key                            |
| `list_resource_tags`            | read        | Tag attach vào một resource                           |
| `list_tags`                     | read        | Mọi tag object trong project (system tag ẩn mặc định) |
| `get_tag_quota`                 | read        | Một resource mang được bao nhiêu tag                  |
| `update_resource_tags`          | write       | Thay thế toàn bộ tag list của resource                |

### Prompts

Mười flow hướng dẫn có sẵn dưới dạng MCP prompt (tiếng Việt) — portable trên mọi MCP client, luôn available (không cần `--allow-write`). Mỗi prompt cũng được serve qua tool `get_feature_guide` (cùng text, một nguồn): prompt do user load, tool do agent tự gọi.

| Prompt                         | Phạm vi                                                          |
| ------------------------------ | ---------------------------------------------------------------- |
| `vserver_getting_started`      | Object model, region/zone, và cách tool chain lại với nhau       |
| `vserver_create_server`        | Discovery → validate → confirm → create → poll cho instance      |
| `vserver_manage_server`        | Power, resize, rename, attach/detach interface, security group   |
| `vserver_create_volume`        | Volume tier, rule zone, flow attach                              |
| `vserver_create_network`       | VPC + subnet + security group từ đầu                             |
| `vserver_secure_server`        | Preset security-group, ACL, giữ port khỏi mặc định               |
| `vserver_snapshot_and_restore` | Bảo vệ point-in-time, retention, rollback vs restore             |
| `vserver_network_acl`          | Firewall subnet-level: stateless, platform rule, replacement PUT |
| `vserver_connect_networks`     | Peering và interconnect — khi nào dùng cái nào                   |
| `vserver_high_availability`    | Virtual IP, secondary subnet, placement group cho HA pair        |

### Ngoài phạm vi

* **Bandwidth** (Network → Bandwidth trong console) không có API công khai — chỉ console. Field `bandwidth` trên flavor là NIC speed, là thứ khác.
* Marketplace, server live migration, custom flavor / zone allocation và vài endpoint internal dư được cố tình bỏ — xem `CLAUDE.md` của package để biết lý do từng endpoint.
