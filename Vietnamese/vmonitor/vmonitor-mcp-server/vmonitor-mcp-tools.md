# vMonitor MCP Tools

vMonitor MCP Server cung cấp bộ tool để quản lý và tự động hóa **vMonitor Platform** — dịch vụ observability của GreenNode: dashboard & widget, metric query, alarm, infrastructure host, log, notification, quota & usage, và synthetic uptime monitor. Server đứng trước **năm API của vMonitor** (metric/dashboard, Log, notification, quota-usage, synthetic/uptime) sau một lớp xác thực IAM duy nhất — request tự động được route tới đúng API. Mọi thao tác đều expose dưới dạng **tool với input theo parameter** — không dùng resource URI.

### Tool groups

| Nhóm                           | Mục đích                                                                                                                 |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| Dashboards                     | List / xem / tạo / clone / cập nhật / xóa dashboard.                                                                     |
| Widgets, variables & views     | Thêm / sửa / di chuyển / resize widget; quản lý variable dùng chung và saved view.                                       |
| Metric query                   | Time-series và single-value statistic — dữ liệu phía sau mọi chart.                                                      |
| Metric catalogue & units       | Tên metric, dimension, value, đơn vị và override đơn vị theo từng user.                                                  |
| Infrastructure hosts           | Host chạy agent và host theo sản phẩm (vServer, vStorage, vDB, vLB, vBackup, vBandwidth, vAS) + metric snapshot của chúng.|
| Alarms                         | Alarm metric / log / change-detection: tạo / sửa / xóa, lịch sử và trạng thái.                                           |
| Integrations & metric API keys | Cài / gỡ tích hợp metric-source; cấp / thu hồi metric API key.                                                           |
| Logs — projects & search       | Log project, certificate, field mapping, search và export log.                                                           |
| Logs — archives & refills      | Đích export (archive) và job nạp lại (refill).                                                                            |
| Logs — pipelines & processors  | Processing pipeline, processor group, processor và library.                                                              |
| Logs — resource mappings       | Log mapping resource → project (vCDN, vDB, vLB, vStorage, vStorage bucket).                                              |
| Notifications                  | Channel xác thực qua OTP: Email, SMS, Slack, Webhook, Telegram, Teams.                                                    |
| Quota & usage                  | Đọc usage, catalogue tier / package, báo giá.                                                                             |
| Quota orders                   | Mua / resize / xóa quota — **tốn tiền**; mỗi đơn hàng đều có bước báo giá miễn phí.                                       |
| Synthetic                      | Uptime monitor và probing location.                                                                                       |
| Feature guide                  | Hướng dẫn từng bước cho mỗi tính năng tổng hợp.                                                                           |

### Conventions

* **Naming `verb_noun`**, mỗi nhóm tính năng một handler.
* **Access** ghi theo từng tool:
  * `read` — luôn khả dụng. Read-only mode mặc định đăng ký **110 tool**.
  * `write` — cần flag `--allow-write`. Các tool này **không được đăng ký** khi thiếu flag, nên agent không nhìn thấy chúng.
  * `destructive` — cũng cần `--allow-write`; tool xóa dữ liệu không thể hoàn tác hoặc tiêu tốn tiền. Client cảnh báo trước khi gọi.
* **Dịch vụ global**: vMonitor không có region — không tool nào nhận parameter `region`, và `GRN_DEFAULT_REGION` bị bỏ qua.
* **Annotations**: mỗi tool khai báo `readOnlyHint` / `destructiveHint` để client auto-approve read và cảnh báo trước destructive call.
* **Structured JSON output** với `outputSchema` + `structuredContent` — client parse trực tiếp.
* **Paging**: các list tool nhận `page` / `size` bắt đầu từ 1 (bỏ `page` để lấy tất cả ở những tool có ghi chú); các endpoint list của Log dùng paging envelope dựa trên `content`.
* **Tốn tiền**: các tool đặt hàng quota (`create_log_project`, `resize_*`) tiêu tốn tiền — luôn gọi `get_creation_price` / `get_resize_price` trước (miễn phí, và validate luôn payload).

***

### Supported Tools

#### Dashboards

