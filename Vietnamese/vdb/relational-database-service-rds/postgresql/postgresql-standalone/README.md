# PostgreSQL Standalone

## Tổng quan

**PostgreSQL Standalone** (Single Node) là mô hình triển khai PostgreSQL trên vDB với **1 node duy nhất**, phù hợp cho môi trường development, testing hoặc các ứng dụng nhỏ không yêu cầu High Availability.

### PostgreSQL Standalone là gì?

Trong mô hình Standalone, toàn bộ hoạt động của database — bao gồm cả đọc lẫn ghi — đều được xử lý bởi **1 node duy nhất**:

* **Single Node**: Xử lý tất cả các thao tác đọc và ghi (SELECT, INSERT, UPDATE, DELETE) trên cùng một instance.
* **Đơn giản, dễ triển khai**: Không cần cấu hình replication hay failover.
* **Chi phí thấp hơn**: Phù hợp cho các workload không yêu cầu tính sẵn sàng cao.

### So sánh Single Node và Cluster

| Đặc điểm              | Single Node                        | Cluster                                                    |
| --------------------- | ---------------------------------- | ---------------------------------------------------------- |
| **Kiến trúc**         | 1 node duy nhất                    | 1 Writer + N Readers                                       |
| **High Availability** | Không                              | Có (Automatic Failover)                                    |
| **Scale Read**        | Không                              | Có (Read traffic phân bổ đến Readers)                      |
| **Backup**            | Automatic daily backup (cơ chế cũ) | Tích hợp Backup Center (Auto Backup + Manual Backup)       |
| **Số lượng node**     | 1                                  | 2 - 10                                                     |
| **Use Case**          | Development, Testing, ứng dụng nhỏ | Production, Mission-critical, ứng dụng yêu cầu uptime cao  |

### Khi nào nên sử dụng PostgreSQL Standalone?

* **Development & Testing**: Môi trường phát triển và kiểm thử không yêu cầu uptime cao.
* **Ứng dụng nhỏ**: Các ứng dụng có lưu lượng thấp, không cần scale read.
* **Chi phí tối ưu**: Khi High Availability không phải ưu tiên hàng đầu.

{% hint style="info" %}
**Lưu ý:**

* **Single Node** phù hợp cho môi trường **development** và **testing** do cấu hình đơn giản và chi phí thấp hơn.
* **Cluster** được khuyến nghị cho môi trường **production** khi cần High Availability và khả năng chịu lỗi.
{% endhint %}

***

## Giới hạn và Lưu ý

{% hint style="info" %}
**Về Reserved Usernames:**

Khi tạo instance, bạn **không được** sử dụng các username sau làm Master Username vì chúng đã được hệ thống sử dụng: `postgres`, `admin`, `cron_admin`, `robot_zmon`, `vngpooler`, `vngpam`, `vngrep`, `vngsuperrole`.
{% endhint %}

{% hint style="info" %}
**Về Deployment Type:**

PostgreSQL Standalone sử dụng Deployment Type là **Single Node**. Nếu bạn cần High Availability và khả năng scale read, hãy cân nhắc sử dụng [PostgreSQL Cluster](../postgresql-cluster/README.md).
{% endhint %}

{% hint style="warning" %}
**Không hỗ trợ chuyển đổi Deployment Type:**

Hiện tại vDB không hỗ trợ chuyển đổi từ Standalone sang Cluster sau khi instance đã được tạo. Để migrate, bạn cần tạo mới một PostgreSQL Cluster và [migrate dữ liệu](../postgresql-cluster/migrate-tu-postgresql-single-sang-cluster.md).
{% endhint %}
