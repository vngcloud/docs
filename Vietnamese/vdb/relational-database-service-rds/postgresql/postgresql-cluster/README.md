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
| **Availability & Durability** | Single-AZ                          | Single-AZ hoặc Multi-AZ                                   |
| **Use Case**          | Development, Testing, ứng dụng nhỏ | Production, Mission-critical, ứng dụng yêu cầu uptime cao |

### Khi nào nên sử dụng PostgreSQL Cluster?

* **Production workloads**: Các ứng dụng yêu cầu uptime cao và không chấp nhận downtime.
* **Read-heavy applications**: Ứng dụng có lượng truy vấn đọc lớn, cần scale out read operations.
* **Mission-critical systems**: Hệ thống thanh toán, giao dịch, dữ liệu quan trọng cần được bảo vệ bởi automatic failover.
* **Data protection**: Các ứng dụng yêu cầu chiến lược backup toàn diện với Auto Backup và Manual Backup thông qua Backup CenteCenter.

{% hint style="info" %}
**Lưu ý:**

* **Single Node** phù hợp cho môi trường **development** và **testing** do cấu hình đơn giản và chi phí thấp hơn.
* **Cluster** được khuyến nghị cho môi trường **production** khi cần High Availability và khả năng chịu lỗi.
{% endhint %}

***

## Kiến trúc PostgreSQL Cluster

**Các thành phần chính:**

* **Writer Node (Primary)**: Xử lý tất cả write operations. Mỗi cluster chỉ có duy nhất 1 Writer.
* **Reader Node(s) (Replica)**: Xử lý read operations, đồng bộ dữ liệu từ Writer qua Streaming Replication. Cung cấp khả năng failover khi Writer gặp sự cố.
* **Automatic Failover**: Khi Writer node không khả dụng, hệ thống tự động promote một Reader lên làm Writer, đảm bảo dịch vụ không bị gián đoạn.

**Phân bổ vai trò theo số lượng node:**

<table><thead><tr><th width="222">Số lượng Node</th><th>Phân bổ vai trò</th></tr></thead><tbody><tr><td>2</td><td>1 Writer + 1 Reader</td></tr><tr><td>3</td><td>1 Writer + 2 Readers</td></tr><tr><td>5</td><td>1 Writer + 4 Readers</td></tr><tr><td>10</td><td>1 Writer + 9 Readers</td></tr></tbody></table>

***

## Chế độ Availability & Durability

PostgreSQL Cluster có hai chế độ triển khai, chọn tại trường **Availability & Durability** ở bước Basic configuration:

* **Single-AZ**: toàn bộ Node nằm trong một Availability Zone. Phù hợp khi bạn cần High Availability ở mức Node và muốn cấu hình đơn giản nhất.
* **Multi-AZ**: Node được trải trên từ hai Availability Zone trở lên. Cluster vẫn phục vụ được khi một Availability Zone gặp sự cố.

Multi-AZ hiện chỉ khả dụng tại region HCM và yêu cầu VPC đã bật DNS. Hướng dẫn chi tiết tại [Khởi tạo PostgreSQL Cluster Multi-AZ](khoi-tao-postgresql-cluster-multi-az.md).

***
## Tích hợp Backup Center

PostgreSQL Cluster được tích hợp với **Backup Center (vBackup)**, cung cấp giải pháp backup & restore toàn diện:

* **Auto Backup**: Được cấu hình bắt buộc khi tạo cluster. Backup chạy tự động theo lịch của Backup Policy đã chọn.
* **Manual Backup**: Cho phép tạo **Full Snapshot** thủ công bất kỳ lúc nào từ trang chi tiết cluster.
* **Restore**: Tạo cluster mới từ một restore point có sẵn trong Backup Center. Cluster mới cần dung lượng lớn hơn dung lượng của bản backup; hệ thống hiển thị mức tối thiểu ngay tại trường **Storage size** sau khi bạn chọn bản backup.

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
| **Số Availability Zone** | Cluster Multi-AZ yêu cầu tối thiểu 2 zone, mỗi zone một Subnet          |
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

**Có.** Khi tạo cluster mới, bạn có thể chọn một restore point từ Backup Center để khôi phục dữ liệu. Cluster mới cần dung lượng lớn hơn dung lượng của bản backup; hệ thống hiển thị mức tối thiểu ngay tại trường **Storage size** sau khi bạn chọn bản backup.

### 4. Database Proxy là gì và khi nào sẽ có?

Database Proxy cung cấp connection pooling và load balancing cho cluster. Tính năng này đang được phát triển và sẽ ra mắt trong **Phase 2**. Vui lòng theo dõi trang [Thông báo và Cập nhật](../../../announcements/release-notes.md) để nắm thông tin mới nhất.

### 5. Multi-AZ khác Single-AZ ở đâu?

**Single-AZ** đặt toàn bộ Node trong một Availability Zone; **Multi-AZ** trải Node trên từ hai Availability Zone trở lên, nên cluster vẫn chạy khi một Availability Zone gặp sự cố. Multi-AZ hiện chỉ có ở region HCM, yêu cầu VPC đã bật DNS và tối thiểu 2 zone. Xem [Khởi tạo PostgreSQL Cluster Multi-AZ](khoi-tao-postgresql-cluster-multi-az.md).