| Tool                        | Access      | Mô tả                                                                                                        |
| --------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------ |
| `list_dashboards`           | read        | List dashboard; filter `searching_text` / `searching_field` (optional), phân trang `page` / `size` từ 1 (bỏ `page` để lấy tất cả). |
| `get_dashboard`             | read        | Một dashboard theo ID (kèm số widget).                                                                       |
| `get_dashboard_by_name`     | read        | Một dashboard theo đúng tên.                                                                                |
| `create_dashboard`          | write       | Tạo dashboard rỗng (chỉ cần `name`).                                                                         |
| `create_dashboard_clone`    | write       | Clone một dashboard thành dashboard mới.                                                                     |
| `update_dashboard`          | write       | Cập nhật cài đặt chung (dark mode, refresh, time range, selected view).                                      |
| `update_dashboard_name`     | write       | Đổi tên dashboard.                                                                                           |
| `update_dashboard_favorite` | write       | Đánh dấu / bỏ đánh dấu favorite.                                                                             |
| `delete_dashboard`          | destructive | Xóa dashboard (không thể hoàn tác).                                                                          |

#### Widgets, variables & views

| Tool                         | Access      | Mô tả                                                                                                              |
| ---------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------ |
| `list_dashboard_variables`   | read        | Các query variable dùng chung của dashboard.                                                                       |
| `get_dashboard_variable`     | read        | Một variable.                                                                                                      |
| `update_dashboard_variables` | write       | Thay danh sách variable của dashboard (thay cả list).                                                              |
| `list_dashboard_views`       | read        | Các preset query / filter / time-range đã lưu.                                                                     |
| `get_dashboard_view`         | read        | Một saved view.                                                                                                    |
| `create_dashboard_view`      | write       | Lưu trạng thái dashboard hiện tại thành một view có tên.                                                           |
| `update_dashboard_view`      | write       | Cập nhật trạng thái đã lưu của một view.                                                                           |
| `delete_dashboard_view`      | destructive | Xóa một saved view (không thể hoàn tác).                                                                           |
| `list_widgets`               | read        | Widget của dashboard **kèm metric query phía sau từng widget** — replay bằng `get_statistics_v2` mà không cần discovery dimension. |
| `get_widget`                 | read        | Một widget (chart config + graph spec).                                                                            |
| `create_widget`              | write       | Thêm widget (v2 `graphs` map; bỏ `layout` để tự đặt trên lưới 10 cột).                                              |
| `update_widget`              | write       | Sửa nội dung widget (mảng v1 `metricGraphs` / `logGraphs`).                                                        |
| `update_widget_v2`           | write       | Sửa nội dung widget (v2 `graphs` map).                                                                             |
| `update_widget_layout`       | write       | Di chuyển / resize widget và chỉnh time window của nó.                                                             |
| `delete_widget`              | destructive | Xóa widget (không thể hoàn tác).                                                                                   |

#### Metric query

| Tool                       | Access | Mô tả                                                                              |
| -------------------------- | ------ | ---------------------------------------------------------------------------------- |
| `get_statistics`           | read   | Dữ liệu time-series (lọc theo dimension, `group_by`, window) — dữ liệu phía sau chart. |
| `get_statistics_synthetic` | read   | Một giá trị tổng hợp đơn (chart number / single-stat).                             |
| `get_statistics_v2`        | read   | Statistic query có typed (`type` = `SIMPLE` / `CUSTOM` + body `data`) — replay nguyên văn query của widget. |

#### Metric catalogue & units

| Tool                           | Access      | Mô tả                                                                   |
| ------------------------------ | ----------- | ----------------------------------------------------------------------- |
| `get_metric_names`             | read        | Catalogue metric — điểm khởi đầu khi chọn metric.                        |
| `list_metric_dimension_names`  | read        | Mọi dimension key biết được trên các metric.                             |
| `list_metric_dimension_values` | read        | Các value đã quan sát của một dimension (vd: các host của `host`).       |
| `get_metric_dimensions`        | read        | Dimension của một metric + value đã quan sát của từng dimension.         |
| `list_metric_units`            | read        | Các đơn vị có thể gán cho metric.                                        |
| `list_metric_unit_mappings`    | read        | Mapping metric → đơn vị hiển thị trong info panel.                       |
| `create_metric_unit_mapping`   | write       | Override đơn vị hiển thị của một metric cho user hiện tại.               |
| `delete_metric_unit_mapping`   | destructive | Reset đơn vị hiển thị (gỡ override).                                     |

#### Infrastructure hosts

Host chạy agent (server có Metric Agent) và resource sản phẩm được giám sát như host. Nhóm `<type>` mở rộng thành một tool cho từng loại sản phẩm — `vserver`, `vstorage`, `vdb`, `vlb`, `vbackup`, `vbandwidth`, `vas` (vDB Kafka chỉ có tool list). Các tool list host luôn gửi `page` / `size` và nhận thêm filter `name` (optional).

