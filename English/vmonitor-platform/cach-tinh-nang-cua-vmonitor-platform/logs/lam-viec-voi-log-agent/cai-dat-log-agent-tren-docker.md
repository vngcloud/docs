# Install Log Agent on Docker

Trước khi thực hiện cài đặt agent trên các hệ điều hành mà chúng tôi hỗ trợ bên dưới, bạn cần phải tải xuống certificate theo hướng dẫn tại [Khởi tạo Certificate](khoi-tao-certificate.md). Thông tin hướng dẫn thiết lập agent nằm trong file readme, các script hướng dẫn cũng nằm trong tệp tin certificate được tải về. Sử dụng thông tin này với các hướng dẫn bên dưới để hoàn thành việc thiết lập Agent for Log.

#### Cài đặt

* Tải image

<pre><code>docker pull docker.elastic.co/beats/filebeat:8.7.0








| docker pull docker.elastic.co/logstash/logstash-oss:8.6.2lấy thông tin xác thực userNếu sử dụng script chuẩn bị sẵn trong thư mục tải về, chạy lệnh:Trong ví dụ thiết lập dưới dây chúng tôi sẽ mount /var/log/app.log vào agent cài bằng docker để đẩy log về hệ thống| docker compose up -d -f docker-compose.ymlCác file cấu hình dưới đều đã được chúng tôi chuẩn bị sẵn tại script khi tải certificate về, mô tả dưới đây giúp người đọc hình dung được nếu tạo manual sẽ thế nào.Cấu hình| File docker-compose.ymlFile filebeat.yml . Cấu hình dưới đây sẽ lấy tất cả log được ghi vào file /var/log/app.log về vMonitor Platform:image: docker.elastic.co/beats/filebeat:8.7.0container_name: filebeat-agent-vmonitorrestart: alwaysenv_file:  - container.envvolumes:  -  $PWD/filebeat.yml:/usr/share/filebeat/filebeat.yml  -  $PWD/VNG.trust.pem:/usr/share/filebeat/VNG.trust:rw  -  $PWD/user.cer.pem:/usr/share/filebeat/user.cer.pem:rw  -  $PWD/user.key.pem:/usr/share/filebeat/user.key.pem:rw  -  /var/log/app.log:/var/log/app.log:ro  -  /var/log/filebeat/:/var/log/filebeat/logging:  driver: "json-file"  options:    max-size: "50m"deploy:  resources:     limits:       cpus: '1'       memory: 2G                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  || filebeat.inputs:type: logpaths:/var/log/app.logoutput.kafka:hosts: ${BOOTSTRAP_SERVERS}topic: ${TOPIC}partition.round_robin:reachable_only: falserequired_acks: 1compression: gzipmax_message_bytes: 1000000ssl.certificate_authorities:- /usr/share/filebeat/VNG.trustssl.certificate: /usr/share/filebeat/user.cer.pemssl.key: /usr/share/filebeat/user.key.pemssl.verification_mode: "none"logging.level: infologging.to_files: truelogging.files:path: /var/log/filebeatname: filebeatkeepfiles: 7permissions: 0644                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    || File docker-compose.ymlFile logstash.conf . Cấu hình dưới đây sẽ lấy tất cả log được ghi vào file /var/log/app.log về vMonitor Platform:image: docker.elastic.co/logstash/logstash-oss:8.6.2container_name: logstash-agent-vmonitorrestart: alwaysenv_file:  - container.envvolumes:  -  $PWD/logstash.conf:/usr/share/logstash/pipeline/logstash.conf  -  $PWD/VNG.trust:/usr/share/logstash/VNG.trust  -  $PWD/user.key:/usr/share/logstash/user.key  -  /var/log/app.log://var/log/app.log:rologging:  driver: "json-file"  options:    max-size: "50m"deploy:  resources:     limits:       cpus: '1'       memory: 2G                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| input {file {start_position => "beginning"path => [ "/var/log/app.log" ]}}output {kafka {codec => jsonbootstrap_servers => "${BOOTSTRAP_SERVERS}"topic_id => "${TOPIC}"security_protocol => "SSL"ssl_truststore_location => "/usr/share/logstash/VNG.trust"ssl_truststore_password => "${TRUTSTORE_PASS}"ssl_keystore_location => "/usr/share/logstash/user.key"ssl_keystore_password => "${KEYSTORE_PASS}"ssl_key_password => "${KEYSTORE_PASS}"ssl_endpoint_identification_algorithm => ""}}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
<strong>Quản trị
</strong>| StopReloadRestartObserveUninstall



































| StopReloadRestartObserveUninstall


































Trước khi thực hiện cài đặt tác nhân trên các hệ điều hành mà chúng tôi hỗ trợ bên dưới, bạn cần tải xuống chứng chỉ theo hướng dẫn tại Khởi tạo Chứng chỉ. Thông báo hướng dẫn tác nhân thiết lập nằm trong tệp readme, hướng dẫn tập lệnh cũng nằm trong tệp tin chứng chỉ được tải về. Sử dụng thông tin này với các hướng dẫn bên dưới để hoàn thành việc thiết lập Agent for Log.
</code></pre>
