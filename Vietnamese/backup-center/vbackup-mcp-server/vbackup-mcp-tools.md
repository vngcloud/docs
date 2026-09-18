# vBackup MCP Tools

**vBackup MCP Server** expose **68 công cụ** với `--allow-write` và **41 công cụ** ở chế độ read-only mặc định. Mọi tool theo convention đặt tên EKS-style `verb_noun` (`list_backup_policies`, `create_backup_server`, `delete_backup_destination`).

Mọi tool đều có **ToolAnnotation** MCP:

| Access        | Ý nghĩa                                                                                                           |
| ------------- | ----------------------------------------------------------------------------------------------------------------- |
| `read`        | Idempotent, không đổi state. Có sẵn ở read-only mode. Client có thể auto-approve.                                 |
| `write`       | Tạo hoặc sửa state. Cần `--allow-write`. Có thể revert (swap schedule có thể swap lại).                           |
| `destructive` | Xóa destination, policy, backup server, backup database hoặc restore point. Cần `--allow-write`. Client nên warn. |

Tool trả về Pydantic model có cấu trúc — FastMCP emit `outputSchema` + `structuredContent` (JSON). Region là `Literal["HCM-3", "HAN"]` cố định; mọi output `list_*` echo lại region đã fetch.

### Catalogue và discovery

| Tool                     | Access | Mô tả                                                                                 |
| ------------------------ | ------ | ------------------------------------------------------------------------------------- |
| `list_backends`          | read   | Backend caller thấy được; `id` là `backendId` mọi create cần                          |
| `get_configuration`      | read   | Giới hạn platform mà policy phải tuân — interval hourly, ceiling retention, open hour |
| `list_protected_servers` | read   | ID instance đã có backup server (chỉ check membership)                                |

### Backup destination (Backup Location trong console)

| Tool                                    | Access      | Mô tả                                                                                  |
| --------------------------------------- | ----------- | -------------------------------------------------------------------------------------- |
| `list_backup_destinations`              | read        | Nơi backup lưu vào, kèm quota, usage, soft delete và lock                              |
| `get_backup_destination`                | read        | Một destination, đọc fresh — dùng để verify sau mỗi edit                               |
| `list_backup_destination_servers`       | read        | Resource vServer lưu ở đây; **delete sẽ phá hủy cái gì**                               |
| `list_backup_destination_databases`     | read        | Resource vDB lưu ở đây                                                                 |
| `list_backup_destination_tags`          | read        | Tag trên destination; `vng.*` do platform set, không edit được                         |
| `list_backup_destination_history`       | read        | Thay đổi config kèm attempt fail và value dùng; account-wide khi omit `destination_id` |
| `list_backup_products`                  | read        | Product vBackup phủ — string `product` mà create cần                                   |
| `list_backup_regions`                   | read        | Region storage theo product; create nhận `region_id`, **không** `id`                   |
| `create_backup_destination`             | write       | Tạo location: product, region, quota, soft delete, lock                                |
| `update_backup_destination_name`        | write       | Đổi tên; chỉ display name, id không đổi                                                |
| `update_backup_destination_max_quota`   | write       | Set ceiling GB — run FAIL khi chạm trần                                                |
| `update_backup_destination_soft_delete` | write       | Recycle bin; backup đã xóa vẫn tính phí trong retention                                |
| `update_backup_destination_vault_lock`  | write       | Retention lock — **trở permanent** với `changeDuration=0` hoặc khi change window hết   |
| `delete_backup_destination`             | destructive | Xóa location **và backup lưu trong đó**                                                |

### Backup policy

| Tool                           | Access      | Mô tả                                                         |
| ------------------------------ | ----------- | ------------------------------------------------------------- |
| `list_backup_policies`         | read        | Policy kèm `schedule.summary` flatten và số server dùng       |
| `get_backup_policy`            | read        | Một policy, cadence từng cái — đọc trước khi update           |
| `create_backup_policy`         | write       | Tạo schedule (toggle hourly/daily/weekly/monthly + retention) |
| `update_backup_policy`         | write       | Thay schedule wholesale; ảnh hưởng mọi server dùng            |
| `update_default_backup_policy` | write       | Thăng một policy lên default, hạ policy đang giữ              |
| `delete_backup_policy`         | destructive | Gỡ policy; từ chối khi còn server attach                      |

### Backup server (instance được bảo vệ)