| Tool                                            | Access      | Mô tả                                                     |
| ----------------------------------------------- | ----------- | --------------------------------------------------------- |
| `list_hosts`                                    | read        | Các infrastructure host chạy agent.                       |
| `get_host`                                      | read        | Một host chạy agent theo ID.                              |
| `get_host_metrics`                              | read        | Metric snapshot hiện tại của host (status + CPU / load / memory). |
| `update_host_enabled` / `update_host_disabled`  | write       | Mở lại / tạm dừng giám sát host chạy agent (agent vẫn cài).|
| `delete_host`                                   | destructive | Gỡ host khỏi danh sách Infrastructure (không thể hoàn tác).|
| `list_vserver_hosts` / `list_vstorage_hosts` / `list_vdb_hosts` / `list_vdb_kafka_hosts` / `list_vlb_hosts` / `list_vbackup_hosts` / `list_vbandwidth_hosts` / `list_vas_hosts` | read | List resource sản phẩm được giám sát như host. |
| `get_<type>_host_metrics`                       | read        | Metric snapshot của host theo sản phẩm.                   |
| `update_<type>_host`                            | write       | Bật / tắt giám sát host sản phẩm (body `{enabled}`).      |
| `delete_<type>_host`                            | destructive | Gỡ host sản phẩm (không thể hoàn tác).                    |

#### Alarms

Alarm metric, synthetic, log và change-detection. Body create / update là DTO phẳng, typed đầy đủ — `name` là field bắt buộc duy nhất.

| Tool                            | Access      | Mô tả                                                                     |
| ------------------------------- | ----------- | ------------------------------------------------------------------------- |
| `list_alarms`                   | read        | List alarm (lọc theo name / severity / status / type).                    |
| `get_alarm`                     | read        | Một alarm theo ID (kèm config theo loại).                                 |
| `get_metric_alarm_definition`   | read        | Định nghĩa evaluator phía trên của metric alarm.                          |
| `list_metric_alarm_histories`   | read        | Lịch sử metric alarm (id = `alarms[].id` của sub-alarm trong definition). |
| `get_synthetic_alarm_definition`| read        | Định nghĩa metric alarm dạng synthetic.                                   |
| `list_synthetic_alarm_histories`| read        | Lịch sử synthetic alarm (id = sub-alarm trong definition).                |
| `list_log_alarm_histories`      | read        | Lịch sử log alarm.                                                        |
| `get_log_alarm_status`          | read        | Trạng thái hiện tại của log alarm.                                        |
| `get_change_alarm`              | read        | Định nghĩa alarm change-detection (cần time window).                      |
| `list_change_alarm_histories`   | read        | Lịch sử change alarm (cần time window).                                   |
| `create_metric_alarm` / `update_metric_alarm` | write | Tạo / sửa metric alarm (severity / condition không phân biệt hoa-thường). |
| `delete_metric_alarm`           | destructive | Xóa metric alarm (không thể hoàn tác).                                    |
| `delete_metric_sub_alarm`       | destructive | Xóa sub-alarm của metric alarm tổng hợp.                                  |
| `create_log_alarm` / `update_log_alarm` | write  | Tạo / sửa log alarm.                                             |
| `delete_log_alarm`              | destructive | Xóa log alarm (không thể hoàn tác).                                       |
| `create_change_alarm` / `update_change_alarm` | write | Tạo / sửa alarm change-detection.                              |
| `delete_change_alarm`           | destructive | Xóa change alarm (không thể hoàn tác).                                    |
| `delete_change_alarm_history`   | destructive | Xóa lịch sử change alarm (không thể hoàn tác).                            |

#### Integrations & metric API keys

| Tool                         | Access      | Mô tả                                          |
| ---------------------------- | ----------- | ----------------------------------------------- |
| `list_integrations`          | read        | Các app metric-source cài được.                |
| `get_integration`            | read        | Một integration.                               |
| `update_integration_installed` / `update_integration_uninstalled` | write | Cài / gỡ một integration. |
| `delete_integration`         | destructive | Xóa integration (không thể hoàn tác).          |
| `list_metric_api_keys`       | read        | List metric API key.                           |
| `create_metric_api_key`      | write       | Cấp metric API key mới.                        |
| `delete_metric_api_key`      | destructive | Thu hồi metric API key (không thể hoàn tác).   |

#### Logs — projects, search & export

