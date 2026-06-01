# PostgreSQL Parameters cho Standalone

Trang này liệt kê các parameter có thể tùy chỉnh thông qua **DB Configuration Group** khi sử dụng vDB PostgreSQL Standalone (Single Node).

{% hint style="info" %}
* **Restart Required** = Có: Thay đổi parameter này yêu cầu **restart** database instance để áp dụng.
* **Restart Required** = Không: Thay đổi được áp dụng ngay lập tức mà không cần restart.
* Tất cả parameter trong danh sách đều có thể chỉnh sửa (modifiable).
{% endhint %}

***

## Danh sách Parameter theo Version

Danh sách parameter cho các phiên bản PostgreSQL **13, 14, 15** là **giống nhau hoàn toàn**. Phiên bản **10** và **12** có thêm một số parameter bổ sung (xem [mục cuối](#cac-parameter-bo-sung-cho-postgresql-10-va-12)).

***

### Checkpoints & WAL

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `checkpoint_timeout` | 30 - 3600 | integer | Không |
| `checkpoint_warning` | 0 - 2147483647 | integer | Không |
| `commit_delay` | 0 - 100000 | integer | Không |
| `commit_siblings` | 0 - 1000 | integer | Không |
| `wal_buffers` | -1 - 262143 | integer | **Có** |
| `wal_keep_size` | 0 - 2147483647 | integer | Không |
| `wal_receiver_timeout` | 0 - 3600000 | integer | Không |
| `wal_sender_timeout` | 0 - 3600000 | integer | Không |

### Connections & Authentication

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `idle_in_transaction_session_timeout` | 0 - 2147483647 | integer | Không |
| `max_connections` | 11 - 65536 | integer | **Có** |
| `tcp_keepalives_count` | 0 - 2147483647 | integer | Không |
| `tcp_keepalives_idle` | 0 - 2147483647 | integer | Không |
| `tcp_keepalives_interval` | 0 - 2147483647 | integer | Không |

### Memory & Buffers

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `effective_cache_size` | 1 - 2147483647 | integer | Không |
| `shared_buffers` | 16 - 1073741823 | integer | **Có** |
| `temp_buffers` | 100 - 1073741823 | integer | Không |
| `work_mem` | 64 - 10485760 | integer | Không |

### Query Planning & Optimization

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `constraint_exclusion` | partition, on, off | string | Không |
| `default_statistics_target` | 1 - 10000 | integer | Không |
| `force_parallel_mode` | true / false | boolean | Không |
| `from_collapse_limit` | 1 - 2147483647 | integer | Không |
| `geqo` | true / false | boolean | Không |
| `geqo_effort` | 1 - 10 | integer | Không |
| `geqo_generations` | 0 - 1000 | integer | Không |
| `geqo_pool_size` | 0 - 1000 | integer | Không |
| `geqo_threshold` | 2 - 2147483647 | integer | Không |
| `join_collapse_limit` | 1 - 2147483647 | integer | Không |
| `replacement_sort_tuples` | 0 - 2147483647 | integer | Không |

### Replication & Standby

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `hot_standby_feedback` | true / false | boolean | Không |
| `synchronize_seqscans` | true / false | boolean | Không |

### Transactions & Locking

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `deadlock_timeout` | 1 - 2147483647 | integer | Không |
| `default_transaction_deferrable` | true / false | boolean | Không |
| `default_transaction_isolation` | serializable, repeatable read, read committed, read uncommitted | string | Không |
| `lock_timeout` | 1 - 2147483647 | integer | Không |
| `max_locks_per_transaction` | 10 - 1000 | integer | **Có** |
| `max_pred_locks_per_transaction` | 10 - 1000 | integer | **Có** |
| `max_prepared_transactions` | 0 - 65536 | integer | **Có** |
| `max_worker_processes` | 0 - 65536 | integer | **Có** |

### Miscellaneous

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `gin_pending_list_limit` | 64 - 2147483647 | integer | Không |
| `standard_conforming_strings` | true / false | boolean | Không |

***

## Các Parameter bổ sung cho PostgreSQL 10 và 12

Các parameter dưới đây **chỉ có trên PostgreSQL 10 và/hoặc 12**, không còn hỗ trợ trên PostgreSQL 13+.

### Connections & Authentication (PG 10, 12)

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `authentication_timeout` | 1 - 600 | integer | Không |
| `max_files_per_process` | 50 - 2000 | integer | **Có** |
| `statement_timeout` | 0 - 2147483647 | integer | Không |
| `superuser_reserved_connections` | 0 - 8388607 | integer | **Có** |

### Memory & I/O (PG 10, 12)

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `backend_flush_after` | 0 - 256 | integer | Không |
| `bgwriter_delay` | 10 - 10000 | integer | Không |
| `bgwriter_flush_after` | 0 - 256 | integer | Không |
| `bgwriter_lru_maxpages` | 0 - 1000 | integer | Không |
| `checkpoint_flush_after` | 0 - 256 | integer | Không |
| `effective_io_concurrency` | 0 - 1000 | integer | Không |

### Encoding & Format (PG 10, 12)

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `backslash_quote` | safe_encoding, on, off | string | Không |
| `bytea_output` | escape, hex | string | Không |
| `client_encoding` | UTF8, LATIN1, ... (nhiều giá trị) | string | Không |
| `datestyle` | ISO, Postgres, SQL, German | string | Không |
| `intervalstyle` | postgres, postgres_verbose, sql_standard, iso_8601 | string | Không |
| `xmlbinary` | base64, hex | string | Không |
| `xmloption` | content, document | string | Không |

### WAL & Replication (PG 10, 12)

| Parameter | Giá trị cho phép | Kiểu | Restart Required | Ghi chú |
| --- | --- | --- | --- | --- |
| `session_replication_role` | origin, replica, local | string | Không | |
| `synchronous_commit` | local, on, off | string | Không | |
| `wal_keep_segments` | 0 - 2147483647 | integer | Không | Chỉ PG 10, đổi thành `wal_keep_size` từ PG 12 |
| `wal_receiver_status_interval` | 0 - 2147483 | integer | Không | |
| `wal_writer_delay` | 1 - 10000 | integer | Không | |

### Boolean Flags (PG 10, 12)

| Parameter | Mô tả | Restart Required |
| --- | --- | --- |
| `array_nulls` | Cho phép giá trị NULL trong array | Không |
| `check_function_bodies` | Kiểm tra body hàm khi CREATE FUNCTION | Không |
| `default_transaction_read_only` | Mặc định transaction read-only | Không |
| `default_with_oids` | Dùng OIDs mặc định cho bảng mới | Không |
| `escape_string_warning` | Cảnh báo escape trong string | Không |
| `exit_on_error` | Thoát session khi có lỗi | Không |
| `fsync` | Buộc đồng bộ dữ liệu xuống disk | Không |
| `full_page_writes` | Ghi toàn bộ page khi checkpoint | Không |
| `lo_compat_privileges` | Tương thích quyền Large Object | Không |
| `quote_all_identifiers` | Quote tất cả identifiers | Không |
| `transform_null_equals` | Biến đổi expr = NULL thành expr IS NULL | Không |

### Miscellaneous (PG 10, 12)

| Parameter | Giá trị cho phép | Kiểu | Restart Required |
| --- | --- | --- | --- |
| `extra_float_digits` | -15 - 3 | integer | Không |
