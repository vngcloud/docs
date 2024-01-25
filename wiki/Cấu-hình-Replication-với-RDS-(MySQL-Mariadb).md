Để dữ liệu giữa MySQL server và RDS Instance đồng bộ hoàn toàn với nhau, bạn có thể cấu hình MySQL Replication. Lúc này, MySQL server của bạn sẽ đóng vai trò  **Master** , RDS Instance sẽ đóng vai trò  **Slave Read-Only** . Sau khi cấu hình thành công, mọi sự thay đổi trên MySQL server của bạn sẽ được đồng bộ trên RDS Instance thông qua cơ chế  **Mysql Asynchronous Replication** .



 **1. Tạo Replication User trên MySQL server của bạn:** Trên MySQL server của bạn, bạn khởi tạo một user để thực hiện Replication như sau:

VD: bạn tạo user 'rep'@'%' với password 'abcd1234' và gán Global Privileges là Replication Slave.


```
mysql> create user 'rep'@'%' identified by 'abcd1234';

mysql> grant replication slave on *.* to 'rep'@'%';

mysql> flush privileges;
```


 **2. Kiểm tra trạng thái Binary Log trên DB Server của bạn:** Để cấu hình Replication, bạn cần  **enable binary log**  trên MySQL server của bạn. 

Để kiểm tra xem MySQL server của bạn đã bật binary log hay chưa, bạn có thể sử dụng câu lệnh sau:


```
mysql> show variables like "log_bin";
```
![](images/storage/Screenshot from 2019-11-08 11-15-34.png)

Nếu kết quả là  **OFF** , bạn có thể bật  **binary log**  bằng cách thêm trong file cấu hình  **my.cnf (** đuờng dẫn mặc định thuờng là **/etc/mysql/my.cnf) ** các giá trị sau:


```
[mysqld]

log-bin=bin.log

log-bin-index=bin-log.index

max_binlog_size=100M

binlog_format=row
```


Sau đó, bạn cần restart lại dịch vụ MySQL/Mariadb. 

Đối với Ubuntu, bạn có thể sử dụng lệnh:


```
systemctl restart mysql
```


Kiểm tra lại bằng cách chạy lại câu lệnh trên: 


```
mysql> show variables like "log_bin";
```
Nếu kết quả là  **ON** , chúc mừng bạn đã cấu hình Binary Log thành công.



 **3. Dump dữ liệu từ MySQL server của bạn và Import dữ liệu vào RDS Instance:** Bạn có thể tham khảo hướng dẫn [Import dữ liệu vào RDS Instance datastore MySQL/Mariadb bằng MySQLDump](https://docs.vngcloud.vn/pages/viewpage.action?pageId=10880027).



 **4. Ghi nhận Binary Log File và Position trên MySQL server:** Trên MySQL server của bạn, bạn sử dụng lệnh sau để kiểm tra trạng thái Master: 


```
mysql> show master status;
```
Kết quả:

![](images/storage/Screenshot from 2019-11-08 11-16-05.png)

Bạn ghi nhận giá trị  **File** và  **Postion** của bin_log trên MySQL server của bạn để chuyển sang bước tiếp theo.



 **5. Cấu hình Replication trên RDS Instance:** Trên RDS Instance, bạn đăng nhập bằng Master User.

Bạn gọi Stored Procedure  **mysql.vdbaas_changeMasterHost**  với cú pháp:


```
mysql> call mysql.vdbaas_changeMasterHost('<Host>','<Replication User>','<Replication User Password>','<Binary Log File>',<Position>);
```
VD: MySQL server của bạn có thông tin như sau: 


*  **Host** : 18.139.18.\*
*  **User** : dba
*  **Password** : password
*  **Bin_log**  **File** : mysql-bin-changelog.000054
*  **Position** : 154

thì bạn sẽ có câu lệnh sau:


```
mysql> call mysql.vdbaas_changeMasterHost('18.139.18.*','dba','password','mysql-bin-changelog.000059',511);
```


Để bắt đầu quá trình Replication, bạn gọi Stored Procedure  **mysql.vdbaas_startSlave** :


```
mysql> call mysql.vdbaas_startSlave();
```


Để kiểm tra kết quả, bạn gõ lệnh: 


```
mysql> show slave status\G;
```
![](images/storage/Screenshot from 2019-11-08 11-16-18.png)

Bạn chú ý các truờng:  **Seconds_Behind_Master**  và  **Slave_SQL_Running_State** .

Nếu  **Slave_SQL_Running_State**  có giá trị  **Slave has read all relay log; waiting for more updates**  và  **Seconds_Behind_Master**  là  **0** có nghĩa là hai bên đều đã đồng bộ thành công.

Từ bậy giờ, bạn có thể tắt đồng bộ và sử dụng RDS Instance là MySQL server chính bằng lệnh:


```
mysql> call mysql.vdbaas_stopSlave();
```
hoặc giữ nguyên và sử dụng RDS Instance như là một  **Replication Slave.** 



*****

[[category.storage-team]] 
[[category.confluence]] 
