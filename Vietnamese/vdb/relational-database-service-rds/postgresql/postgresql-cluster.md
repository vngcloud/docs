# PostgreSQL Cluster

## Tổng quan

**PostgreSQL Cluster** là tính năng cho phép triển khai PostgreSQL với kiến trúc **1 Writer (Primary) + N Readers (Replica)**, đảm bảo **High Availability** và khả năng **scale read** cho các workload production trên vDB.

### PostgreSQL Cluster là gì?

Trong mô hình PostgreSQL Cluster, các node được phân vai trò rõ ràng:

* **Writer (Primary)**: Node xử lý tất cả các thao tác ghi (INSERT, UPDATE, DELETE). Mỗi cluster luôn có đúng **1 Writer**.
* **Reader (Replica)**: Node chỉ đọc, đồng bộ dữ liệu từ Writer thông qua **Streaming Replication**. Cluster có thể có từ **1 đến 9 Readers**.
* **Automatic Failover**: Khi Writer gặp sự cố, một Reader sẽ được **tự động promote** thành Writer mà không cần can thiệp thủ công.

Để khởi tạo và quản lý PostgreSQL Cluster, vui lòng tham khảo hướng dẫn tại [đây](khoi-tao-va-quan-ly-postgresql-cluster.md).

### So sánh Single Node và Cluster

| Đặc điểm              | Single Node                        | Cluster                                                   |
| --------------------- | ---------------------------------- | --------------------------------------------------------- |
| **Kiến trúc**         | 1 node duy nhất                    | 1 Writer + N Readers                                      |
| **High Availability** | Không                              | Có (Automatic Failover)                                   |
| **Scale Read**        | Không                              | Có (Read traffic phân bổ đến Readers)                     |
| **Backup**            | Automatic daily backup (cơ chế cũ) | Tích hợp Backup Center (Auto Backup + Manual Backup)      |
| **Số lượng node**     | 1                                  | 2 - 10                                                    |
| **Use Case**          | Development, Testing, ứng dụng nhỏ | Production, Mission-critical, ứng dụng yêu cầu uptime cao |

### Khi nào nên sử dụng PostgreSQL Cluster?

* **Production workloads**: Các ứng dụng yêu cầu uptime cao và không chấp nhận downtime.
* **Read-heavy applications**: Ứng dụng có lượng truy vấn đọc lớn, cần scale out read operations.
* **Mission-critical systems**: Hệ thống thanh toán, giao dịch, dữ liệu quan trọng cần được bảo vệ bởi automatic failover.
* **Data protection**: Các ứng dụng yêu cầu chiến lược backup toàn diện với Auto Backup và Manual Backup thông qua Backup Center.

{% hint style="info" %}
**Lưu ý:**

* **Single Node** phù hợp cho môi trường **development** và **testing** do cấu hình đơn giản và chi phí thấp hơn.
* **Cluster** được khuyến nghị cho môi trường **production** khi cần High Availability và khả năng chịu lỗi.
{% endhint %}

***

## Kiến trúc PostgreSQL Cluster

<figure><img src="../../../.gitbook/assets/vDB Postgres Cluster Architecture Diagram.png" alt=""><figcaption></figcaption></figure>

**Các thành phần chính:**

* **Writer Node (Primary)**: Xử lý tất cả write operations. Mỗi cluster chỉ có duy nhất 1 Writer.
* **Reader Node(s) (Replica)**: Xử lý read operations, đồng bộ dữ liệu từ Writer qua Streaming Replication. Cung cấp khả năng failover khi Writer gặp sự cố.
* **Automatic Failover**: Khi Writer node không khả dụng, hệ thống tự động promote một Reader lên làm Writer, đảm bảo dịch vụ không bị gián đoạn.

**Phân bổ vai trò theo số lượng node:**

