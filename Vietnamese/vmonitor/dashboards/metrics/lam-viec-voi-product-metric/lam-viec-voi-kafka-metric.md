# Làm việc với Kafka-Metric

Sau khi tạo cụm Kafka thành công, hệ thống sẽ tự động thu thập Kafka metric và hiển thị ở tab Infrastructure List/vDB - Database , giúp bạn có thể theo dõi được các Kafka Project trên VNG Cloud hoàn toàn miễn phí.

Bước 1: Truy cập vào vMonitor portal:  [https://vmonitor.console.vngcloud.vn/infrastructure/vdb](https://vmonitor.console.vngcloud.vn/infrastructure/vdb)

Bước 2: Chọn filter resources Kafka

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Tại trang này ở mỗi Kafka bạn sẽ thấy các thông tin như sau:

* **Host**: Tên và ID của Kafka
* **Status**: Trạng thái về monitor của Kafka, UP là đang có dữ liệu, UNDERTERMINE là trong vòng 5p chưa có dữ liệu mới
* **Broker online**: Broker đang hoạt động, kết nối tốt và sẵn sàng xử lý dữ liệu
* **Messages in per second**: Số lượng message mà toàn bộ cluster (hoặc một broker cụ thể) nhận được từ producer **trong một giây**
* **Messages consumed per second**: Số lượng message mà consumer (hoặc consumer group) đang đọc từ Kafka **trong một giây**
* **Detailed Monitoring**: mặc định là tắt, khi bạn có nhu cầu cần vẽ các Kafka metric khác ngoài các Metric mà dashboard mặc định chúng tôi đã vẽ và tạo các Alarm để cảnh báo với tài nguyên này, thì bạn cần bật tính năng này lên. Để bật tính năng này bạn cần mua gói Metric Quota (gói có phí hoặc miễn phí).

&#x20;Khi click vào tên của Kafka, bạn sẽ được chuyển sang trang Dashboard, và xem default dashboard của Kafka này (Tên dashboard của Kafka: vDB-Kafka-Project\_Name-{suffix Kafka ID})).

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Chú ý:**

* Sau khi tạo Kafka, hệ thống vMonitor sẽ mất 1 khoảng thời gian trung bình 5-10 phút (có thể có trường hợp lâu nhất là 20 phút) để cập nhập Kafka metric.
* Để xem danh sách metrics tương ứng với mỗi Kafka, xem tại [Danh sách Metrics hỗ trợ](../../../../vmonitor-platform/cach-tinh-nang-cua-vmonitor-platform/metrics/danh-sach-metrics-ho-tro/).
{% endhint %}

<br>