`search_logs` / `search_logs_default` nhận DSL có cấu trúc `{type,value}` (match / range / exists / bool; các cách viết tắt kiểu Elasticsearch được chuyển đổi).

| Tool                               | Access      | Mô tả                                                                          |
| ---------------------------------- | ----------- | ------------------------------------------------------------------------------- |
| `list_projects`                    | read        | Log project (Log API).                                                          |
| `get_project`                      | read        | Một log project.                                                                |
| `get_project_mappings`             | read        | Field mapping của project.                                                      |
| `get_project_log_data_exists`      | read        | Project có dữ liệu log đã ingest hay không.                                     |
| `search_logs` / `search_logs_default` | read     | Query dữ liệu project bằng DSL có cấu trúc.                                     |
| `get_log_export`                   | read        | Theo dõi một log export.                                                        |
| `get_project_certificate_download` | read        | Tải certificate của project (ZIP base64; `cert_id` từ `list_projects` → `certInfos[]`). |
| `update_project` / `update_project_mappings` | write | Sửa cài đặt / field mapping của project.                            |
| `create_project_certificate`       | write       | Cấp client certificate cho project.                                             |
| `delete_project_certificate`       | destructive | Thu hồi client certificate của project.                                         |
| `create_log_export`                | write       | Chuẩn bị log export bất đồng bộ.                                                |

#### Logs — archives & refills

| Tool                           | Access      | Mô tả                                        |
| ------------------------------ | ----------- | --------------------------------------------- |
| `list_archives` / `get_archive`| read        | Log archive (đích export).                    |
| `validate_archive_connection`  | read        | Kiểm tra kết nối storage của archive.         |
| `create_archive` / `update_archive` | write  | Tạo / sửa log archive.                        |
| `delete_archive`               | destructive | Xóa log archive.                              |
| `list_refills` / `get_refill`  | read        | Job refill log (nạp lại).                     |
| `validate_refill_connection`   | read        | Kiểm tra kết nối storage của refill.          |
| `create_refill` / `create_refill_from_archive` | write | Tạo job refill.               |
| `delete_refill`                | destructive | Xóa job refill.                               |

#### Logs — pipelines & processors

| Tool                                    | Access      | Mô tả                                                 |
| --------------------------------------- | ----------- | ------------------------------------------------------ |
| `list_pipelines` / `get_pipeline`       | read        | Processing pipeline của log.                           |
| `create_pipeline` / `update_pipeline`   | write       | Tạo / sửa pipeline.                                    |
| `delete_pipeline`                       | destructive | Xóa pipeline.                                          |
| `get_processor_group`                   | read        | Một processor group.                                   |
| `list_processor_group_libraries`        | read        | Processor group library.                               |
| `list_date_formats`                     | read        | Danh sách date format hỗ trợ.                          |
| `validate_grok_parser`                  | read        | Validate grok parser.                                  |
| `create_processor_group` / `update_processor_group` / `update_processor_order` / `create_processor_group_library` | write | Quản lý processor group và thứ tự. |
| `delete_processor_group`                | destructive | Xóa processor group.                                   |
| `create_processor` / `update_processor` | write       | Quản lý processor.                                     |
| `delete_processor`                      | destructive | Xóa processor.                                         |

#### Logs — resource mappings

Placeholder `<product>` mở rộng thành `vcdn`, `vdb`, `vlb`, `vstorage` (kèm tool riêng cho vStorage bucket).

| Tool                                                                  | Access | Mô tả                                            |
| --------------------------------------------------------------------- | ------ | ------------------------------------------------- |
| `list_<product>_log_mappings` (+ `list_vstorage_bucket_log_mappings`) | read   | Log mapping resource → project.                   |
| `list_vcdn_log_mapping_types` / `list_vstorage_log_mapping_regions`   | read   | Tra cứu loại mapping / region.                    |
| `update_<product>_log_mapping[_enabled\|_disabled]`                   | write  | Sửa / bật / tắt log mapping của resource.         |
| `update_vstorage_bucket_log_mapping`                                  | write  | Gán log mapping cho vStorage bucket.              |

#### Notifications

Việc tạo channel cần xác thực OTP: `create_notification_otp` → `validate_notification_otp` → `create_notification`. Channel gồm Email, SMS, Slack, Webhook, Telegram, Teams.

