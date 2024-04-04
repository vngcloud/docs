# Làm việc với Log Agent

Chúng tôi sử dụng giao thức nhận log chuẩn **Kafka** đối với vMonitor Platform Logs. Do đó chúng tôi hỗ trợ bạn cấu hình đẩy logs từ tất cả các agent logs phổ biến hiện có như filebeat, fluentd, logstash, rsyslog, vector,… Nếu bạn còn phân vân, lời khuyên chúng tôi là cài **Filebeat** - nhẹ và hiệu năng cao, hoặc **Logstash** - với nhu cầu parse log phức tạp hơn.

| **Môi trường** | Phiên bản (Version) | **Phiên bản logstash VNG đã kiểm tra tương thích** | Phiên bản filebeat **VNG đã kiểm tra** tương thích |
| -------------- | ------------------- | -------------------------------------------------- | -------------------------------------------------- |
| Centos         | 7, 8                | logstash-8.6.2                                     | filebeat-8.7                                       |
| Debian         | 7,8,9               | logstash-8.6.2                                     | filebeat-8.7                                       |
| Ubuntu         | 14,16,18,20,22      | logstash-8.6.2                                     | filebeat-8.7                                       |
| Docker         | Từ 18 trở lên       | logstash-8.6.2                                     | filebeat-8.7                                       |
| Kubernetes     | Từ 1.18 trở lên     | logstash-8.6.2                                     | filebeat-8.7                                       |
| Windows        | 2016, 2019, 2022    | logstash-8.6.2                                     | filebeat-8.7                                       |

Để làm việc với Log Agent, bạn cần thực hiện theo các bước:

* [Chuẩn bị kết nối đẩy log](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59803494\&src=contextnavpagetreemode)
* [Khởi tạo Certificate](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59803496\&src=contextnavpagetreemode)
* [Cài đặt Log Agent trên các hệ điều hành](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59801611\&src=contextnavpagetreemode)
  * [CentOS](https://docs.vngcloud.vn/display/VPV/CentOS?src=contextnavpagetreemode)
  * [Debian/ Ubuntu](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59803507\&src=contextnavpagetreemode)
  * [Windows](https://docs.vngcloud.vn/display/VPV/Windows?src=contextnavpagetreemode)
* [Cài đặt Log Agent trên docker](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59803511\&src=contextnavpagetreemode)
* [Cài đặt Log Agent trên kubernetes](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59803513\&src=contextnavpagetreemode)

```
```