| Tool                                    | Access      | Mô tả                                                                                       |
| --------------------------------------- | ----------- | ------------------------------------------------------------------------------------------- |
| `list_backup_servers`                   | read        | Server được bảo vệ kèm policy, destination và flag per-disk; filter theo `server_id`        |
| `get_backup_server`                     | read        | Một backup server, đọc fresh (list bị cache)                                                |
| `list_backup_server_volumes`            | read        | Disk nào include trong run, kèm size và usage                                               |
| `list_backup_server_points`             | read        | Restore point server giữ, kèm policy tại thời điểm run                                      |
| `get_backup_statistics`                 | read        | Coverage account và counter outcome — truyền `project_id`, không thì ratio không có ý nghĩa |
| `get_vserver_instance`                  | read        | Máy vServer đằng sau backup server (name, state, flavour, image)                            |
| `get_backup_server_point_download_urls` | read        | Link download signed cho restore point — **link là credential**                             |
| `create_backup_server`                  | write       | Bảo vệ instance với policy, destination và disk selection                                   |
| `update_backup_server_volumes`          | write       | Include hoặc exclude một disk khỏi các run sau này                                          |
| `update_backup_server_policy`           | write       | Attach schedule khác                                                                        |
| `update_backup_server_destination`      | write       | Hướng run sau này sang destination khác; point hiện tại giữ nguyên và vẫn tính phí          |
| `start_backup`                          | write       | Chạy backup ngay ("Back now"), ngoài schedule                                               |
| `enable_backup_server`                  | write       | Resume schedule đang pause                                                                  |
| `disable_backup_server`                 | write       | Pause schedule; restore point giữ và vẫn tính phí                                           |
| `delete_backup_server_point`            | destructive | Xóa MỘT restore point                                                                       |
| `delete_backup_server`                  | destructive | Xóa backup server **và mọi restore point nó giữ**                                           |

### Backup database (vDB instance được bảo vệ)

Nửa vDB của vBackup. Share policy, destination và history service với family backup-server nhưng không share gì khác — database không bao giờ xuất hiện trong listing backup-server, và mỗi call trả `200` với list rỗng thay vì error khi hỏi sai product.

| Tool                            | Access      | Mô tả                                                               |
| ------------------------------- | ----------- | ------------------------------------------------------------------- |
| `list_backup_databases`         | read        | Database được bảo vệ kèm engine, policy, destination và stored size |
| `get_backup_database`           | read        | Một backup database, đọc fresh (list bị cache)                      |
| `list_backup_database_points`   | read        | Restore point database giữ, kèm stored và uncompressed size         |
| `list_protected_databases`      | read        | ID vDB instance của một engine family đã được bảo vệ                |
| `list_databases`                | read        | Estate vDB kèm eligibility từng instance và lý do khi không         |
| `create_backup_database`        | write       | Bảo vệ MỘT vDB instance với policy và destination                   |
| `update_backup_database_policy` | write       | Attach schedule khác                                                |
| `start_database_backup`         | write       | Chạy backup ngay, ngoài schedule                                    |
| `enable_backup_database`        | write       | Resume schedule đang pause                                          |
| `disable_backup_database`       | write       | Pause schedule; restore point giữ và vẫn tính phí                   |
| `delete_backup_database_point`  | destructive | Xóa MỘT restore point                                               |
| `delete_backup_database`        | destructive | Xóa backup database **và mọi restore point nó giữ**                 |

Bốn rule trên family database dễ bị miss:

* **`databaseType` là `PostgresCluster` hoặc `RedisCluster`** — spelling cluster, không phải engine name. Value không nhận trả `200` với list rỗng thay vì error.
* **Chỉ deployment cluster mới backup được.** PostgreSQL single-node không eligible; `list_databases` nói vậy từng instance trong `ineligible_reason` thay vì omit im lặng.
* **Một backup location chứa tối đa MỘT backup database.** Dùng lại location đã có database bị từ chối với `The backup destination already contains resources.`
* **Vault lock trên location chặn cả hai delete**, trả `Your resource is being managed by Vault.` — khác 409 "being processed", retry không bao giờ giúp cho đến khi retention hết hạn.

### History

| Tool                            | Access | Mô tả                                                                                                                |
| ------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------- |
| `list_backup_history`           | read   | Run backup vServer mới nhất trước; **`from_date` — window mặc định chỉ 180 ngày**                                    |
| `list_restore_history`          | read   | Restore vServer đã xảy ra (server này không thể start)                                                               |
| `list_database_backup_history`  | read   | Run backup vDB, kèm compressed vs uncompressed size                                                                  |
| `list_database_restore_history` | read   | Restore vDB, và instance nào data được ghi vào                                                                       |
| `list_server_migration_history` | read   | Migration vServer (Start / Complete / Rollback) — phase `status` và `action` đạt tới đó là 2 field riêng; đọc cả hai |

