# vMonitor MCP Tools

vMonitor MCP Server provides tools to manage and automate the **vMonitor Platform** — GreenNode's observability service: dashboards & widgets, metric queries, alarms, infrastructure hosts, logs, notifications, quota & usage, and synthetic uptime monitors. The server fronts **five vMonitor APIs** (metric/dashboard, Log, notification, quota-usage, synthetic/uptime) behind a single IAM authentication — requests are routed to the right API automatically. Every operation is exposed as a **tool with argument-based input** — no resource URIs are used.

### Tool groups

| Group                          | Purpose                                                                                                                              |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| Dashboards                     | List / inspect / create / clone / update / delete dashboards.                                                                        |
| Widgets, variables & views     | Add / edit / move / resize widgets; manage shared variables and saved views.                                                         |
| Metric query                   | Time-series and single-value statistics — the data behind every chart.                                                               |
| Metric catalogue & units       | Metric names, dimensions, values, units and per-user unit overrides.                                                                |
| Infrastructure hosts           | Agent-based hosts and product hosts (vServer, vStorage, vDB, vLB, vBackup, vBandwidth, vAS) + their metric snapshots.                |
| Alarms                         | Metric / log / change-detection alarms: create / update / delete, histories and statuses.                                            |
| Integrations & metric API keys | Install / uninstall metric-source integrations; issue / revoke metric API keys.                                                      |
| Logs — projects & search       | Log projects, certificates, field mappings, log search and export.                                                                   |
| Logs — archives & refills      | Export destinations (archives) and re-ingest jobs (refills).                                                                         |
| Logs — pipelines & processors  | Processing pipelines, processor groups, processors and libraries.                                                                    |
| Logs — resource mappings       | Resource → project log mappings (vCDN, vDB, vLB, vStorage, vStorage bucket).                                                         |
| Notifications                  | OTP-verified channels: Email, SMS, Slack, Webhook, Telegram, Teams.                                                                  |
| Quota & usage                  | Usage reads, tier / package catalog, price quotes.                                                                                   |
| Quota orders                   | Buy / resize / delete quotas — **spends money**; every order has a zero-cost pre-flight quote.                                       |
| Synthetic                      | Uptime monitors and probing locations.                                                                                               |
| Feature guide                  | Step-by-step guide for each composite feature.                                                                                       |

### Conventions

* **`verb_noun` naming**, one handler per feature area.
* **Access** is noted per tool:
  * `read` — always available. The default read-only mode registers **110 tools**.
  * `write` — requires the `--allow-write` flag. These tools are **not registered** without it, so the agent cannot see them.
  * `destructive` — also requires `--allow-write`; the tool deletes data irreversibly or spends money. Clients warn before the call.
* **Global service**: vMonitor has no regions — no tool takes a `region` parameter, and `GRN_DEFAULT_REGION` is ignored.
* **Annotations**: every tool declares `readOnlyHint` / `destructiveHint` so clients can auto-approve reads and warn before destructive calls.
* **Structured JSON output** with `outputSchema` + `structuredContent` — clients parse it directly.
* **Paging**: list tools take 1-based `page` / `size` (omit `page` to fetch everything where noted); log list endpoints use a `content`-based paging envelope.
* **Money-spending**: quota-order tools (`create_log_project`, `resize_*`) spend money — always call `get_creation_price` / `get_resize_price` first (free, and it validates the payload).

***

### Supported Tools

#### Dashboards

| Tool                       | Access      | Description                                                                                                              |
| -------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| `list_dashboards`          | read        | List dashboards; optional `searching_text` / `searching_field` filter, 1-based `page` / `size` paging (omit `page` for all). |
| `get_dashboard`            | read        | Single dashboard by ID (includes widget count).                                                                          |
| `get_dashboard_by_name`    | read        | Single dashboard by exact name.                                                                                          |
| `create_dashboard`         | write       | Create an empty dashboard (only `name` required).                                                                        |
| `create_dashboard_clone`   | write       | Clone a dashboard into a new one.                                                                                        |
| `update_dashboard`         | write       | Update general settings (dark mode, refresh, time range, selected view).                                                 |
| `update_dashboard_name`    | write       | Rename a dashboard.                                                                                                      |
| `update_dashboard_favorite`| write       | Mark / unmark favorite.                                                                                                  |
| `delete_dashboard`         | destructive | Delete a dashboard (irreversible).                                                                                       |

