Để nạp dữ liệu (import) vào RDS Instance với datastore MySQL/Mariadb, bạn có thể sử dụng công cụ  **mysqldump** .

Bạn có thể tự thực hiện thông qua các bước sau:

  * [2. Import dữ liệu vào RDS Instance.](#2.-import-dữ-liệu-vào-rds-instance.)


1. Dump dữ liệu từ MySQL server của bạn:Trên MySQL server của bạn, bạn có thể lấy danh sách database mình hiện có bằng lệnh sau:


```
mysql> show databases;
```
![](images/storage/Screenshot from 2019-10-30 17-44-08.png)

















Xác định các database cần import ví dụ như trong hình là:  _mysql02, mysql03, mysql04_ .

 **Lưu ý:**  RDS Instance không hỗ trợ import các database hệ thống như:  **mysql, performance_schema, information_schema và sys** . Bạn vui lòng bỏ qua các database này.

Sau khi đã có danh sách các database cần chuyển, bạn có thể dump dữ liệu bằng mysqldump với format tham khảo sau:


```
mysqldump -h<Local_DB_IP> -P<Local_DB_Port> -u<Local_DB_User> -p \
--single-transaction \
--routines --triggers \
--databases <Your_DB_List >> dump-database.sql
```
trong đó: 


* Local_DB_IP: IP MySQL Server của bạn.
* Local_DB_Port: Port MYSQL Server của bạn
* Local_DB_User: User trên MySQL Server của bạn.
* Your_DB_LIst: danh sách các database bạn muốn dump cách nhau bởi dấu khoảng trắng. VD:  _mysql02, mysql03, mysql04_ 

Kết quả bạn sẽ có một file  **dump-database.sql**  chứa dữ liệu sẽ import.


## 2. Import dữ liệu vào RDS Instance.
Để thực hiện import, bạn sử dụng Master User được cấp khi khởi tạo RDS Instance.

Bạn có thể dùng lệnh:


```
mysql -h<RDS Instance_IP> -P3306 -u<RDS Instance_Master_User> -p < dump-database.sql
```
với: 


* RDS Instance_IP: IP của RDS Instance
* RDS Instance_Master_User: Master User được cấp khi khởi tạo RDS Instance.

    

    

Tùy vào lượng dữ liệu của bạn mà thời gian import có thể kéo dài hay không. 

Trên đây là hướng dẫn Import dữ liệu vào RDS Instance datastore MySQL/Mariadb. Chúc bạn thực hiện thành công.



*****

[[category.storage-team]] 
[[category.confluence]] 