| Tool                         | Access      | Mô tả                                             |
| ---------------------------- | ----------- | -------------------------------------------------- |
| `list_notification_types`    | read        | Các loại channel.                                  |
| `list_notifications`         | read        | Các notification channel.                          |
| `get_notification_otp_info`  | read        | Thông tin OTP đang chờ.                           |
| `create_notification_otp`    | write       | Gửi OTP tới địa chỉ channel.                       |
| `validate_notification_otp`  | write       | Xác thực OTP.                                      |
| `create_notification` / `update_notification` | write | Tạo / sửa channel (đã xác thực OTP). |
| `delete_notification`        | destructive | Xóa notification channel (không thể hoàn tác).     |

#### Quota & usage (đọc — miễn phí)

| Tool                                                                                                                                                | Access | Mô tả                                            |
| ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------------------------------------------------- |
| `get_quota_usage` / `get_log_usage` / `get_composite_usage`                                                                                          | read   | Usage theo category / theo log project / gộp chung. |
| `get_current_quota` / `list_log_quotas` / `get_log_quota` / `get_quota_detail`                                                                       | read   | Quota đang hiệu lực và chi tiết.                   |
| `get_billing_settings` / `list_trash_quotas` / `get_convert_result`                                                                                  | read   | Billing settings / quota trong thùng rác / kết quả chuyển đổi. |
| `list_tiers` / `get_tier` / `get_tier_description`                                                                                                   | read   | Catalogue quota tier (metric / synthetic / log).   |
| `list_packages` / `get_package` / `get_package_detail` / `get_package_description` / `get_package_description_detail`                                 | read   | Catalogue package có thể mua.                      |
| `list_quota_classes` / `list_quota_class_packages`                                                                                                   | read   | Quota class v2 và package của chúng.               |
| `get_creation_price` / `get_resize_price` / `get_recovery_price` / `get_renewal_price`                                                               | read   | Báo giá (chưa đặt hàng).                           |

#### Quota orders (tốn tiền; chỉ với `--allow-write`)

Mỗi đơn hàng đều có pre-flight miễn phí qua `get_creation_price` / `get_resize_price`.

| Tool                    | Access      | Mô tả                                                                                     |
| ----------------------- | ----------- | ------------------------------------------------------------------------------------------ |
| `create_log_project`    | write       | Mua log project mới — đơn hàng log quota tạo project (**tốn tiền**).                       |
| `resize_log_project`    | destructive | Tăng quota / nâng Basic → Pro (**tốn tiền**, không thể hoàn tác).                          |
| `delete_log_project`    | destructive | Xóa project, quota và toàn bộ log đã lưu (không thể hoàn tác).                             |
| `resize_metric_quota`   | destructive | Resize metric quota duy nhất của account (**tốn tiền**, không thể hoàn tác).               |
| `resize_sms_quota` / `resize_email_quota` | destructive | Đổi quota notification SMS / email sang package khác (**tốn tiền**, không thể hoàn tác). |

Renew và recover-from-trash hiện chỉ dừng ở báo giá. Kết quả đơn hàng gồm `order_id`, `amount` và `payment_url` — `payment_url` khác rỗng nghĩa là **đang chờ** (quota chỉ thay đổi sau khi user thanh toán qua link đó); `pay: true` trừ tiền trực tiếp từ account.

#### Synthetic (uptime monitor & location)

| Tool                                                 | Access      | Mô tả                                              |
| ---------------------------------------------------- | ----------- | --------------------------------------------------- |
| `list_uptimes` / `get_uptime` / `get_uptime_config` / `validate_uptime` | read | Uptime monitor + preview probe.       |
| `create_uptime` / `update_uptime` / `update_uptime_status` | write | Tạo / sửa / bật-tắt monitor.           |
| `delete_uptime`                                      | destructive | Xóa monitor (không thể hoàn tác).                  |
| `list_locations` / `get_location`                    | read        | Các probing location của synthetic.                |
| `create_location` / `update_location`                | write       | Tạo / sửa private probing location.                |
| `delete_location`                                    | destructive | Xóa probing location (không thể hoàn tác).         |

#### Feature guide

| Tool                | Access | Mô tả                                                                                                                                     |
| ------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `get_feature_guide` | read   | Hướng dẫn từng bước cho một tính năng tổng hợp: `build_dashboard`, `query_metrics`, `create_metric_alarm`, `monitor_infrastructure`, `edit_metric_unit`, `manage_log_projects`, `manage_integrations`, `create_notification_channel`, `view_quota_usage`, `create_uptime_monitor`. |

***

### Prompts (11)

Server kèm **11 prompt** (tiếng Việt) — hướng dẫn tính năng từng bước, luôn khả dụng (không cần `--allow-write`). Load từ danh sách prompt của client (vd: prompt picker trong Claude Code), hoặc để agent gọi tool `get_feature_guide` với cùng feature key.