#### Widgets, variables & views

| Tool                        | Access      | Description                                                                                                          |
| --------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------- |
| `list_dashboard_variables`  | read        | Shared query variables of a dashboard.                                                                               |
| `get_dashboard_variable`    | read        | One shared variable.                                                                                                 |
| `update_dashboard_variables`| write       | Replace a dashboard's variable list (whole-list replace).                                                            |
| `list_dashboard_views`      | read        | Saved query / filter / time-range presets.                                                                           |
| `get_dashboard_view`        | read        | One saved view.                                                                                                      |
| `create_dashboard_view`     | write       | Save the current dashboard state as a named view.                                                                    |
| `update_dashboard_view`     | write       | Update a saved view's stored state.                                                                                  |
| `delete_dashboard_view`     | destructive | Delete a saved view (irreversible).                                                                                  |
| `list_widgets`              | read        | Dashboard widgets **plus the metric query behind each** — replay via `get_statistics_v2` with no dimension discovery. |
| `get_widget`                | read        | One widget (chart config + graph specs).                                                                             |
| `create_widget`             | write       | Add a widget (v2 `graphs` map; omit `layout` to auto-place on the 10-column grid).                                    |
| `update_widget`             | write       | Edit widget content (v1 `metricGraphs` / `logGraphs` arrays).                                                        |
| `update_widget_v2`          | write       | Edit widget content (v2 `graphs` map).                                                                               |
| `update_widget_layout`      | write       | Move / resize a widget and adjust its time window.                                                                   |
| `delete_widget`             | destructive | Delete a widget (irreversible).                                                                                      |

#### Metric query

| Tool                    | Access | Description                                                                                          |
| ----------------------- | ------ | ---------------------------------------------------------------------------------------------------- |
| `get_statistics`        | read   | Time-series data (filter by dimensions, `group_by`, window) — the data behind a chart.               |
| `get_statistics_synthetic` | read | Single aggregated value (number / single-stat charts).                                               |
| `get_statistics_v2`     | read   | Typed statistic query (`type` = `SIMPLE` / `CUSTOM` + `data` body) — replays a widget's query as-is. |

#### Metric catalogue & units

| Tool                          | Access      | Description                                                                  |
| ----------------------------- | ----------- | ---------------------------------------------------------------------------- |
| `get_metric_names`            | read        | Metric catalogue — the starting point for picking a metric.                  |
| `list_metric_dimension_names` | read        | Every dimension key known across metrics.                                    |
| `list_metric_dimension_values`| read        | Observed values of one dimension (e.g. hosts for `host`).                    |
| `get_metric_dimensions`       | read        | A metric's dimensions + each dimension's observed values.                    |
| `list_metric_units`           | read        | Units assignable to a metric.                                                |
| `list_metric_unit_mappings`   | read        | Metric → unit mappings shown in info panels.                                 |
| `create_metric_unit_mapping`  | write       | Override a metric's display unit for the current user.                       |
| `delete_metric_unit_mapping`  | destructive | Reset the display unit (remove the override).                                |

#### Infrastructure hosts

Agent-based hosts (Metric Agent servers) plus product resources monitored as hosts. The `<type>` families expand to one tool per product type — `vserver`, `vstorage`, `vdb`, `vlb`, `vbackup`, `vbandwidth`, `vas` (vDB Kafka has a list tool only). Host-listing tools always send `page` / `size` and accept an optional `name` filter.

