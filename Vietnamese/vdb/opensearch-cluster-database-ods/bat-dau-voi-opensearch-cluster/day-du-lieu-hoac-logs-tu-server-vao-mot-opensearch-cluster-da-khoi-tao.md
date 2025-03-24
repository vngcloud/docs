# Đẩy dữ liệu hoặc logs từ server vào một OpenSearch Cluster đã khởi tạo

## **Đẩy dữ liệu mẫu vào OpenSearch Dashboards**

Dữ liệu mẫu sẽ giúp bạn làm quen với OpenSearch Dashboards và kiểm tra khả năng hiển thị dữ liệu.

#### **Bước 1: Tải dữ liệu mẫu**

Chạy lệnh sau để tải dữ liệu mẫu:

```bash
curl -O https://raw.githubusercontent.com/opensearch-project/documentation-website/2.19/assets/examples/ecommerce-field_mappings.json
curl -O https://raw.githubusercontent.com/opensearch-project/documentation-website/2.19/assets/examples/ecommerce.ndjson
```

#### **Bước 2: Tạo index và đẩy dữ liệu vào OpenSearch**

Chạy lệnh sau để tạo index và đẩy dữ liệu OpenSearch:

```bash
# 2. Create index and data.
curl -H "Content-Type: application/json" -X PUT "https://<<OpenSearch_Dashboard_Endpoint>>/ecommerce" -k -H "Authorization: Basic $(echo -n 'master-user:<<Master_User_Password>>' | base64)" --data-binary "@ecommerce-field_mappings.json"
curl -H "Content-Type: application/json" -X PUT "https://<<OpenSearch_Dashboard_Endpoint>>/ecommerce/_bulk" -k -H "Authorization: Basic $(echo -n 'master-user:<<Master_User_Password>>' | base64)" --data-binary "@ecommerce.ndjson"
```

Bạn cần thay thế `<<OpenSearch_Dashboard_Endpoint>>` bằng Endpoint của OpenSearch Dashboard (ví dụ:`https://your-opensearch-endpoint-hcm03.vdb-opensearch.vngcloud.vn:443` và `<<Master_User_Password>>` bằng mật khẩu tài khoản master mà bạn đã khởi tạo trước đó.

[\
](https://liemnt5-cidr-11430-2ue3z-hcm03.vdb-opensearch.vngcloud.tech)**Bước 3: Kiểm tra dữ liệu trên OpenSearch Dashboards**

1.  Truy cập **OpenSearch Dashboards** thông qua đường dẫn:

    ```
    https://your-opensearch-endpoint-hcm03.vdb-opensearch.vngcloud.vn:443
    ```
2. Vào **Stack Management** → **Index Patterns**, tạo index pattern cho `ecommerce*`.
3. Truy cập **Discover** để xem dữ liệu mẫu.

## **Đẩy event logs từ Logstash vào OpenSearch**

Nếu bạn muốn thu thập và đẩy event logs từ Logstash vào OpenSearch, hãy làm theo các bước sau:

#### **Bước 1: Cài đặt Logstash (nếu chưa có)**

Trên Ubuntu/Debian:

```bash
sudo apt update && sudo apt install logstash
```

Trên CentOS/RHEL:

```bash
sudo yum install logstash
```

#### **Bước 2: Cấu hình Logstash để gửi logs đến OpenSearch**

Tạo một file cấu hình cho Logstash, ví dụ:

```bash
sudo nano /etc/logstash/conf.d/opensearch_logstash.conf
```

Thêm nội dung sau:

```plaintext
input {
  file {
    path => "/var/log/syslog"
    start_position => "beginning"
  }
}

filter {
  grok {
    match => { "message" => "%{SYSLOGTIMESTAMP:timestamp} %{HOSTNAME:hostname} %{DATA:program}: %{GREEDYDATA:log_message}" }
  }
}

output {
  opensearch {
    hosts => ["https://your-opensearch-endpoint:9200"]
    user => "master-user"
    password => "your-master-password"
    index => "logstash-logs"
    ssl_certificate_verification => false
  }
}
```

Thay thế:

* `"https://your-opensearch-endpoint:9200"` bằng OpenSearch Receive Logs Endpoint của bạn.
* `"your-master-password"` bằng mật khẩu tài khoản master bạn đã khởi tạo trước đó.

#### **Bước 3: Khởi động Logstash**

Sau khi cấu hình xong, khởi động Logstash để bắt đầu gửi logs:

```bash
sudo systemctl start logstash
```

#### **Bước 4: Kiểm tra dữ liệu trong OpenSearch**

Bạn có thể kiểm tra logs bằng API OpenSearch:

```bash
curl -X GET "<<OpenSearch_Dashboard_Endpoint>>/logstash-logs/_search?pretty" -k \
-H "Authorization: Basic $(echo -n 'master-user:<<Master_User_Password>>' | base64)"
```

Nếu logs xuất hiện, có nghĩa là Logstash đã gửi dữ liệu thành công vào OpenSearch.

#### **Bước 5: Xem logs trên OpenSearch Dashboards**

1. Truy cập **OpenSearch Dashboards**.
2. Vào **Stack Management** → **Index Patterns**, tạo index pattern cho `logstash-logs*`.
3. Chuy cập **Discover** để xem logs.
