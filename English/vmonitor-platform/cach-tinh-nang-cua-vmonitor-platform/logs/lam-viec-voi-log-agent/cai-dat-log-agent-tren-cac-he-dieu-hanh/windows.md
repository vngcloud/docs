# Windows

Trước khi thực hiện cài đặt agent trên các hệ điều hành mà chúng tôi hỗ trợ bên dưới, bạn cần phải tải xuống certificate theo hướng dẫn tại [Khởi tạo Certificate](../khoi-tao-certificate.md). Trong tệp tải xuống sẽ chứa các certificate được sử dụng để xác thực với hệ thống vMonitor Logs. Sử dụng thông tin này với các hướng dẫn bên dưới để hoàn thành việc thiết lập Agent for Log.

#### Cài đặt

Xác định một loại agent mà mình muốn cài và làm theo hướng dẫn của agent đó dưới đây:

|

* Tải filebeat tại [https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.7.1-windows-x86\_64.zip](https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.7.1-windows-x86\_64.zip)
* Giải nén thư mục filebeat vừa tải xuống
* Sao chép các file user.cer.pem, user.key.pem, VNG.trust.pem từ thư mục certificate vào thư mục filebeat đã giải nén. giả sử dưới đây chúng tôi đã giải nén filebeat vào thư mục `C:\filebeat-8.7.1-windows-x86_64`
* Chạy thủ công câu lệnh bên dưới với PowerShell

| <pre><code>cd C:\filebeat-8.7.1-windows-x86_64
.\filebeat.exe -c .\filebeat.yml
</code></pre> |
| --------------------------------------------------------------------------------------------- |

* Trong đó:\
  Trong file filebeat.yml, chúng tôi đã thiết lập ví dụ trong thư mục certificate tải về như dưới để đẩy nội dung file C:\agent.log về hệ thống.

| <pre><code>filebeat.inputs:

type: log
paths:

C:\agent.log



output.kafka:
hosts: ["$BOOTSTRAP_SERVERS"]
topic: $TOPIC
partition.round_robin:
reachable_only: false
required_acks: 1
compression: gzip
max_message_bytes: 1000000
ssl.certificate_authorities:
- $PATH_FILE_VNG_TRUST_PEM
ssl.certificate: $PATH_FILE_USER_CER_PEM
ssl.key: $PATH_FILE_USER_KEY_PEM
ssl.verification_mode: "none"
logging.level: info
logging.to_files: true
logging.files:
path: /var/log/filebeat
name: filebeat
keepfiles: 7
permissions: 0644
</code></pre> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Trong đó:

* Tại `input` đường dẫn tới file log
* Tại `output` , các biến cần điền bạn lấy từ bước tải certicate ở trên:
  * `$BOOTSTRAP_SERVERS, $TOPIC` lấy trong file [info.md](http://info.md/)
  * `$PATH_FILE_VNG_TRUST_PEM,$PATH_FILE_USER_CER_PEM,$PATH_FILE_USER_KEY_PEM` là đường dẫn tới file VNG.trust.pem user.cer.pem user.key.pem

Cài đặt service chạy background:

Trên powershell khi đã vào đường dẫn filebeat

| <pre><code>.\install-service-filebeat.ps1



Chúng tôi khuyên bạn nên thử chạy thủ công thành công trước để xác định vấn đề nếu có.
</code></pre> |
| ------------------------------------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                                                   |
| <pre><code>cd C:\filebeat-8.7.1-windows-x86_64
</code></pre>                                                                                      |
| .\filebeat.exe -c .\filebeat.yml                                                                                                                  |
|                                                                                                                                                   |
| <pre><code>filebeat.inputs:
</code></pre>                                                                                                         |

* type: log paths:
  * C:\agent.log

output.kafka: hosts: \["$BOOTSTRAP\_SERVERS"] topic: $TOPIC partition.round\_robin: reachable\_only: false required\_acks: 1 compression: gzip max\_message\_bytes: 1000000 ssl.certificate\_authorities: - $PATH\_FILE\_VNG\_TRUST\_PEM ssl.certificate: $PATH\_FILE\_USER\_CER\_PEM ssl.key: $PATH\_FILE\_USER\_KEY\_PEM ssl.verification\_mode: "none" logging.level: info logging.to\_files: true logging.files: path: /var/log/filebeat name: filebeat keepfiles: 7 permissions: 0644 | |

```
.\install-service-filebeat.ps1
```

|

***

|

* Tải [Download the Microsoft Build of OpenJDK](https://learn.microsoft.com/en-us/java/openjdk/download) file zip và giải nén . Tối thiểu yêu cầu jdk11.
* Sau khi cài xong, thêm biến môi trường LS\_JAVA\_HOME . Mở powershell với quyền administrator chạy lệnh dưới ( giả sử bước trên bạn đã giải nén vào C:\Program Files (x86)\Java\ ) :

| <pre><code>SETX /m PATH "$env:PATH;C:\Program Files (x86)\Java\jdk-11.0.3\bin;"
SETX /m LS_JAVA_HOME "C:\Program Files (x86)\Java\jdk-11.0.3"
In some environments you must replace "Program Files (x86)" by progra~2, like:
SETX /m LS_JAVA_HOME "C:\progra~2\Java\jdk"
</code></pre> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

* Kiểm tra

| <pre><code>Java --verison
java version "11.0.3" 2019-04-16 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.3+12-LTS)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.3+12-LTS, mixed mode)
</code></pre> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Cài logstash:

