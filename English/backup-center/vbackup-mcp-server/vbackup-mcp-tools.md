# vBackup MCP Tools

**vBackup MCP Server** exposes **68 tools** with `--allow-write` and **41 tools** in the default read-only mode. Every tool follows the EKS-style `verb_noun` naming convention (`list_backup_policies`, `create_backup_server`, `delete_backup_destination`).

Every tool carries an MCP **ToolAnnotation**:

| Access        | Meaning                                                                                                                                |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `read`        | Idempotent, no state change. Available in read-only mode. Clients can auto-approve.                                                    |
| `write`       | Creates or modifies state. Requires `--allow-write`. Reversible (a schedule swap can be swapped back).                                 |
| `destructive` | Deletes a destination, a policy, a backup server, a backup database or a restore point. Requires `--allow-write`. Clients should warn. |

Data tools return structured Pydantic models — FastMCP emits `outputSchema` + `structuredContent` (JSON). Region is a fixed `Literal["HCM-3", "HAN"]`; every `list_*` output echoes back the region it was fetched from.

### Catalogue and discovery

| Tool                     | Access | Description                                                                              |
| ------------------------ | ------ | ---------------------------------------------------------------------------------------- |
| `list_backends`          | read   | Backends visible to the caller; `id` is the `backendId` every create needs               |
| `get_configuration`      | read   | Platform limits a policy must respect — hourly intervals, retention ceilings, open hours |
| `list_protected_servers` | read   | Instance IDs that already have a backup server (membership check only)                   |

### Backup destinations (the console's _Backup Location_)

| Tool                                    | Access      | Description                                                                                             |
| --------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------- |
| `list_backup_destinations`              | read        | Where backups land, with quota, usage, soft delete and lock                                             |
| `get_backup_destination`                | read        | One destination, read fresh — how every edit is verified                                                |
| `list_backup_destination_servers`       | read        | vServer resources stored here; **what a delete would destroy**                                          |
| `list_backup_destination_databases`     | read        | vDB resources stored here                                                                               |
| `list_backup_destination_tags`          | read        | Tags on a destination; `vng.*` are platform-set and not editable                                        |
| `list_backup_destination_history`       | read        | Config changes incl. failed attempts and the values used; account-wide when `destination_id` is omitted |
| `list_backup_products`                  | read        | Products vBackup covers — the `product` string a create needs                                           |
| `list_backup_regions`                   | read        | Storage regions per product; a create takes `region_id`, **not** `id`                                   |
| `create_backup_destination`             | write       | Create a location: product, region, quota, soft delete, lock                                            |
| `update_backup_destination_name`        | write       | Rename; display name only, ids are unaffected                                                           |
| `update_backup_destination_max_quota`   | write       | Set the GB ceiling — runs FAIL once it is reached                                                       |
| `update_backup_destination_soft_delete` | write       | Recycle bin; deleted backups stay billed for the retention                                              |
| `update_backup_destination_vault_lock`  | write       | Retention lock — **becomes permanent** with `changeDuration=0` or after the change window expires       |
| `delete_backup_destination`             | destructive | Delete the location **and the backups stored in it**                                                    |

### Backup policies

| Tool                           | Access      | Description                                                                |
| ------------------------------ | ----------- | -------------------------------------------------------------------------- |
| `list_backup_policies`         | read        | Policies with a flattened `schedule.summary` and how many servers use each |
| `get_backup_policy`            | read        | One policy, cadence by cadence — read before updating                      |
| `create_backup_policy`         | write       | Create a schedule (hourly/daily/weekly/monthly toggles + retention)        |
| `update_backup_policy`         | write       | Replace a schedule wholesale; affects every server using it                |
| `update_default_backup_policy` | write       | Make one policy the default, demoting whichever holds it now               |
| `delete_backup_policy`         | destructive | Remove a policy; refused while servers are attached                        |

### Backup servers (protected instances)

