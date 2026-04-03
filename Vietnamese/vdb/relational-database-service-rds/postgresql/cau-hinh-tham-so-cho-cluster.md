# PostgreSQL Parameters cho Cluster

Trang này liệt kê các parameter có thể tùy chỉnh thông qua **DB Configuration Group** khi sử dụng vDB PostgreSQL Cluster (1 Writer + N Readers).

{% hint style="info" %}
* Các parameter này áp dụng cho PostgreSQL version **15, 16, 17**.
* **Restart Required** = Có: Thay đổi parameter này yêu cầu **restart** cluster để áp dụng.
* **Restart Required** = Không: Thay đổi được áp dụng ngay lập tức mà không cần restart.
* Tất cả parameter trong danh sách đều có thể chỉnh sửa (modifiable).
{% endhint %}

***

### Connections

| Parameter | Giá trị mặc định | Giá trị cho phép | Kiểu | Unit | Công dụng | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `max_connections` | 100 | 14 - 65536 | integer | | Số lượng tối đa các connection đồng thời truy cập đến database | **Có** |

### Memory & Buffers

| Parameter | Giá trị mặc định | Giá trị cho phép | Kiểu | Unit | Công dụng | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `shared_buffers` | 16384 | 16 - 1073741823 | integer | 8kB | Memory dùng làm buffer cho shared memory giữa các backend process | **Có** |
| `work_mem` | 4096 | 64 - 2147483647 | integer | kB | Memory cho ORDER BY, JOIN, DISTINCT; vượt ngưỡng sẽ dùng disk | Không |
| `maintenance_work_mem` | 65536 | 1024 - 2147483647 | integer | kB | Memory cho VACUUM, CREATE INDEX | Không |
| `temp_buffers` | 1024 | 100 - 1073741823 | integer | 8kB | Buffer memory cho mỗi session | Không |
| `max_prepared_transactions` | 0 | 0 - 262143 | integer | | Số transaction ở trạng thái prepared | **Có** |

### Autovacuum

| Parameter | Giá trị mặc định | Giá trị cho phép | Kiểu | Unit | Công dụng | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `autovacuum` | on | true / false | boolean | | Bật/tắt Autovacuum | Không |
| `autovacuum_naptime` | 60 | 1 - 2147483 | integer | s | Thời gian giữa 2 lần vacuum cùng table | Không |
| `autovacuum_vacuum_threshold` | 50 | 0 - 2147483647 | integer | | Ngưỡng row update/delete để VACUUM | Không |
| `autovacuum_analyze_threshold` | 50 | 0 - 2147483647 | integer | | Ngưỡng row change để ANALYZE | Không |

### Logging

| Parameter | Giá trị mặc định | Giá trị cho phép | Kiểu | Unit | Công dụng | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `log_min_duration_statement` | -1 | -1 - 2147483647 | integer | ms | Log query chạy lâu hơn thời gian chỉ định. Giá trị `-1` = tắt | Không |

### Query Planning & Optimization

| Parameter | Giá trị mặc định | Giá trị cho phép | Kiểu | Unit | Công dụng | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `effective_cache_size` | 524288 | 1 - 2147483647 | integer | 8kB | Ước tính disk cache để planner chọn index | Không |
| `random_page_cost` | 4 | 0 - 1.79769e+308 | float | | Cost truy cập page random | Không |
| `seq_page_cost` | 1 | 0 - 1.79769e+308 | float | | Cost truy cập page sequential | Không |
| `enable_seqscan` | on | true / false | boolean | | Bật/tắt seq scan | Không |
| `enable_indexscan` | on | true / false | boolean | | Bật/tắt index scan | Không |
| `enable_hashjoin` | on | true / false | boolean | | Bật/tắt hash join | Không |

### Locale & Format

| Parameter | Giá trị mặc định | Giá trị cho phép | Kiểu | Unit | Công dụng | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `DateStyle` | ISO, MDY | Xem bảng bên dưới | string | | Format hiển thị ngày giờ | Không |

**Các giá trị DateStyle được hỗ trợ:**

| DateStyle | Input ví dụ | Output ví dụ |
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

| Parameter | Giá trị mặc định | Giá trị cho phép | Kiểu | Unit | Công dụng | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `max_worker_processes` | 32 | 0 - 65536 | integer | | Số tiến trình background tối đa | **Có** |

### Transactions & Locking

| Parameter | Giá trị mặc định | Giá trị cho phép | Kiểu | Unit | Công dụng | Restart Required |
| --- | --- | --- | --- | --- | --- | --- |
| `max_locks_per_transaction` | 64 | 10 - 2147483647 | integer | | Số lock tối đa mỗi transaction | **Có** |
