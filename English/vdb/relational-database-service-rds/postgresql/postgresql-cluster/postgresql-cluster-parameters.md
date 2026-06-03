# PostgreSQL Parameters for Cluster

This page lists the parameters that can be customized through a **DB Configuration Group** when using vDB PostgreSQL Cluster (1 Writer + N Readers).

{% hint style="info" %}
* These parameters apply to PostgreSQL versions **15, 16, 17**.
* **Restart Required** = Yes: Changing this parameter requires a **restart** of the cluster to take effect.
* **Restart Required** = No: Changes are applied immediately without a restart.
* All parameters in the list are modifiable.
{% endhint %}

***

### Connections

| Parameter | Default Value | Allowed Values | Type | Unit | Description | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `max_connections` | 100 | 14 - 65536 | integer | | Maximum number of concurrent connections to the database | **Yes** |

### Memory & Buffers

| Parameter | Default Value | Allowed Values | Type | Unit | Description | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `shared_buffers` | 16384 | 16 - 1073741823 | integer | 8kB | Memory used as a shared buffer between backend processes | **Yes** |
| `work_mem` | 4096 | 64 - 2147483647 | integer | kB | Memory for ORDER BY, JOIN, DISTINCT; uses disk when exceeded | No |
| `maintenance_work_mem` | 65536 | 1024 - 2147483647 | integer | kB | Memory for VACUUM, CREATE INDEX | No |
| `temp_buffers` | 1024 | 100 - 1073741823 | integer | 8kB | Buffer memory per session | No |
| `max_prepared_transactions` | 0 | 0 - 262143 | integer | | Number of transactions in prepared state | **Yes** |

### Autovacuum

| Parameter | Default Value | Allowed Values | Type | Unit | Description | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `autovacuum` | on | true / false | boolean | | Enable/disable Autovacuum | No |
| `autovacuum_naptime` | 60 | 1 - 2147483 | integer | s | Time between two vacuum runs on the same table | No |
| `autovacuum_vacuum_threshold` | 50 | 0 - 2147483647 | integer | | Row update/delete threshold to trigger VACUUM | No |
| `autovacuum_analyze_threshold` | 50 | 0 - 2147483647 | integer | | Row change threshold to trigger ANALYZE | No |

### Logging

| Parameter | Default Value | Allowed Values | Type | Unit | Description | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `log_min_duration_statement` | -1 | -1 - 2147483647 | integer | ms | Log queries that run longer than the specified duration. Value `-1` = disabled | No |

### Query Planning & Optimization

| Parameter | Default Value | Allowed Values | Type | Unit | Description | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `effective_cache_size` | 524288 | 1 - 2147483647 | integer | 8kB | Estimated disk cache for the planner to choose indexes | No |
| `random_page_cost` | 4 | 0 - 1.79769e+308 | float | | Cost of random page access | No |
| `seq_page_cost` | 1 | 0 - 1.79769e+308 | float | | Cost of sequential page access | No |
| `enable_seqscan` | on | true / false | boolean | | Enable/disable sequential scan | No |
| `enable_indexscan` | on | true / false | boolean | | Enable/disable index scan | No |
| `enable_hashjoin` | on | true / false | boolean | | Enable/disable hash join | No |

### Locale & Format

| Parameter | Default Value | Allowed Values | Type | Unit | Description | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `DateStyle` | ISO, MDY | See table below | string | | Date/time display format | No |

**Supported DateStyle values:**

| DateStyle | Input Example | Output Example |
| --- | --- | --- |
| ISO, DMY | `01-02-2026` → 1 Feb 2026 | `2026-02-01` |
| ISO, MDY | `01-02-2026` → 2 Jan 2026 | `2026-01-02` |
| ISO, YMD | `2026-02-01` → 1 Feb 2026 | `2026-02-01` |
| SQL, DMY | `01-02-2026` → 1 Feb 2026 | `01/02/2026` |
| SQL, MDY | `01-02-2026` → 2 Jan 2026 | `01/02/2026` |
| SQL, YMD | `2026-02-01` → 1 Feb 2026 | `2026-02-01` |
| Postgres, DMY | `01-02-2026` → 1 Feb 2026 | `Fri 01 Feb 00:00:00 2026` |
| Postgres, MDY | `01-02-2026` → 2 Jan 2026 | `Fri 02 Jan 00:00:00 2026` |
| Postgres, YMD | `2026-02-01` → 1 Feb 2026 | `Fri 01 Feb 00:00:00 2026` |
| German, DMY | `01.02.2026` → 1 Feb 2026 | `01.02.2026` |
| German, MDY | `01.02.2026` → 2 Jan 2026 | `02.01.2026` |
| German, YMD | `2026.02.01` → 1 Feb 2026 | `01.02.2026` |

### Asynchronous & Workers

| Parameter | Default Value | Allowed Values | Type | Unit | Description | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `max_worker_processes` | 32 | 0 - 65536 | integer | | Maximum number of background worker processes | **Yes** |

### Transactions & Locking

| Parameter | Default Value | Allowed Values | Type | Unit | Description | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `max_locks_per_transaction` | 64 | 10 - 2147483647 | integer | | Maximum number of locks per transaction | **Yes** |
