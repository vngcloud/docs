
# A. Master User Privileges:
Đối với vDB dạng relational database, khi khởi tạo vDB, bạn được cấp một Master User để truy cập vào vDB.

Master User này sẽ được cấp các quyền sau:


* MySQL/MariaDB:
    * Global Privileges: ALTER ROUTINE, ALTER, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, CREATE, DELETE, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, REPLICATION CLIENT, REPLICATION SLAVE, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, UPDATE.
    * Database Privileges: Full Privileges.

    

 **Lưu ý** : database privileges ngoại trừ các database hệ thống như: mysql, information_schema, performance_schema, sys. Khi bạn tạo một database mới, hệ thống sẽ tự grant all privileges cho master user. Nếu chưa có, bạn vui lòng chờ trong giây lát hoặc liên hệ VNG Cloud Support.


* Postgresql: Createrole, CreateDB, Replication.


# B. Service Users/Roles:
Đối với vDB dạng relational database, hệ thống sẽ tạo sẵn các service users/roles để thực hiện các tác vụ tự động. Bạn vui lòng không xóa các user/role này để tránh các tính năng tự động bị lỗi.


* MySQL/MariaDB: `os_admin`@`127.0.0.1`, `root`@`localhost`
* Postgresql: os_admin, postgres


# C. Import Database:
Đối với các vDB dạng Relational, khi tiến hành backup source DB, bạn chỉ cần backup các database chứa dữ liệu, tránh backup all-databases (bao gồm các database hệ thống như mysql, sys, performance_schema, information_schema) hoặc các stored procedure có definer là quyền root. Nếu trong file dump tồn tại stored procedure có definer=root, bạn vui lòng replace bằng Master User đã khai báo lúc khởi tạo vDB. VD: sed -i 's/definer=root/definer=<master_user>/g' dump.sql


# D. Failover khi vDB role Master down:
Hiện tại, vDB sẽ không tự động failover khi có sự cố đối với vDB role Master (Read/Write) trong mô hình Master/Read-Replica. Quyền quyết định việc Promote Read Replica thành Master mới sẽ thuộc về Khách hàng. Bạn lưu ý sau khi Promote, quá trình đồng bộ dữ liệu với Master trước sẽ bị ngắt và không thể rollback được. Để khôi phục tính High Avaibility cho hệ thống, bạn có thể create read-replica mới từ Standalone vDB này.

Để thực hiện việc này, bạn có thể làm theo [[hướng dẫn sau|Promote-Read-Relica-thành-Standalone]]. Quá trình này sẽ bao gồm các bước sau:


1. Bạn chọn instance có role Replica và thao tác Promote to Standalone.
1. Bạn update connection_string trong application của mình để Read/Write data vào Master mới.
1. Sau khi kiểm tra application đã ổn định, bạn chọn vào Master mới và tiến hành create read-replica từ Master mới này.
1. Bạn có thể xóa Master cũ nếu không còn nhu cầu sử dụng.



*****

[[category.storage-team]] 
[[category.confluence]] 