History theo product và hai family không bao giờ trộn: run vDB không xuất hiện trong `list_backup_history`. Thay đổi config destination là trail thứ ba riêng — `list_backup_destination_history`, đọc account-wide khi omit `destination_id`.

### vServer projection

API publish một bản copy vServer-flavoured thứ hai của endpoint backup-server. Không phải duplicate: nó báo image của instance được chụp và per-disk detail của restore point, cái mà family generic không có.

| Tool                                | Access | Mô tả                                                                 |
| ----------------------------------- | ------ | --------------------------------------------------------------------- |
| `list_vserver_backup_servers`       | read   | Listing projection; `project_id` bắt buộc                             |
| `get_vserver_backup_server`         | read   | Một backup server, shape projection (IAM-gated)                       |
| `list_vserver_backup_server_points` | read   | Restore point kèm `server_info` — image đằng sau mỗi point            |
| `get_vserver_backup_server_point`   | read   | Một restore point, shape projection (IAM-gated)                       |
| `list_vserver_backup_volume_points` | read   | Bên trong restore point: disk nào, cái nào bootable                   |
| `get_vserver_backup_volume_point`   | read   | Một disk slice của restore point (IAM-gated)                          |
| `create_vserver_backup_servers`     | write  | Shortcut create dùng default policy và destination của platform       |
| `list_volume_usage`                 | read   | Size và used space của volume vServer — read biểu diễn dưới dạng POST |

### Metric (vMonitor)

| Tool                             | Access | Mô tả                                                                                  |
| -------------------------------- | ------ | -------------------------------------------------------------------------------------- |
| `get_backup_metrics`             | read   | Trend product-wide: backup server, server, storage used — cả hai region trong một call |
| `get_backup_destination_metrics` | read   | Trend per-location: usage và count success/failure; omit id để chart mọi location      |

Cả hai post fixed query tới vMonitor API của Backup Center. vMonitor publish đúng sáu metric vBackup, payload ship built-in và caller chỉ chọn time window — không có free-form metric query, vì metric name không nhận trả `200` rỗng thay vì error.

### Chẩn đoán và guidance

| Tool                | Access | Mô tả                                                    |
| ------------------- | ------ | -------------------------------------------------------- |
| `get_access_token`  | read   | IAM access token hiện tại, region và endpoint            |
| `get_feature_guide` | read   | Hướng dẫn từng bước cho một capability vBackup composite |

> Tool **IAM-gated** trả `403 IAM_PERMISSION_DENIED` cho caller thiếu grant, trong khi list sibling chạy được. 403 ở đây nghĩa là "không được phép", không bao giờ "không tồn tại" — docstring nêu tool list fallback.

### Prompts

Chín flow hướng dẫn có sẵn dưới dạng MCP prompt (tiếng Việt) — portable trên mọi MCP client, luôn available (không cần `--allow-write`). Mỗi prompt cũng được serve qua tool `get_feature_guide` (cùng text, một nguồn): prompt do user load, tool do agent tự gọi.

| Prompt                          | Phạm vi                                                                       |
| ------------------------------- | ----------------------------------------------------------------------------- |
| `vbackup_getting_started`       | Object model, region và backend, và vBackup khác snapshot vServer thế nào     |
| `vbackup_protect_server`        | Toàn bộ chain từ discovery tới tạo backup server                              |
| `vbackup_protect_database`      | Chain vDB: eligibility, chọn location và policy, và constraint delete         |
| `vbackup_manage_policy`         | Schedule, retention, và giới hạn platform để validate                         |
| `vbackup_check_backups`         | Backup đêm qua có chạy không, và tại sao fail                                 |
| `vbackup_inspect_restore_point` | Restore point thực sự giữ gì — và tại sao restore phải start trong console    |
| `vbackup_manage_backup_server`  | Statistic coverage, backup immediate, move destination, download và xóa point |
| `vbackup_manage_destination`    | Tạo, edit và xóa backup location — và setting nào trở irreversible            |
| `vbackup_reduce_backup_cost`    | Tìm backup tốn tiền mà không mang lại giá trị                                 |

### Giới hạn đã biết

* **Restore không thể start qua API này.** Gateway publish `list_restore_history` và không có endpoint trigger restore; restore thực hiện trong console.
* **`list_volume_usage` 404 trên server đã xóa.** Endpoint trả `404 "Not found volumeId <id>"` cho toàn request khi bất kỳ volume nào không còn tồn tại trong vServer. `list_volume_usage` báo id không đo được trong `missing_volume_ids`; dùng restore point để size backup của server đã xóa.
* **Snapshot policy nằm trong vServer**, không phải ở đây. `list_snapshot_policies` (và mọi thao tác snapshot server / volume) được expose bởi vServer MCP Server. Snapshot là block-level và khác backup.