| Tool                                              | Access      | Description                                             |
| ------------------------------------------------- | ----------- | ------------------------------------------------------- |
| `list_hosts`                                      | read        | Agent-based infrastructure hosts.                       |
| `get_host`                                        | read        | One agent-based host by ID.                             |
| `get_host_metrics`                                | read        | Host's current metric snapshot (status + CPU / load / memory). |
| `update_host_enabled` / `update_host_disabled`    | write       | Resume / pause monitoring of an agent-based host (agent stays installed). |
| `delete_host`                                     | destructive | Remove an agent-based host from the Infrastructure list (irreversible). |
| `list_vserver_hosts` / `list_vstorage_hosts` / `list_vdb_hosts` / `list_vdb_kafka_hosts` / `list_vlb_hosts` / `list_vbackup_hosts` / `list_vbandwidth_hosts` / `list_vas_hosts` | read | List product resources monitored as hosts. |
| `get_<type>_host_metrics`                         | read        | Metric snapshot for a product host.                     |
| `update_<type>_host`                              | write       | Enable / disable monitoring for a product host (body `{enabled}`). |
| `delete_<type>_host`                              | destructive | Remove a product host (irreversible).                   |

#### Alarms

Metric, synthetic, log and change-detection alarms. Create / update bodies are flat, fully-typed DTOs — `name` is the only strictly required field.

| Tool                             | Access      | Description                                                                    |
| -------------------------------- | ----------- | ------------------------------------------------------------------------------ |
| `list_alarms`                    | read        | List alarms (filter by name / severity / status / type).                       |
| `get_alarm`                      | read        | One alarm by ID (with type-specific config).                                   |
| `get_metric_alarm_definition`    | read        | Metric alarm's upstream evaluator definition.                                  |
| `list_metric_alarm_histories`    | read        | Metric alarm history (id = a sub-alarm `alarms[].id` from the definition).     |
| `get_synthetic_alarm_definition` | read        | Synthetic metric alarm's definition.                                           |
| `list_synthetic_alarm_histories` | read        | Synthetic alarm history (id = sub-alarm from the definition).                  |
| `list_log_alarm_histories`       | read        | Log alarm history.                                                             |
| `get_log_alarm_status`           | read        | Log alarm's current status.                                                    |
| `get_change_alarm`               | read        | Change-detection alarm's definition (requires a time window).                  |
| `list_change_alarm_histories`    | read        | Change alarm history (requires a time window).                                 |
| `create_metric_alarm` / `update_metric_alarm` | write | Create / edit a metric alarm (severity / condition case-insensitive). |
| `delete_metric_alarm`            | destructive | Delete a metric alarm (irreversible).                                          |
| `delete_metric_sub_alarm`        | destructive | Delete a composite metric alarm's sub-alarm.                                   |
| `create_log_alarm` / `update_log_alarm`       | write      | Create / edit a log alarm.                                       |
| `delete_log_alarm`               | destructive | Delete a log alarm (irreversible).                                             |
| `create_change_alarm` / `update_change_alarm` | write      | Create / edit a change-detection alarm.                          |
| `delete_change_alarm`            | destructive | Delete a change alarm (irreversible).                                          |
| `delete_change_alarm_history`    | destructive | Clear change alarm history (irreversible).                                     |

#### Integrations & metric API keys

| Tool                          | Access      | Description                                       |
| ----------------------------- | ----------- | ------------------------------------------------- |
| `list_integrations`           | read        | Installable metric-source apps.                   |
| `get_integration`             | read        | One integration.                                  |
| `update_integration_installed` / `update_integration_uninstalled` | write | Install / uninstall an integration. |
| `delete_integration`          | destructive | Delete an integration (irreversible).             |
| `list_metric_api_keys`        | read        | List metric API keys.                             |
| `create_metric_api_key`       | write       | Issue a new metric API key.                       |
| `delete_metric_api_key`       | destructive | Revoke a metric API key (irreversible).           |

#### Logs — projects, search & export

`search_logs` / `search_logs_default` take a structured `{type,value}` DSL (match / range / exists / bool; Elasticsearch shorthands are translated).

