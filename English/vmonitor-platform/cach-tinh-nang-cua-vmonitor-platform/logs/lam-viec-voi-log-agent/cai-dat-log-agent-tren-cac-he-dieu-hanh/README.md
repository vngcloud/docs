# Install Log Agent on OS

#### Chuẩn bị kết nối cài agent

* Nếu bạn có đầy đủ kết nối ra internet là cách tốt nhất để khi cài cài đặt agent đỡ gặp lỗi.
* Nếu phải cài qua proxy hoặc firewall. Mở policy cho phép kết nối tới các địa chỉ sau:

```
# filebeat / logstash
https://artifacts.elastic.co
fluentd
https://toolbelt.treasuredata.com
https://packages.treasuredata.com
fluentbit
https://packages.fluentbit.io
vector
https://repositories.timber.io








Nếu phải cài hoàn toàn offline, chúng tôi khuyên bạn tải filebeat. Các agent khác như fluentbit, fluentd, logstash, … có thể cần thêm các gói phụ thuộc phức tạp. Tải sẵn filebeat về máy tại địa chỉ:

| # debian, ubuntuhttps://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.6.0-amd64.debfedora, centoshttps://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.6.0-x86_64.rpmwindowshttps://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.7.0-windows-x86_64.msiSau khi tải agent xong, kết nối này có thể đóng. Bạn vẫn cần duy trì kết nối đẩy log.
```
