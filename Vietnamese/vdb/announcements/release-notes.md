# Release Notes

Tổng hợp các bản cập nhật và tính năng mới của tất cả các engine trong dịch vụ vDB.

---

## April 03, 2026 - vDB PostgreSQL Cluster (RDS) <a href="#april_03_2026_postgresql_cluster" id="april_03_2026_postgresql_cluster"></a>

GreenNode ra mắt tính năng PostgreSQL Cluster cho dịch vụ vDB Relational, cho phép triển khai PostgreSQL với kiến trúc High Availability, tự động Failover và khả năng scale linh hoạt cho môi trường production.

* Kiến trúc High Availability: Hỗ trợ từ 2 đến 10 nodes, tự động failover khi Writer gặp sự cố.
* Hai Endpoint RW & RO riêng biệt: dễ dàng scale out các heavy-read workload.
* Tích hợp sẵn với vBackup: dễ dàng thiết lập các Backup Policy, Vault Lock tại Backup Center.
* Hỗ trợ các extension phổ biến: pgvector, timescaledb, postgis, pg_stat_statements,... phù hợp với nhiều usecase như VectorDB for AI, high-performance real-time analytics, ...
* Tìm hiểu thêm tại [PostgreSQL Cluster](../relational-database-service-rds/postgresql/postgresql-cluster.md).

---



## April 08, 2025 - vDB OpenSearch Cluster (ODS) `<a href="#april_08_2025_ods" id="april_08_2025_ods"></a>`

GreenNode vừa ra phiên bản đầu tiên cho dịch vụ vDB OpenSearch, mang đến cho bạn trải nghiệm quản lý logs và tìm kiếm dữ liệu mạnh mẽ và hiệu quả hơn bao giờ hết!

**Điểm nổi bật:**

* **Triển khai dễ dàng:** Dễ dàng khởi tạo và quản lý các OpenSearch Cluster chỉ với vài bước đơn giản trên giao diện vDB.&#x20;
* **Dễ dàng tiếp nhận log từ nhiều nguồn:** OpenSearch có thể dễ dàng tiếp nhận log từ các nguồn khác trong hoặc ngoài hệ sinh thái GreenNode như: Database (PostgreSQL, MySQL, Redis, Kafka, MongoDB), VKS,...
* **Mở rộng dễ dàng:** Cho phép scale up OpenSearch Cluster một cách linh hoạt để đáp ứng nhu cầu ngày càng tăng về hiệu suất và dung lượng lưu trữ.
* **Phân tích dữ liệu theo thời gian thực:** Khả năng phân tích log, ứng dụng, chỉ số hiệu năng và bảo mật trong thời gian thực, với giao diện trực quan, tương tác cao.
* **Bảo mật:** OpenSearch tăng cường bảo mật bởi các tính năng như Encryption sử dụng VNG Managed Keys, Encryption in transit, Encryption within Cluster. Ngoài ra, bạn có thể chủ động tạo và quản lý Master User Password để truy cập trực tiếp vào OpenSearch Dashboard, phục vụ nhu cầu quan sát và phân tích dữ liệu theo thời gian thực.
* **Dễ dàng mở rộng với đa dạng plugin:** Bạn có thể sử dụng các plugin để hỗ trợ bạn mở rộng sử dụng OpenSearch Cluster cho nhiều usecase khác nhau, ví dụ plugin kNN có thể được sử dụng để ứng dụng trong tìm kiếm vector và machine learning,...
* **Tối ưu chi phí:** Trả phí minh bạch, rõ ràng, giúp bạn kiểm soát ngân sách hiệu quả.

Hãy liên hệ với chúng tôi để được tư vấn và hỗ trợ thêm!

---

## Oct 02, 2024 - vDB Kafka Cluster (KDS) `<a href="#oct_02_2024_kds" id="oct_02_2024_kds"></a>`

vDB Kafka Cluster chính thức ra mắt, đánh dấu một bước tiến quan trọng trong việc tối ưu hóa quy trình xử lý dữ liệu. vDB Kafka Cluster giúp bạn phân tích dữ liệu và đưa ra quyết định kinh doanh một cách nhanh chóng và chính xác hơn. Bên cạnh đó, giao diện người dùng trực quan và dễ sử dụng sẽ giúp bạn làm quen với công cụ một cách nhanh chóng.

<table data-full-width="true"><thead><tr><th width="169.5">Tính năng</th><th width="522">Mô tả</th><th width="135">Region</th><th>Tài liệu</th></tr></thead><tbody><tr><td><strong>Quản lý DB Kafka Cluster</strong></td><td><p>Việc quản lý DB Kafka Cluster trở nên dễ dàng hơn bao giờ hết thông qua việc tương tác với portal, website hỗ trợ đầy đủ các tính năng như:</p><ul><li><strong>Tạo cụm:</strong> Dễ dàng khởi tạo cụm Kafka với các tùy chọn cấu hình linh hoạt.</li><li><strong>Điều chỉnh số lượng broker:</strong> Tăng hoặc giảm số lượng broker để đáp ứng nhu cầu xử lý dữ liệu.</li><li><strong>Mở rộng lưu trữ:</strong> Tăng dung lượng lưu trữ cho các broker khi cần thiết.</li><li><strong>Chỉnh sửa cấu hình:</strong> Tùy chỉnh các tham số Kafka để tối ưu hóa hiệu suất và độ tin cậy.</li><li><strong>Version</strong>: Hỗ trợ các version 3.6, 3.6.1, 3.7</li></ul><p></p></td><td>HCM03</td><td><a href="../kafka-cluster-kds/bat-dau-voi-kafka-cluster.md">Bắt đầu với DB Kafka Cluster.</a><br><a href="../kafka-cluster-kds/quan-ly-kafka-cluster/">Quản lý DB Kafka Cluster.</a></td></tr><tr><td><strong>Bảo mật và kiểm soát truy cập</strong></td><td><p>Cơ chế bảo mật và kiểm soát truy cập linh hoạt với các tính năng như:</p><ul><li><strong>Phương thức truy cập đa dạng:</strong> Hỗ trợ mTLS, SASL và Public Accessibility.</li><li><strong>Quản lý người dùng:</strong> Tạo, phân quyền và xóa người dùng Kafka.</li><li><strong>Quản lý topic:</strong> Tạo, xóa, sửa đổi cấu hình topic.</li><li><strong>Cập nhật certificate:</strong> Tạo mới chứng chỉ trong trường hợp chứng chỉ cũ hết hạn hoặc không thể truy cập.</li><li><strong>Hỗ trợ các tính năng encrypt dữ liệu</strong>: Encryption at rest (volume), Encryption within the cluster (brokers to brokers), Encryption in transit (clients to brokers)</li></ul></td><td>HCM03</td><td><a href="../kafka-cluster-kds/quan-ly-kafka-cluster/chinh-sua-phuong-thuc-truy-cap.md">Chỉnh sửa phương thức truy cập</a></td></tr></tbody></table>