| Tool                              | Access      | Description                                                                  |
| --------------------------------- | ----------- | ---------------------------------------------------------------------------- |
| `list_projects`                   | read        | Log projects (Log API).                                                      |
| `get_project`                     | read        | One log project.                                                             |
| `get_project_mappings`            | read        | A project's field mappings.                                                  |
| `get_project_log_data_exists`     | read        | Whether a log project has ingested data.                                     |
| `search_logs` / `search_logs_default` | read    | Query a project's data with the structured DSL.                              |
| `get_log_export`                  | read        | Track an asynchronous log export.                                            |
| `get_project_certificate_download`| read        | Download a project certificate (base64 ZIP; `cert_id` from `list_projects` → `certInfos[]`). |
| `update_project` / `update_project_mappings` | write | Edit a project's settings / field mappings.                     |
| `create_project_certificate`      | write       | Issue a project client certificate.                                          |
| `delete_project_certificate`      | destructive | Revoke a project client certificate.                                        |
| `create_log_export`               | write       | Prepare an asynchronous log export.                                          |

#### Logs — archives & refills

| Tool                          | Access      | Description                                |
| ----------------------------- | ----------- | ------------------------------------------ |
| `list_archives` / `get_archive` | read      | Log archives (export destinations).        |
| `validate_archive_connection` | read        | Test archive storage connectivity.         |
| `create_archive` / `update_archive` | write | Create / edit a log archive.             |
| `delete_archive`              | destructive | Delete a log archive.                      |
| `list_refills` / `get_refill` | read        | Log refill (re-ingest) jobs.               |
| `validate_refill_connection`  | read        | Test refill storage connectivity.          |
| `create_refill` / `create_refill_from_archive` | write | Create a refill job.        |
| `delete_refill`               | destructive | Delete a refill job.                       |

#### Logs — pipelines & processors

| Tool                                   | Access      | Description                                          |
| -------------------------------------- | ----------- | ---------------------------------------------------- |
| `list_pipelines` / `get_pipeline`      | read        | Log processing pipelines.                            |
| `create_pipeline` / `update_pipeline`  | write       | Create / edit a pipeline.                            |
| `delete_pipeline`                      | destructive | Delete a pipeline.                                   |
| `get_processor_group`                  | read        | One processor group.                                 |
| `list_processor_group_libraries`       | read        | Processor group libraries.                           |
| `list_date_formats`                    | read        | Date-format helpers.                                 |
| `validate_grok_parser`                 | read        | Validate a grok parser.                              |
| `create_processor_group` / `update_processor_group` / `update_processor_order` / `create_processor_group_library` | write | Manage processor groups and their order. |
| `delete_processor_group`               | destructive | Delete a processor group.                            |
| `create_processor` / `update_processor`| write       | Manage processors.                                   |
| `delete_processor`                     | destructive | Delete a processor.                                  |

#### Logs — resource mappings

The `<product>` placeholder expands to `vcdn`, `vdb`, `vlb`, `vstorage` (plus a dedicated vStorage bucket tool).

| Tool                                                                   | Access | Description                                        |
| ---------------------------------------------------------------------- | ------ | -------------------------------------------------- |
| `list_<product>_log_mappings` (+ `list_vstorage_bucket_log_mappings`)  | read   | Resource → project log mappings.                   |
| `list_vcdn_log_mapping_types` / `list_vstorage_log_mapping_regions`    | read   | Mapping type / region lookups.                     |
| `update_<product>_log_mapping[_enabled\|_disabled]`                    | write  | Edit / enable / disable a resource log mapping.    |
| `update_vstorage_bucket_log_mapping`                                   | write  | Set a vStorage bucket's log mapping.               |

#### Notifications

Channel creation is OTP-verified: `create_notification_otp` → `validate_notification_otp` → `create_notification`. Channels cover Email, SMS, Slack, Webhook, Telegram, Teams.