* Tải [![](https://www.elastic.co/favicon-16x16.png)Logstash 8.6.2](https://www.elastic.co/downloads/past-releases/logstash-8-6-2) và giải nén.
* Coppy các file logstash.conf, user.key, VNG.trust từ thư mục certificate vào thư mục config vừa giải nén. giả sử dưới đây chúng tôi đã giải nén logstash vào thư mục `C:\logstash-8.6.2`
* Chạy thủ công , mở PowerShell

| <pre><code>cd C:\logstash-8.6.2
.\bin\logstash.bat -f .\config\logstash.conf
</code></pre> |
| ------------------------------------------------------------------------------------------ |

* Trong đó:\
  Trong file logstash.conf, chúng tôi đã thiết lập ví dụ như dưới để đẩy nội dung file C:\install.log về hệ thống.

| <pre><code>input {
file {
path => ["C:/install.log"]
}
stdin{}
}
output {
kafka {
codec => json
bootstrap_servers => "$BOOTSTRAP_SERVERS"
topic_id => "$TOPIC"
security_protocol => "SSL"
ssl_truststore_location => "$PATH_FILE_VNG_TRUST"
ssl_truststore_password => "$TRUTSTORE_PASS"
ssl_keystore_location => "$PATH_FILE_USER_KEY"
ssl_keystore_password => "$USER_PASS"
ssl_key_password => "$USER_PASS"
ssl_endpoint_identification_algorithm => ""
}
}
</code></pre> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

* Chạy ngầm bằng Task Scheduler

Chúng tôi khuyên bạn nên thử chạy thủ công thành công trước để xác định vấn đề nếu có. Tham khảo thêm tại [Running Logstash on Windows | Logstash Reference \[8.6\] | Elastic](https://www.elastic.co/guide/en/logstash/8.6/running-logstash-windows.html#running-logstash-windows-scheduledtask).

\| | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | |

```
SETX /m PATH "$env:PATH;C:\Program Files (x86)\Java\jdk-11.0.3\bin;"
SETX /m LS_JAVA_HOME "C:\Program Files (x86)\Java\jdk-11.0.3"
In some environments you must replace "Program Files (x86)" by progra~2, like:
SETX /m LS_JAVA_HOME "C:\progra~2\Java\jdk"
```

\| |

```
Java --verison
java version "11.0.3" 2019-04-16 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.3+12-LTS)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.3+12-LTS, mixed mode)
```

\| |

```
cd C:\logstash-8.6.2
.\bin\logstash.bat -f .\config\logstash.conf
```

\| |

```
input {
file {
path => ["C:/install.log"]
}
stdin{}
}
output {
kafka {
codec => json
bootstrap_servers => "$BOOTSTRAP_SERVERS"
topic_id => "$TOPIC"
security_protocol => "SSL"
ssl_truststore_location => "$PATH_FILE_VNG_TRUST"
ssl_truststore_password => "$TRUTSTORE_PASS"
ssl_keystore_location => "$PATH_FILE_USER_KEY"
ssl_keystore_password => "$USER_PASS"
ssl_key_password => "$USER_PASS"
ssl_endpoint_identification_algorithm => ""
}
}
```

|

\\
