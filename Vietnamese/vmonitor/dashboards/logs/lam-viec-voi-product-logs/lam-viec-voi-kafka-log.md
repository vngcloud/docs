# Làm việc với Kafka-Log

Để có thể xem được log của Kafka Project bạn truy cập vào vMonitor, sau đó vào **Infrastructure list/vDB Log,** tại màn hình này sẽ giúp bạn có thể theo dõi được các Kafka project log trên VNG Cloud

Bước 1: Truy cập vào vMonitor portal:  [https://vmonitor.console.vngcloud.vn/infrastructure/vdb-log](https://vmonitor.console.vngcloud.vn/infrastructure/vdb-log)

Bước 2: Tìm các Kafka project cần xem log

Tại màn hình này, mỗi Kafka Project bạn sẽ thấy các cột thông tin cơ bản như:

* **vDB resource**: Tên và ID của Kafka Project
* **Region**: Region của Kafka Project
* **Engine**: Phiên bản đang dùng để xử lý streaming data cho kafka project
* **Log Project**: Log project sẽ chứa logs của Kafka Project khi bạn enable radio-button "Detailed Monitoring"
* **Log Project Usage**: Thông tin về mức độ sử dụng của Log Project đã được gắn vào Kafka Project này
* **Monitoring Status**: Trạng thái monitoring của Kafka Project, nếu chưa enable "Detailed Monitoring" thì trạng thái sẽ là INACTIVE, nếu đã enable thì trạng thái là ACTIVE và bạn có thể vào Log Project được gắn để xem Kafka Logs
* **Detailed Monitoring**: Bật tắt theo dõi Logs của Kafka Project.

Để có thể xem Logs của Kafka Project bạn cần nhấn **enable** tại cột **Detailed Monitoring**, hệ thống sẽ hiển thị Popup và  **chọn Log Project** để chứa logs của Kafka Project này. Nếu bạn chưa có bất kì Log Project nào, bạn có thể nhấn "Create a log project" ở popup hoặc qua tab Quota & Usage để tạo Log Project trước.

<figure><img src="../../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Sau khi enable bạn sẽ thấy status của Kafka Project này chuyển thành **ACTIVE**, và bạn có thể truy cập vào Log Project vừa chọn để xem logs

Nếu có nhu cầu thay đổi Log Project chứa Logs, bạn chọn nút 3 chấm và chọn "**Edit Log Project**" để thay đổi.

Nếu không còn nhu cầu để xem logs của Kafka Project thì bạn có thể **disable** ở cột **Detailed Monitoring**.

***

## **Một số chú ý:**

* Kafka Project sau khi được tạo từ vDB Kafka Portal, sẽ mất khoảng vài phút (tối đa 10 phút) để có thể đồng bộ về vMonitor Log.