| Tool                        | Access      | Description                                        |
| --------------------------- | ----------- | -------------------------------------------------- |
| `list_notification_types`   | read        | Channel types.                                     |
| `list_notifications`        | read        | Notification channels.                             |
| `get_notification_otp_info` | read        | Pending OTP info.                                  |
| `create_notification_otp`   | write       | Send an OTP to a channel address.                  |
| `validate_notification_otp` | write       | Validate the OTP.                                  |
| `create_notification` / `update_notification` | write | Create / edit an (OTP-verified) channel. |
| `delete_notification`       | destructive | Delete a notification channel (irreversible).      |

#### Quota & usage (reads — free)

| Tool                                                                                                                                                 | Access | Description                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------------------------------------------------- |
| `get_quota_usage` / `get_log_usage` / `get_composite_usage`                                                                                          | read   | Usage per category / per log project / combined.   |
| `get_current_quota` / `list_log_quotas` / `get_log_quota` / `get_quota_detail`                                                                       | read   | Current active quota and its detail.               |
| `get_billing_settings` / `list_trash_quotas` / `get_convert_result`                                                                                  | read   | Billing settings / trashed quotas / conversion result. |
| `list_tiers` / `get_tier` / `get_tier_description`                                                                                                   | read   | Quota tier catalog (metric / synthetic / log).     |
| `list_packages` / `get_package` / `get_package_detail` / `get_package_description` / `get_package_description_detail`                                 | read   | Purchasable package catalog.                       |
| `list_quota_classes` / `list_quota_class_packages`                                                                                                   | read   | v2 quota classes and their packages.               |
| `get_creation_price` / `get_resize_price` / `get_recovery_price` / `get_renewal_price`                                                               | read   | Price quotes (no order placed).                    |

#### Quota orders (money-spending; `--allow-write` only)

Every order has a zero-cost pre-flight via `get_creation_price` / `get_resize_price`.

| Tool                   | Access      | Description                                                                                     |
| ---------------------- | ----------- | ----------------------------------------------------------------------------------------------- |
| `create_log_project`  | write       | Buy a new log project — the log quota order creates the project (**spends money**).             |
| `resize_log_project`  | destructive | Grow quota / upgrade Basic → Pro (**spends money**, irreversible).                              |
| `delete_log_project`  | destructive | Delete a project, its quota and stored logs (irreversible).                                     |
| `resize_metric_quota` | destructive | Resize the account's single metric quota (**spends money**, irreversible).                      |
| `resize_sms_quota` / `resize_email_quota` | destructive | Swap SMS / email notification quota to another package (**spends money**, irreversible). |

Renew and recover-from-trash remain quote-only. Orders respond with `order_id`, `amount` and `payment_url` — a non-empty `payment_url` means **pending** (the quota changes only after the user pays via that link); `pay: true` charges the account directly.

#### Synthetic (uptime monitors & locations)

| Tool                                            | Access      | Description                                       |
| ----------------------------------------------- | ----------- | ------------------------------------------------- |
| `list_uptimes` / `get_uptime` / `get_uptime_config` / `validate_uptime` | read | Uptime monitors + probe preview.       |
| `create_uptime` / `update_uptime` / `update_uptime_status` | write | Create / edit / toggle a monitor.        |
| `delete_uptime`                                 | destructive | Delete a monitor (irreversible).                  |
| `list_locations` / `get_location`               | read        | Synthetic probing locations.                      |
| `create_location` / `update_location`           | write       | Create / edit a private probing location.         |
| `delete_location`                               | destructive | Delete a probing location (irreversible).         |

#### Feature guide

| Tool               | Access | Description                                                                                                                              |
| ------------------ | ------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `get_feature_guide`| read   | Step-by-step guide for a composite feature: `build_dashboard`, `query_metrics`, `create_metric_alarm`, `monitor_infrastructure`, `edit_metric_unit`, `manage_log_projects`, `manage_integrations`, `create_notification_channel`, `view_quota_usage`, `create_uptime_monitor`. |

***

### Prompts (11)