| Tool                                    | Access      | Description                                                                           |
| --------------------------------------- | ----------- | ------------------------------------------------------------------------------------- |
| `list_backup_servers`                   | read        | Protected servers with policy, destination and per-disk flags; filter by `server_id`  |
| `get_backup_server`                     | read        | One backup server, read fresh (the list is cached)                                    |
| `list_backup_server_volumes`            | read        | Which disks are included in runs, with size and usage                                 |
| `list_backup_server_points`             | read        | Restore points a server holds, with the policy as it was at run time                  |
| `get_backup_statistics`                 | read        | Account coverage and outcome counters — pass `project_id` or the ratio is meaningless |
| `get_vserver_instance`                  | read        | The vServer machine behind a backup server (name, state, flavour, image)              |
| `get_backup_server_point_download_urls` | read        | Signed download links for a restore point — **the links are credentials**             |
| `create_backup_server`                  | write       | Protect instances with a chosen policy, destination and disk selection                |
| `update_backup_server_volumes`          | write       | Include or exclude one disk from future runs                                          |
| `update_backup_server_policy`           | write       | Attach a different schedule                                                           |
| `update_backup_server_destination`      | write       | Write future runs elsewhere; existing points stay put and stay billed                 |
| `start_backup`                          | write       | Run a backup now ("Back now"), outside the schedule                                   |
| `enable_backup_server`                  | write       | Resume a paused schedule                                                              |
| `disable_backup_server`                 | write       | Pause the schedule; restore points are kept and still billed                          |
| `delete_backup_server_point`            | destructive | Delete ONE restore point                                                              |
| `delete_backup_server`                  | destructive | Delete the backup server **and every restore point it holds**                         |

### Backup databases (protected vDB instances)

The vDB half of vBackup. It shares policies, destinations and the history service with the backup-server family but nothing else — a database never appears in a backup-server listing, and each call answers `200` with an empty list rather than an error when asked about the wrong product.

| Tool                            | Access      | Description                                                                |
| ------------------------------- | ----------- | -------------------------------------------------------------------------- |
| `list_backup_databases`         | read        | Protected databases with engine, policy, destination and stored size       |
| `get_backup_database`           | read        | One backup database, read fresh (the list is cached)                       |
| `list_backup_database_points`   | read        | Restore points a database holds, with stored and uncompressed sizes        |
| `list_protected_databases`      | read        | vDB instance ids of one engine family that are already protected           |
| `list_databases`                | read        | The vDB estate with per-instance eligibility and the reason when it is not |
| `create_backup_database`        | write       | Protect ONE vDB instance with a chosen policy and destination              |
| `update_backup_database_policy` | write       | Attach a different schedule                                                |
| `start_database_backup`         | write       | Run a backup now, outside the schedule                                     |
| `enable_backup_database`        | write       | Resume a paused schedule                                                   |
| `disable_backup_database`       | write       | Pause the schedule; restore points are kept and still billed               |
| `delete_backup_database_point`  | destructive | Delete ONE restore point                                                   |
| `delete_backup_database`        | destructive | Delete the backup database **and every restore point it holds**            |

Four rules on the database family are easy to miss:

* **`databaseType` is `PostgresCluster` or `RedisCluster`** — a cluster spelling, not an engine name. An unrecognised value answers `200` with an empty list rather than an error.
* **Only cluster deployments can be backed up.** A single-node PostgreSQL is ineligible; `list_databases` says so per instance in `ineligible_reason` instead of silently omitting it.
* **A backup location holds at most one backup database.** Reusing an occupied one is refused with `The backup destination already contains resources.`
* **A vault lock on the location blocks both deletes**, answering `Your resource is being managed by Vault.` — unlike the "being processed" 409, retrying never helps until the retention expires.

### History

| Tool                            | Access | Description                                                                                                                           |
| ------------------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| `list_backup_history`           | read   | vServer backup runs newest-first; **`from_date` — the default window is only 180 days**                                               |
| `list_restore_history`          | read   | vServer restores that have happened (this server cannot start one)                                                                    |
| `list_database_backup_history`  | read   | vDB backup runs, with compressed vs uncompressed size                                                                                 |
| `list_database_restore_history` | read   | vDB restores, and which instance the data was written into                                                                            |
| `list_server_migration_history` | read   | vServer migrations (Start / Complete / Rollback) — the `status` phase and the `action` that reached it are separate fields; read both |

History is per-product and the two families never mix: a vDB run does not appear in `list_backup_history`. Configuration changes to a destination are a third, separate trail — `list_backup_destination_history`, which reads account-wide when `destination_id` is omitted.