| Prompt                                 | Mục đích                                                                                  |
| -------------------------------------- | ------------------------------------------------------------------------------------------ |
| `vmonitor_getting_started`             | Onboarding: khái niệm, thiết lập auth, mô hình không region, routing tool, sơ đồ tính năng.|
| `vmonitor_build_dashboard`             | Dashboard + variable + view + widget (kèm cấu trúc `graphs` / auto-layout).               |
| `vmonitor_query_metrics`               | Query metric / vẽ dữ liệu, search & export log (kèm log search DSL).                      |
| `vmonitor_create_metric_alarm`         | Tạo alarm (metric / log / change-detection): nguồn → ngưỡng → notification → cổng xác nhận.|
| `vmonitor_monitor_infrastructure`      | Khám phá infrastructure host và metric của chúng.                                         |
| `vmonitor_edit_metric_unit`            | Override đơn vị hiển thị của metric.                                                       |
| `vmonitor_manage_log_projects`         | Quản lý log project, mapping, certificate.                                                 |
| `vmonitor_manage_integrations`         | Cài / gỡ tích hợp metric-source.                                                           |
| `vmonitor_create_notification_channel` | Tạo notification channel có xác thực OTP.                                                  |
| `vmonitor_view_quota_usage`            | Đọc quota usage và giá, rồi mua / resize / xóa quota.                                      |
| `vmonitor_create_uptime_monitor`       | Tạo synthetic uptime monitor + probing location.                                           |

### Key workflows

#### Đọc metric của một resource từ default dashboard

Mọi resource GreenNode đều có một **system dashboard** tự sinh, và mỗi widget lưu nguyên văn query mà console đang vẽ (tên metric, statistic, grouping, chuỗi `dimensions` đầy đủ mang `resource_id`). Vì vậy hỏi "server này đang thế nào?" không cần đi hết metric catalogue:

```
list_dashboards searching_text="<tên resource>"   →  dashboard id
list_widgets    dashboard_id=<id>                  →  metric_queries của từng widget
get_statistics_v2 body={"type":"SIMPLE","data":{"graph":{
    "name": <metric_name>, "statistics": <statistic>,
    "dimensions": <dimensions>,   # dùng nguyên văn
    "group_by": <group_by>, "offset":0, "limit":"", "rollup":"", "rate":0},
  "start_time":<epoch_ms>, "end_time":<epoch_ms>,
  "period":<period của widget>, "alarm":false}}
```

Dùng lại `period` của widget sẽ khớp đúng chart trên web. Widget có `log_graph_count > 0` đang vẽ dữ liệu log — query những widget đó bằng `search_logs`.

#### Mua hoặc resize quota (tốn tiền, `--allow-write`)

`packageId` nằm trong các retention entry của quota class, kèm các giới hạn mà `quantity` phải tuân theo. Lệnh báo giá vừa tính giá vừa validate payload:

```
list_quota_classes category=log       →  class → config.retentions[]:
                                         { amount: 7, minSize: 20, maxSize: 5000,
                                           step: 10, packageId: "<pkg>" }
quantity = <GB mỗi ngày> * <retention amount>          # log quota: GB-days
get_creation_price category=log package_id=<pkg> quantity=<n>   # chi phí 0
create_log_project body={"projectName":"my-logs",
                         "packageId":"<pkg>", "quantity":<n>}
```

Đừng đụng vào `redirectUrl` — mỗi tool đặt hàng tự điền trang quota của console vMonitor. Resize theo cùng cấu trúc (`get_resize_price` → `resize_log_project`; `resize_metric_quota` dùng số host và `minResource` / `maxResource` / `step`). SMS / email là bundle cố định từ `list_packages category=sms|email` — không có `quantity`.

### Usage notes

* **Input theo parameter, không dùng resource URI.** Mọi thao tác là một tool.
* **Read-only mặc định** (110 tool). Thao tác write cần `--allow-write` — xem Configure Local MCP. Với endpoint host sẵn, access level do người deploy cố định.
* **Báo giá trước khi đặt hàng, xem kỹ trước khi xóa.** Đơn hàng quota luôn có bước báo giá miễn phí; trước các lần xóa không thể hoàn tác, hãy đọc tool detail / history của resource trước.
* **Mọi infrastructure host đều có default dashboard tự sinh, read-only** — con đường nhanh nhất tới metric của một resource.