The server ships **11 prompts** (Vietnamese) — step-by-step feature guides, always available (no `--allow-write` needed). Load them from the client's prompt list (e.g. the prompt picker in Claude Code), or let the agent call the `get_feature_guide` tool with the same feature key.

| Prompt                              | Purpose                                                                           |
| ----------------------------------- | --------------------------------------------------------------------------------- |
| `vmonitor_getting_started`          | Onboarding: concepts, auth setup, no-region model, tool routing, feature map.     |
| `vmonitor_build_dashboard`          | Dashboards + variables + views + widgets (incl. the `graphs` / auto-layout shape).|
| `vmonitor_query_metrics`            | Query metrics / plot data, search & export logs (incl. the log search DSL).       |
| `vmonitor_create_metric_alarm`      | Create an alarm (metric / log / change-detection): source → threshold → notification → confirm gate. |
| `vmonitor_monitor_infrastructure`   | Explore infrastructure hosts and their metrics.                                   |
| `vmonitor_edit_metric_unit`         | Override a metric's display unit.                                                 |
| `vmonitor_manage_log_projects`      | Manage log projects, mappings, certificates.                                      |
| `vmonitor_manage_integrations`      | Install / uninstall metric-source integrations.                                   |
| `vmonitor_create_notification_channel` | OTP-verified notification-channel creation.                                    |
| `vmonitor_view_quota_usage`         | Read quota usage and prices, then buy / resize / delete a quota.                  |
| `vmonitor_create_uptime_monitor`    | Create a synthetic uptime monitor + probing location.                             |

### Key workflows

#### Read a resource's metrics off its default dashboard

Every GreenNode resource owns an auto-generated **system dashboard**, and each widget stores the exact query the console plots (metric name, statistic, grouping, full `dimensions` string carrying the `resource_id`). So "how is this server doing?" needs no metric-catalogue walk:

```
list_dashboards searching_text="<resource name>"   →  dashboard id
list_widgets    dashboard_id=<id>                  →  metric_queries per widget
get_statistics_v2 body={"type":"SIMPLE","data":{"graph":{
    "name": <metric_name>, "statistics": <statistic>,
    "dimensions": <dimensions>,   # use as-is
    "group_by": <group_by>, "offset":0, "limit":"", "rollup":"", "rate":0},
  "start_time":<epoch_ms>, "end_time":<epoch_ms>,
  "period":<widget's period>, "alarm":false}}
```

Reusing the widget's `period` matches the web chart. Widgets with `log_graph_count > 0` plot log data — query those with `search_logs`.

#### Buy or resize a quota (money-spending, `--allow-write`)

`packageId` lives on a quota class's retention entries, along with the bounds the `quantity` must respect. The quote call both prices and validates the payload:

```
list_quota_classes category=log       →  class → config.retentions[]:
                                         { amount: 7, minSize: 20, maxSize: 5000,
                                           step: 10, packageId: "<pkg>" }
quantity = <GB per day> * <retention amount>          # log quota: GB-days
get_creation_price category=log package_id=<pkg> quantity=<n>   # zero cost
create_log_project body={"projectName":"my-logs",
                         "packageId":"<pkg>", "quantity":<n>}
```

Leave `redirectUrl` alone — each order tool fills in the vMonitor console's quota page automatically. Resizing follows the same shape (`get_resize_price` → `resize_log_project`; `resize_metric_quota` uses host counts and `minResource` / `maxResource` / `step`). SMS / email are fixed bundles from `list_packages category=sms|email` — no `quantity`.

### Usage notes

* **Argument-based input, no resource URIs.** Every operation is a tool.
* **Read-only by default** (110 tools). Writes need `--allow-write` — see Configure Local MCP. On a hosted endpoint the access level is fixed by whoever deployed it.
* **Quote before ordering, inspect before deleting.** Quota orders always have a free pre-flight quote; before irreversible deletes, read the resource's detail / history tools first.
* **Every infrastructure host owns an auto-generated, read-only default dashboard** — the fastest path to a resource's metrics.
