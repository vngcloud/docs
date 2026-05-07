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

<table><thead><tr><th width="164">Engine</th><th width="148">MySQL Single</th><th width="148">Mariadb Single</th><th width="148">Postgresql Single</th><th width="120">Redis Single</th><th width="137">Kafka Cluster</th><th width="148">Opensearch Cluster</th><th width="211">Postgresql Cluster (New)</th></tr></thead><tbody><tr><td>Supported AZ</td><td>HCM 1a, 1b, 1c</td><td>HCM 1a, 1b, 1c</td><td>HCM 1a, 1b, 1c</td><td>HCM 1a, 1b, 1c</td><td>HCM 1a</td><td>HCM 1a, 1b, 1c</td><td>HCM 1a, 1b, 1c</td></tr><tr><td>Multi-AZ Replication</td><td>yes</td><td>yes</td><td>yes</td><td>yes</td><td>no</td><td>no</td><td>coming soon</td></tr><tr><td>Auto failover</td><td>no</td><td>no</td><td>no</td><td>no</td><td>yes</td><td>yes</td><td>yes</td></tr><tr><td>Scale Up Flavor</td><td>yes</td><td>yes</td><td>yes</td><td>yes</td><td>yes</td><td>yes</td><td>coming soon</td></tr><tr><td>Scale Up Storage</td><td>yes</td><td>yes</td><td>yes</td><td>n/a</td><td>yes</td><td>yes</td><td>yes</td></tr><tr><td>Scale out (read-replica)</td><td>yes, up to 5</td><td>yes, up to 5</td><td>yes, up to 5</td><td>yes, up to 5</td><td>no</td><td>no</td><td>yes, up to 9</td></tr><tr><td>Scale out (writer)</td><td>n/a</td><td>n/a</td><td>n/a</td><td>n/a</td><td>yes, up to 10</td><td>yes, up to 9</td><td>n/a</td></tr><tr><td>Configuration Group</td><td>yes</td><td>yes</td><td>yes</td><td>yes</td><td>yes</td><td>no</td><td>yes</td></tr><tr><td>Monitoring</td><td>metric</td><td>metric</td><td>metric</td><td>metric</td><td>metric + log</td><td>no</td><td>coming soon</td></tr><tr><td>Backup Method</td><td>Full, Incremental</td><td>Full, Incremental</td><td>Full, Incremental</td><td>Full, Incremental</td><td>n/a</td><td>n/a</td><td>Full</td></tr><tr><td>Auto Backup</td><td>Daily</td><td>Daily</td><td>Daily</td><td>Daily</td><td>n/a</td><td>n/a</td><td>Hourly, Daily, Weekly, Monthly</td></tr><tr><td>Integrate vBackup</td><td>no</td><td>no</td><td>no</td><td>no</td><td>no</td><td>no</td><td>yes</td></tr><tr><td>Backup Location</td><td>HCM</td><td>HCM</td><td>HCM</td><td>HCM</td><td>n/a</td><td>n/a</td><td>HCM or HAN</td></tr><tr><td>Version</td><td>5.7, 8.0</td><td>10.3, 10.4, 10.5</td><td>12, 13, 14, 15</td><td>4.0, 5.0, 6.2, 7.2</td><td>3.6.0, 3.6.1,  3.7.0</td><td>2.15, 2.17</td><td>15, 16, 17</td></tr><tr><td>Authentication</td><td>Username/Password</td><td>Username/Password</td><td>Username/Password</td><td>Password</td><td>SASL/mTLS</td><td>Username/Password</td><td>Username/Password</td></tr><tr><td>Encryption at-rest</td><td>no</td><td>no</td><td>no</td><td>no</td><td>yes</td><td>no</td><td>no</td></tr></tbody></table>
