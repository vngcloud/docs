# Giám sát hoạt động

## **Tổng quan**

Hệ thống vCDN hỗ trợ khách hàng giám sát và theo dõi toàn bộ hoạt động của dịch vụ CDN qua **Portal** hoặc **API**, cung cấp thông tin chi tiết, trực quan về hiệu suất và trạng thái dịch vụ.

Các chỉ số sẽ được cung cấp trực quan thành các Dashboard và biểu đồ với:&#x20;

* Dữ liệu được cập nhật với tần suất **từng phút**.
* Độ trễ tối đa là **5 phút** (cận realtime), giúp khách hàng nắm bắt kịp thời các thay đổi trong hệ thống.

## Chi tiết

Các loại biểu đồ/ báo cáo chúng tôi cung cấp cho bạn bao gồm:&#x20;

* **Traffic Consuming:** tổng lượng băng thông được sử dụng trên hệ thống CDN trong một tháng.
* **Origin Request/s**: số lượng yêu cầu (requests) gửi từ CDN tới Origin theo từng giây.
* **Origin Traffic Consuming/s (GB/s)**: lưu lượng tiêu thụ từ Origin, đo bằng GB mỗi giây.
* **Unique IPs:** Hiển thị số lượng IP duy nhất gửi yêu cầu tới hệ thống CDN.
* **Origin Speed/s:** tốc độ tải và phục vụ từ Origin theo thời gian thực.
* **Average User Speed:** Tốc độ tải trung bình từ Origin tới CDN trong một khoảng thời gian.
* **Hit Cache Ratio:** Tỷ lệ yêu cầu được phục vụ từ bộ nhớ đệm (cache) của CDN thay vì Origin.
* **Request Content Type:** Phân loại các loại nội dung yêu cầu (ví dụ: HTML, CSS, JS, hình ảnh, video).
* **CDN HTTP Codes, Origin HTTP Codes:** Theo dõi trạng thái kết nối giữa CDN và Origin (thành công, lỗi 4xx, lỗi 5xx...).
* Quản lý và theo dõi tín hiệu được đẩy đến hệ thống Live Entry point
