Database Monitoring là việc giám sát toàn diện CSDL MySQL của bạn thông qua việc thu thập các số liệu metrics, logs. Bạn có thể sử dụng thông tin này để cải thiện hiệu suất các ứng dụng của mình và đảm bảo CSDL của bạn luôn hoạt động trơn tru.

Để thu thập dữ liệu giám sát, bạn có thể sử dụng Agent với tư cách là người dùng chỉ đọc (Read-Only User). Hãy thực hiện theo các bước bên dưới để bật giám sát CSDL của bạn: 

* [Thông tin chung](#thông-tin-chung)
* [Chuẩn bị](#chuẩn-bị)
* [Cấu hình MySQL/MariaDB](#cấu-hình-mysql/mariadb)
* [Grant quyền truy cập cho Agent](#grant-quyền-truy-cập-cho-agent)
* [Cài đặt](#cài-đặt)
  * [Cài đặt Agent với Docker](#cài-đặt-agent-với-docker)
  * [Cài đặt Agent với process](#cài-đặt-agent-với-process)
* [Gỡ cài đặt Agent](#gỡ-cài-đặt-agent)



# Thông tin chung

*  **Các versions MySQL, MariaDB hỗ trợ: ** 


    *  **MySQL:** 5.6, 5.7, or 8.0+


    *  **MariaDB** : 10.1+



    
*  **Ảnh hưởng hiệu năng:** 


    * Cấu hình mặc định của Agent đã được thiết lập để phù hợp cho việc giám sát CSDL. Bạn có thể điều chỉnh các cài đặt như khoảng thời gian thu thập (collection interval) và tỉ lệ thực hiện truy vấn (query sampling rate)  để phù hợp hơn với nhu cầu của mình. Đối với hầu hết các khối lượng công việc, Agent chiếm ít hơn 1% thời gian thực hiện truy vấn trên CSDL và ít hơn 1% CPU.

    


*  **Proxies, cân bằng tải (load balancers), và kết nối (connection poolers):** 
    * Agent có thể kết nối gián tiếp với host (máy chủ) cần được giám sát.

    


*  **Bảo mật (Data security):** 


    * Agent bảo mật dữ liệu trong câu truy vấn thông qua việc thay thế các tham số 
    * Agent làm bình thường hóa các truy vấn và cũng làm xáo trộn tất cả các tham số trong truy vấn được gửi đến hệ thống vMonitor Platform. Do đó, mật khẩu, PII (Thông tin nhận dạng cá nhân) và các thông tin nhạy cảm khác được lưu trữ trong CSDL của bạn sẽ không thể xem được trong metric hoặc logs. Tuy nhiên, có một số nguồn rủi ro bảo mật dữ liệu phổ biển: 
    *  **Database schema:** những dữ liệu như tên bảng, tên cột, chỉ mục (index), tên CSDL hoặc bất kỳ thành phần nào khác chứa thông tin nhạy cảm sẽ không bị xáo trộn bởi Agent. Nếu bạn cho rằng Database schema của mình chứa thông tin nhạy cảm, bạn nên cân nhắc áp dụng các biện pháp bảo mật bổ sung, chẳng hạn như mã hóa database schema.


    *  **Database logs:**  Nếu bạn đang gửi logs đến vMonitor Platform từ CSDL của mình, hãy lưu ý rằng một số logs có thể chứa văn bản truy vấn SQL đầy đủ bao gồm các tham số nằm trong câu truy vấn. Xem xét và áp dụng các quy tắc bảo mật logs phù hợp với yêu cầu của tổ chức bạn như xóa các tham số nhạy cảm trong câu truy vấn trước khi gửi chúng đến vMonitor Platform, mã hóa logs trước khi gửi chúng đến vMonitor Platform, hay hạn chế quyền truy cập vào logs,...


    *  **Query comments: ** Agent có thể thu thập comment truy vấn SQL và gửi đến vMonitor Platform. Comment truy vấn SQL thường không chứa dữ liệu nhạy cảm, nhưng các comment được trích xuất từ truy vấn SQL sẽ không vượt qua được quá trình làm rối mã nguồn. Nếu bạn cho rằng comment truy vấn SQL của mình có thể chứa dữ liệu nhạy cảm, bạn nên cân nhắc không thu thập các comment này hoặc xem xét áp dụng các biện pháp bảo mật bổ sung, chẳng hạn như mã hóa chúng khi gửi chúng đến vMonitor Platform.



    

    


# Chuẩn bị

* Để đẩy metrics về hệ thống vMonitor Platform, bạn cần: 
    * Kiểm tra bạn đã có Metric Quota và quota chưa chạm mức giới hạn, nếu chưa có bạn cần thực hiện mua Quota Metric tại [đây](https://docs.vngcloud.vn/pages/viewpage.action?pageId=31555658).
    *  **Tạo Service Account và gắn policy: vMonitorMetricPush để có đủ quyền đẩy Metric về vMonitor** 

Để tạo service account bạn truy cập tại [đây](https://hcm-3.console.vngcloud.vn/iam/service-accounts), sau đó thực hiện các bước sau:


    * Chọn " **Create a Service Account** ", điền tên cho Service Account và nhấn  **Next Step ** để gắn quyền cho Service Account
    * Tìm và chọn ** Policy:**   **vMonitorMetricPush, ** sau đó nhấn " **Create a Service Account** " để tạo Service Account, Policy: vMonitorMetricPush do VNG Cloud tạo ra chỉ chứa chính xác quyền đẩy metric về hệ thống
    * Sau khi tạo thành công bạn cần phải lưu lại  **Client_ID**  và  **Secret_Key**  để thực hiện bước tiếp theo.

    

    
* Để đẩy logs về hệ thống vMonitor Platform, bạn cần: 
    * Kiểm tra bạn đã có Log Project Quota và quota chưa chạm mức giới hạn, nếu chưa có bạn cần thực hiện mua Log Project tại [đây](https://docs.vngcloud.vn/pages/viewpage.action?pageId=31555637).
    * Tải xuống tệp tin Certificate tương ứng của Log project nhận logs và thực hiện giải nén. Chi tiết tham khảo tại [đây.](https://docs.vngcloud.vn/pages/viewpage.action?pageId=31555643) Sau đó sao chép 3 tệp tin (user.cer.pem, user.key.pem, VNG.trust.pem) vào thư mục /etc/vmonitor-agent/.

    


# Cấu hình MySQL/MariaDB
Để thu thập metrics và logs, bạn cần thực hiện bật MySQL Performance Schema theo câu lệnh.

vDB sẽ auto bật chế độ Performance Schema với các thông số mặc định, ví dụ: 


* performance_schema=ON


* max_digest_length=1024


* performance_schema_max_digest_length=1024


* performance_schema_max_sql_text_length=1024



 **Bạn không thể thay đổi các thông số này. Nếu thật sự có nhu cầu thay đổi, vui lòng liên hệ với chúng tôi.** 


* Cập nhật runtime consume theo câu lệnh: 


```
mysql>
UPDATE performance_schema.setup_consumers SET enabled='YES' WHERE name LIKE 'events_statements_%';
UPDATE performance_schema.setup_consumers SET enabled='YES' WHERE name = 'events_waits_current';
UPDATE performance_schema.setup_consumers SET enabled='YES' where name = 'statements_digest';
```

# Grant quyền truy cập cho Agent
Thực hiện grant quyền truy cập cho Agent theo hướng dẫn bên dưới: 


* Đối với CSDL MariaDB phiên bản từ 10.2 trở về trước: 




```
mysql>
CREATE USER vmonitor@'%' IDENTIFIED by '<UNIQUEPASSWORD>';
GRANT USAGE ON *.* TO 'vmonitor'@'%' WITH MAX_USER_CONNECTIONS 5;
GRANT REPLICATION CLIENT ON *.* TO vmonitor@'%';
GRANT PROCESS ON *.* TO vmonitor@'%';
GRANT SELECT ON performance_schema.* TO vmonitor@'%';
```

* Đối với CSDL MySQL(5.6, 5.7, or 8.0+) /MariaDB phiên bản từ 10.2 trở về sau:




```
mysql>
CREATE USER vmonitor@'%' IDENTIFIED by '<UNIQUEPASSWORD>';
ALTER USER vmonitor@'%' WITH MAX_USER_CONNECTIONS 5;
GRANT REPLICATION CLIENT ON *.* TO vmonitor@'%';
GRANT PROCESS ON *.* TO vmonitor@'%';
GRANT SELECT ON performance_schema.* TO vmonitor@'%';
```

* Tạo schema theo cú pháp:


```
mysql>
CREATE SCHEMA IF NOT EXISTS vmonitor;
GRANT EXECUTE ON vmonitor.* to vmonitor@'%';
GRANT CREATE TEMPORARY TABLES ON vmonitor.* TO vmonitor@'%';
```

* Tạo 1 procedure để cho phép Agent thu thập  **explain**  queries:


```sql
mysql>
DELIMITER $$
CREATE PROCEDURE vmonitor.explain_statement(IN query TEXT)
SQL SECURITY DEFINER
BEGIN
SET @explain := CONCAT('EXPLAIN FORMAT=json ', query);
PREPARE stmt FROM @explain;
EXECUTE stmt;
DEALLOCATE PREPARE stmt;
END $$
DELIMITER ;

```

* Ngoài ra, hãy tạo procedure này trong mọi schema mà bạn muốn thu thập metrics hay logs. Thay thế tham số <YOUR_SCHEMA> bằng database schema của bạn:


```
mysql>
DELIMITER $$
CREATE PROCEDURE <YOUR_SCHEMA>.explain_statement(IN query TEXT)
    SQL SECURITY DEFINER
BEGIN
    SET @explain := CONCAT('EXPLAIN FORMAT=json ', query);
    PREPARE stmt FROM @explain;
    EXECUTE stmt;
    DEALLOCATE PREPARE stmt;
END $$
DELIMITER ;
GRANT EXECUTE ON PROCEDURE <YOUR_SCHEMA>.explain_statement TO vmonitor@'%';
```



* Đối với các schema được tạo procedure, chúng tôi sẽ thu thập thêm thông số  **explain**  tại logs của bạn.
* Bạn không cần tạo procedure cho 4 schema mặc định bên dưới: 
    * sys
    * mysql
    * performance_schema
    * information_schema

    


# Cài đặt

## Cài đặt Agent với Docker

* Chạy command line:


```
docker run \
  --name vagent \
  --network host \
  -e V_USER=vmonitor \
  -e V_PASS=<Nhập password cho user vmonitor đã tạo trước đó> \
  -e V_HOST=<Nhập Host IP> \
  -e V_PORT=3306 \
  -e HOST_NAME=<Nhập Host Name> -- Hostname này sẽ dùng để nhận biết trên hệ thống vMonitor Platform \
  -e IAM_CLIENT_ID=<Nhập Client ID của Service Account đã khởi tạo trên IAM> \
  -e IAM_CLIENT_SECRET=<Nhập Client Secret của Service Account tương ứng> \
  -e TOPIC=<Nhập topic -- Thông tin này bạn có thể lấy tại tệp tin Certificate (cụ thể file info.md)> \
  -v /etc/vmonitor-agent/VNG.trust.pem:/etc/vmonitor-agent/VNG.trust.pem \
  -v /etc/vmonitor-agent/user.cer.pem:/etc/vmonitor-agent/user.cer.pem \
  -v /etc/vmonitor-agent/user.key.pem:/etc/vmonitor-agent/user.key.pem \
  -d vngcloud/vmonitor-agent:latest
```

## Cài đặt Agent với process

* Sử dụng Root user thực hiện chạy các command line sau để cài đặt Agent tại host của bạn:


```
V_USER=vmonitor \
V_PASS=<Nhập password cho user vmonitor đã tạo trước đó> \
V_HOST=<Nhập Host IP> \
V_PORT=3306 \
IAM_CLIENT_ID=<Nhập Client ID của Service Account đã khởi tạo trên IAM> \
IAM_CLIENT_SECRET=<Nhập Client Secret của Service Account tương ứng> \
VMONITOR_SITE=https://monitoring-agent.vngcloud.vn:443 \
IAM_URL=https://iamapis.vngcloud.vn/accounts-api/v2/auth/token \
TOPIC=<Nhập topic -- Thông tin này bạn có thể lấy tại tệp tin Certificate (cụ thể file info.md)> \
bash -c "$(curl -L https://raw.githubusercontent.com/vngcloud/opentelemetry-collector-contrib/release/v0.85.x-old/install.sh)"
```

* Cuối cùng, thực hiện restart gửi MySQL/MariaDB để bắt đầu đẩy metrics và logs về vMonitor Platform:


```powershell
sudo systemctl restart vmonitor-agent
```

```

```

# Gỡ cài đặt Agent
Khi bạn không còn nhu cầu monitor database của bạn, hãy chạy câu lệnh bên dưới để gỡ cài đặt Agent:


```

```

```powershell
sudo systemctl stop vmonitor-agent
```

```

```

```powershell
sudo apt purge vmonitor-agent
```


 



*****

[[category.storage-team]] 
[[category.confluence]] 