| Số lượng Node | Phân bổ vai trò      |
| ------------- | -------------------- |
| 2             | 1 Writer + 1 Reader  |
| 3             | 1 Writer + 2 Readers |
| 5             | 1 Writer + 4 Readers |
| 10            | 1 Writer + 9 Readers |

***

## Tích hợp Backup Center

PostgreSQL Cluster được tích hợp với **Backup Center (vBackup)**, cung cấp giải pháp backup & restore toàn diện:

* **Auto Backup**: Được cấu hình bắt buộc khi tạo cluster. Backup chạy tự động theo lịch của Backup Policy đã chọn.
* **Manual Backup**: Cho phép tạo **Full Snapshot** thủ công bất kỳ lúc nào từ trang chi tiết cluster.
* **Restore**: Tạo cluster mới từ một restore point có sẵn trong Backup Center. Storage Size của cluster mới phải lớn hơn hoặc bằng Backup Size.

{% hint style="warning" %}
**Lưu ý về Backup khi xóa Cluster:**

* **Auto Backup**: Sẽ được **tự động xóa** khi cluster bị xóa.
* **Manual Backup**: Sẽ được **giữ lại** sau khi xóa cluster. Bạn cần tự quản lý và xóa thủ công tại Backup Center nếu không còn cần thiết.
{% endhint %}

***

## Giới hạn và Lưu ý

### Giới hạn hiện tại

| Giới hạn             | Mô tả                                                                   |
| -------------------- | ----------------------------------------------------------------------- |
| **Số lượng node**    | Tối thiểu 2, tối đa 10 node mỗi cluster                                 |
| **Writer node**      | Luôn có đúng 1 Writer trong mỗi cluster                                 |
| **Database Proxy**   | Chưa hỗ trợ trong phiên bản hiện tại (Coming Soon - Phase 2)            |
| **Backup đồng thời** | Chỉ cho phép 1 job backup/restore chạy tại 1 thời điểm trên mỗi cluster |

### Lưu ý quan trọng

{% hint style="info" %}
**Về Reserved Usernames:**

Khi tạo cluster, bạn **không được** sử dụng các username sau làm Master Username vì chúng đã được hệ thống sử dụng: `postgres`, `admin`, `cron_admin`, `robot_zmon`, `vngpooler`, `vngpam`, `vngrep`, `vngsuperrole`.
{% endhint %}

{% hint style="info" %}
**Về Deployment Type:**

Tính năng PostgreSQL Cluster chỉ khả dụng khi chọn Engine là **PostgreSQL**. Các engine khác (MySQL, MariaDB) hiện chỉ hỗ trợ deployment type **Single Node**.
{% endhint %}

***

## FAQ

### 1. Tôi có thể chuyển từ Single Node sang Cluster không?

**Không.** Hiện tại vDB không hỗ trợ chuyển đổi Deployment Type sau khi database đã được tạo. Bạn cần tạo mới một cluster và migrate dữ liệu.

### 2. Điều gì xảy ra khi Writer node gặp sự cố?

Khi Writer node gặp sự cố, hệ thống sẽ **tự động failover**: một Reader node sẽ được promote thành Writer mới. Quá trình này diễn ra tự động, không cần can thiệp thủ công. UI sẽ cập nhật vai trò (role) của các node sau khi failover hoàn tất.

### 3. Tôi có thể tạo cluster từ bản backup có sẵn không?

**Có.** Khi tạo cluster mới, bạn có thể chọn một restore point từ Backup Center để khôi phục dữ liệu. Lưu ý rằng Storage Size của cluster mới phải lớn hơn hoặc bằng Backup Size của bản backup.

### 4. Database Proxy là gì và khi nào sẽ có?

Database Proxy cung cấp connection pooling và load balancing cho cluster. Tính năng này đang được phát triển và sẽ ra mắt trong **Phase 2**. Vui lòng theo dõi trang [Thông báo và Cập nhật](../../announcements/release-notes.md) để nắm thông tin mới nhất.
