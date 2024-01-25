Để đẩy Log về vMonitor, bạn cần cài đặt Log Agent trên server, vMonitor hỗ trợ rất nhiều Log Agent như: filebeat, fluentd, logstash và rsyslog. Bạn có thể sử dụng các certificate tải từ trang Certificate (nếu chưa tải bạn đọc hướng dẫn tại [đây](https://docs.vngcloud.vn/pages/viewpage.action?pageId=31555643)), nếu bạn đã có các Agent kể trên, bạn có thể sử dụng các certificate file trong tập tin tải về. Nếu chưa cài bất kì Log Agent nào, bạn có thể đọc hướng dẫn trong file readme và cài bằng các script trong tập tin tải về.

![](images/storage/image2021-5-14_14-37-11.png)

Hoặc đọc các hướng dẫn tại trang Integration/Agent for Log, ví dụ coi chi tiết hướng dẫn Logstash

![](images/storage/image2021-5-14_14-39-33.png)

![](images/storage/image2021-5-14_14-44-12.png)

Giả sử bạn muốn đẩy log từ /var/log/applog/applog.log, bạn cần vào thư mục Linux/logstash/, chạy các câu lệnh:


* sudo chmod u+x logstash.sh
* sudo /logstash.sh /var/log/applog/applog.log
* sudo systemctl enable logstash.service


* sudo systemctl start logstash.service



Sau đó bạn có thể vào tab Log/Log Search để coi Log đẩy về.

![](images/storage/image2021-5-14_15-38-1.png)





*****

[[category.storage-team]] 
[[category.confluence]] 
