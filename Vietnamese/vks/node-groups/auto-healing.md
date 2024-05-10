# Auto Healing

### Tổng quan

Trên hệ thống VKS, tính năng Auto Healing được apply cho mỗi Node Group và luôn luôn ở trạng thái bật. Việc bật tính năng tự phục hồi (self-healing) trong Kubernetes mang lại nhiều lợi ích quan trọng, giúp đảm bảo tính sẵn sàng và độ tin cậy cao cho ứng dụng của bạn.&#x20;

***

### Cơ chế hoạt động

#### Cơ chế Auto Healing: hệ thống VKS thực hiện kích hoạt auto healing khi

* Node báo cáo trạng thái **NotReady** trong các lần kiểm tra liên tiếp trong khoảng thời gian **10 phút**.

Nếu thỏa mãn điều kiện trên, hệ thống sẽ ngay lập tức thực hiện auto healing. Quá trình này được thực hiện theo 3 bước:

* Bước 1: Hệ thống VKS thực hiện drain node, tức là di chuyển tất cả các pod đang chạy trên node NotReady này sang các node khác trong node group trước khi gỡ bỏ node đó khỏi node group.&#x20;
* Bước 2: Hệ thống sẽ tạo lại node mới với cấu hình đã được thiết lập trên node group và thực hiện join node này vào cụm. Nếu sau khi khởi động lại, node vẫn báo cáo trạng thái "NotReady", hệ thống sẽ tiếp tục khởi động lại node cho đến khi node trở lại trạng thái hoạt động bình thường.&#x20;
* Bước 3: Hệ thống sẽ di chuyển (move) các pod sang node mới.
