# vDB

GreenNode Database as a Service (vDB) là dịch vụ cho phép dễ dàng thiết lập, vận hành và mở rộng cơ sở dữ liệu doanh nghiệp trên nền tảng điện toán đám mây của GreenNode. vDB cung cấp khả năng tự động hóa các tác vụ như là khởi tạo phần cứng, cài đặt cơ sở dữ liệu, sao lưu và phục hồi với mức chi phí hiệu quả. Khi sử dụng vDB, khách hàng có thể hoàn toàn tập trung vào việc xây dựng và chạy ứng dụng của mình.

vDB gồm nhiều loại dịch vụ cho từng loại cơ sở dữ liệu , hiện nay chúng tôi đang cung cấp:

* [Relational Databases Service (RDS)](relational-database-service-rds/): bao gồm các cơ sở dữ liệu quan hệ quen thuộc như MySQL, Mariadb, Postgresql.
* [MemoryStore Database Service (MDS)](memorystore-database-service-mds/): bao gồm các hệ lưu trữ dữ liệu trên bộ nhớ (in-memory) như Redis, Memcached.

### Lợi ích <a href="#vdb-database-loiich" id="vdb-database-loiich"></a>

**Quản trị dễ dàng, đơn giản**

* vDB giúp bạn triển khai và quản lý cơ sở dữ liệu trên đám mây một cách dễ dàng, bạn có thể sử dụng giao diện trực quan hoặc giao diện lập trình ứng dụng (API) để quản lý cơ sở dữ liệu trong vài phút. Bạn không cần phải khởi tạo hạ tầng và cũng không cần phải cài đặt hay cấu hình những bước phức tạp.

**Khả năng mở rộng linh hoạt**

* Bạn có thể mở rộng tài nguyên tính toán (CPU, Memory) và tài nguyên lưu trữ của cơ sở dữ liệu với chỉ vài thao tác đơn giản trên giao diện hoặc gọi vào giao diện lập trình ứng dụng (API), giúp đáp ứng được nhu cầu mở rộng nhanh chóng.

**Sao lưu và khôi phục dữ liệu dễ dàng**

* vDB cung cấp khả năng tự động sao lưu dữ liệu hàng ngày giúp đảm bảo khả năng khôi phục dữ liệu theo bản sao lưu khi xảy ra sự cố, đồng thời cho phép tạo bản sao lưu theo nhu cầu của bạn

**Hiệu năng cao**

* Phần cứng chuyên dụng dành cho doanh nghiệp kết hợp với hệ thống lưu trữ SSD mang lại cho bạn hiệu năng cao mà bạn cần.

**Kết nối dễ dàng**

* Bạn chỉ cần vào xem chi tiết một vDB bất kỳ, bạn chọn tab Connectivity & Security xem thông tin endpoint và port để thực hiện kết nối.

**An toàn**

* vDB giúp bạn dễ dàng kiểm soát truy cập mạng vào cơ sở dữ liệu của bạn, đồng thời cho phép bạn chạy hệ thống cơ sở dữ liệu trong mạng riêng ảo (vVPC), mà cung cấp nhiều tính năng bảo mật khác.

**Chỉ trả cho những gì bạn sử dụng**

* vDB có thể giúp bạn tối ưu hoá việc sử dụng tài nguyên và hiệu quả chi phí, bạn có thể mở rộng tài nguyên khi cần và thu hẹp hệ thống khi không cần, bạn chỉ trả tiền cho những gì bạn đang sử dụng.



### Các engine được hỗ trợ:

#### Single Mode:

| Engine                   | MySQL             | MariaDB           | PostgreSQL        | Redis              |
| ------------------------ | ----------------- | ----------------- | ----------------- | ------------------ |
| Version                  | 5.7, 8.0          | 10.3, 10.4, 10.5  | 12, 13, 14, 15    | 4.0, 5.0, 6.2, 7.2 |
| Supported AZ             | HCM 1a, 1b, 1c    | HCM 1a, 1b, 1c    | HCM 1a, 1b, 1c    | HCM 1a, 1b, 1c     |
| Multi-AZ Replication     | yes               | yes               | yes               | yes                |
| Scale Up Flavor          | yes               | yes               | yes               | yes                |
| Scale Up Storage         | yes               | yes               | yes               | n/a                |
| Scale out (read-replica) | up to 5           | up to 5           | up to 5           | up to 5            |
| Scale out (writer)       | n/a               | n/a               | n/a               | n/a                |
| Configuration Group      | yes               | yes               | yes               | yes                |
| Monitoring               | metric            | metric            | metric            | metric             |
| Backup Method            | Full, Incremental | Full, Incremental | Full, Incremental | Full, Incremental  |
| Auto Backup              | Daily             | Daily             | Daily             | Daily              |
| Integrate vBackup        | no                | no                | no                | no                 |
| Backup Location          | HCM               | HCM               | HCM               | HCM                |

#### Cluster Mode:

<table><thead><tr><th>Engine</th><th>Kafka</th><th>OpenSearch</th><th>PostgreSQL</th><th data-hidden>Redis</th></tr></thead><tbody><tr><td>Version</td><td>3.6.0, 3.6.1, 3.7.0</td><td>2.15, 2.17</td><td>15, 16, 17</td><td>7.0, 7.1, 7.2</td></tr><tr><td>Supported AZ</td><td>HCM 1a</td><td>HCM 1a, 1b, 1c</td><td>HCM 1a, 1b, 1c</td><td>HCM 1a, 1b, 1c</td></tr><tr><td>Multi-AZ Replication</td><td>no</td><td>no</td><td>coming soon</td><td>coming soon</td></tr><tr><td>Scale Up Flavor</td><td>yes</td><td>yes</td><td>coming soon</td><td>coming soon</td></tr><tr><td>Scale Up Storage</td><td>yes</td><td>yes</td><td>yes</td><td>n/a</td></tr><tr><td>Scale out (read-replica)</td><td>no</td><td>no</td><td>up to 9</td><td>up to 9</td></tr><tr><td>Scale out (writer)</td><td>up to 10</td><td>up to 9</td><td>n/a</td><td>n/a</td></tr><tr><td>Configuration Group</td><td>yes</td><td>no</td><td>yes</td><td>yes</td></tr><tr><td>Monitoring</td><td>metric + log</td><td>no</td><td>coming soon</td><td>coming soon</td></tr><tr><td>Backup Method</td><td>n/a</td><td>n/a</td><td>Full</td><td>Full</td></tr><tr><td>Auto Backup</td><td>n/a</td><td>n/a</td><td>Hourly, Daily, Weekly, Monthly</td><td>Hourly, Daily, Weekly, Monthly</td></tr><tr><td>Integrate vBackup</td><td>no</td><td>no</td><td>yes</td><td>yes</td></tr><tr><td>Backup Location</td><td>n/a</td><td>n/a</td><td>HCM or HAN</td><td>HCM or HAN</td></tr></tbody></table>