### vServer projection

The API publishes a second, vServer-flavoured copy of the backup-server endpoints. It is not a duplicate: it reports the captured instance's image and a restore point's per-disk detail, which the generic family does not.

| Tool                                | Access | Description                                                         |
| ----------------------------------- | ------ | ------------------------------------------------------------------- |
| `list_vserver_backup_servers`       | read   | Projection listing; `project_id` is required                        |
| `get_vserver_backup_server`         | read   | One backup server, projection shape (IAM-gated)                     |
| `list_vserver_backup_server_points` | read   | Restore points with `server_info` — the image behind each point     |
| `get_vserver_backup_server_point`   | read   | One restore point, projection shape (IAM-gated)                     |
| `list_vserver_backup_volume_points` | read   | What is inside a restore point: which disk, which was bootable      |
| `get_vserver_backup_volume_point`   | read   | One disk slice of a restore point (IAM-gated)                       |
| `create_vserver_backup_servers`     | write  | Shortcut create using the platform's default policy and destination |
| `list_volume_usage`                 | read   | Size and used space of vServer volumes — a read expressed as a POST |

### Metrics (vMonitor)

| Tool                             | Access | Description                                                                               |
| -------------------------------- | ------ | ----------------------------------------------------------------------------------------- |
| `get_backup_metrics`             | read   | Product-wide trend: backup servers, servers, storage used — both regions in one call      |
| `get_backup_destination_metrics` | read   | Per-location trend: usage and success/failure counts; omit the id to chart every location |

Both post fixed queries to the Backup Center's vMonitor API. vMonitor publishes exactly six vBackup metrics, so the payloads ship built in and the caller chooses only the time window — there is no free-form metric query, because an unknown metric name returns an empty `200` rather than an error.

### Diagnostics and guidance

| Tool                | Access | Description                                              |
| ------------------- | ------ | -------------------------------------------------------- |
| `get_access_token`  | read   | Current IAM access token, region and endpoint            |
| `get_feature_guide` | read   | Step-by-step guidance for a composite vBackup capability |

> **IAM-gated** tools answer `403 IAM_PERMISSION_DENIED` for a caller whose policy does not grant them, while their sibling list tools work. A 403 there means "not allowed", never "does not exist" — each docstring names the list tool to fall back to.

### Prompts

Nine guided flows are available as MCP prompts (Vietnamese) — portable across any MCP client, and always available (no `--allow-write` needed). Each prompt is also served through the `get_feature_guide` **tool** (same text, one source of truth): prompts must be loaded by the user, while agents call the tool on their own.

| Prompt                          | Covers                                                                                        |
| ------------------------------- | --------------------------------------------------------------------------------------------- |
| `vbackup_getting_started`       | The object model, regions and backends, and how vBackup differs from vServer snapshots        |
| `vbackup_protect_server`        | The full chain from discovery to creating a backup server                                     |
| `vbackup_protect_database`      | The vDB chain: eligibility, choosing a location and policy, and the delete constraints        |
| `vbackup_manage_policy`         | Schedules, retention, and the platform limits to validate against                             |
| `vbackup_check_backups`         | Did last night's backup run, and why did it fail                                              |
| `vbackup_inspect_restore_point` | What a restore point actually holds — and why a restore must be started in the console        |
| `vbackup_manage_backup_server`  | Coverage statistics, immediate backups, moving a destination, downloading and deleting points |
| `vbackup_manage_destination`    | Creating, editing and deleting a backup location — and which settings become irreversible     |
| `vbackup_reduce_backup_cost`    | Finding backups that cost money for nothing                                                   |

### Known limits

* **A restore cannot be started through this API.** The gateway publishes `list_restore_history` and no endpoint to trigger a restore; restores are performed in the console.
* **`list_volume_usage` 404s on a deleted server.** The endpoint answers `404 "Not found volumeId <id>"` for the whole request when any requested volume no longer exists in vServer. `list_volume_usage` reports the ids it could not measure in `missing_volume_ids`; use the restore points to size a deleted server's backups.
* **Snapshot policies live in vServer**, not here. `list_snapshot_policies` (and every server / volume snapshot operation) is exposed by vServer MCP Server. Snapshots are block-level and different from backups.
