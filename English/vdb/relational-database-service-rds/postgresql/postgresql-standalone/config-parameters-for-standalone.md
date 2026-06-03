# PostgreSQL Parameters for Standalone

This page lists the parameters that can be customized through a **DB Configuration Group** when using vDB PostgreSQL Standalone (Single Node).

{% hint style="info" %}
* **Restart Required** = Yes: Changing this parameter requires a **restart** of the database instance to take effect.
* **Restart Required** = No: Changes are applied immediately without a restart.
* All parameters listed are modifiable.
{% endhint %}

***

## Parameter List by Version

The parameter list for PostgreSQL versions **13, 14, and 15** is **identical**. Versions **10** and **12** support additional parameters (see [the section below](#additional-parameters-for-postgresql-10-and-12)).

***

### Checkpoints & WAL

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `checkpoint_timeout` | 30 - 3600 | integer | No |
| `checkpoint_warning` | 0 - 2147483647 | integer | No |
| `commit_delay` | 0 - 100000 | integer | No |
| `commit_siblings` | 0 - 1000 | integer | No |
| `wal_buffers` | -1 - 262143 | integer | **Yes** |
| `wal_keep_size` | 0 - 2147483647 | integer | No |
| `wal_receiver_timeout` | 0 - 3600000 | integer | No |
| `wal_sender_timeout` | 0 - 3600000 | integer | No |

### Connections & Authentication

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `idle_in_transaction_session_timeout` | 0 - 2147483647 | integer | No |
| `max_connections` | 11 - 65536 | integer | **Yes** |
| `tcp_keepalives_count` | 0 - 2147483647 | integer | No |
| `tcp_keepalives_idle` | 0 - 2147483647 | integer | No |
| `tcp_keepalives_interval` | 0 - 2147483647 | integer | No |

### Memory & Buffers

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `effective_cache_size` | 1 - 2147483647 | integer | No |
| `shared_buffers` | 16 - 1073741823 | integer | **Yes** |
| `temp_buffers` | 100 - 1073741823 | integer | No |
| `work_mem` | 64 - 10485760 | integer | No |

### Query Planning & Optimization

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `constraint_exclusion` | partition, on, off | string | No |
| `default_statistics_target` | 1 - 10000 | integer | No |
| `force_parallel_mode` | true / false | boolean | No |
| `from_collapse_limit` | 1 - 2147483647 | integer | No |
| `geqo` | true / false | boolean | No |
| `geqo_effort` | 1 - 10 | integer | No |
| `geqo_generations` | 0 - 1000 | integer | No |
| `geqo_pool_size` | 0 - 1000 | integer | No |
| `geqo_threshold` | 2 - 2147483647 | integer | No |
| `join_collapse_limit` | 1 - 2147483647 | integer | No |
| `replacement_sort_tuples` | 0 - 2147483647 | integer | No |

### Replication & Standby

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `hot_standby_feedback` | true / false | boolean | No |
| `synchronize_seqscans` | true / false | boolean | No |

### Transactions & Locking

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `deadlock_timeout` | 1 - 2147483647 | integer | No |
| `default_transaction_deferrable` | true / false | boolean | No |
| `default_transaction_isolation` | serializable, repeatable read, read committed, read uncommitted | string | No |
| `lock_timeout` | 1 - 2147483647 | integer | No |
| `max_locks_per_transaction` | 10 - 1000 | integer | **Yes** |
| `max_pred_locks_per_transaction` | 10 - 1000 | integer | **Yes** |
| `max_prepared_transactions` | 0 - 65536 | integer | **Yes** |
| `max_worker_processes` | 0 - 65536 | integer | **Yes** |

### Miscellaneous

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `gin_pending_list_limit` | 64 - 2147483647 | integer | No |
| `standard_conforming_strings` | true / false | boolean | No |

***

## Additional Parameters for PostgreSQL 10 and 12

The parameters below are **only available on PostgreSQL 10 and/or 12** and are not supported on PostgreSQL 13+.

### Connections & Authentication (PG 10, 12)

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `authentication_timeout` | 1 - 600 | integer | No |
| `max_files_per_process` | 50 - 2000 | integer | **Yes** |
| `statement_timeout` | 0 - 2147483647 | integer | No |
| `superuser_reserved_connections` | 0 - 8388607 | integer | **Yes** |

### Memory & I/O (PG 10, 12)

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `backend_flush_after` | 0 - 256 | integer | No |
| `bgwriter_delay` | 10 - 10000 | integer | No |
| `bgwriter_flush_after` | 0 - 256 | integer | No |
| `bgwriter_lru_maxpages` | 0 - 1000 | integer | No |
| `checkpoint_flush_after` | 0 - 256 | integer | No |
| `effective_io_concurrency` | 0 - 1000 | integer | No |

### Encoding & Format (PG 10, 12)

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `backslash_quote` | safe_encoding, on, off | string | No |
| `bytea_output` | escape, hex | string | No |
| `client_encoding` | UTF8, LATIN1, ... (multiple values) | string | No |
| `datestyle` | ISO, Postgres, SQL, German | string | No |
| `intervalstyle` | postgres, postgres_verbose, sql_standard, iso_8601 | string | No |
| `xmlbinary` | base64, hex | string | No |
| `xmloption` | content, document | string | No |

### WAL & Replication (PG 10, 12)

| Parameter | Allowed Values | Type | Restart Required | Notes |
| --- | --- | --- | --- | --- |
| `session_replication_role` | origin, replica, local | string | No | |
| `synchronous_commit` | local, on, off | string | No | |
| `wal_keep_segments` | 0 - 2147483647 | integer | No | PG 10 only; replaced by `wal_keep_size` from PG 12 |
| `wal_receiver_status_interval` | 0 - 2147483 | integer | No | |
| `wal_writer_delay` | 1 - 10000 | integer | No | |

### Boolean Flags (PG 10, 12)

| Parameter | Description | Restart Required |
| --- | --- | --- |
| `array_nulls` | Allow NULL values in arrays | No |
| `check_function_bodies` | Validate function bodies at CREATE FUNCTION | No |
| `default_transaction_read_only` | Default transactions to read-only | No |
| `default_with_oids` | Use OIDs by default for new tables | No |
| `escape_string_warning` | Warn on escape sequences in strings | No |
| `exit_on_error` | Exit session on any error | No |
| `fsync` | Force synchronization of data to disk | No |
| `full_page_writes` | Write full pages during checkpoint | No |
| `lo_compat_privileges` | Enable large object privilege compatibility | No |
| `quote_all_identifiers` | Quote all identifiers | No |
| `transform_null_equals` | Treat expr = NULL as expr IS NULL | No |

### Miscellaneous (PG 10, 12)

| Parameter | Allowed Values | Type | Restart Required |
| --- | --- | --- | --- |
| `extra_float_digits` | -15 - 3 | integer | No |
