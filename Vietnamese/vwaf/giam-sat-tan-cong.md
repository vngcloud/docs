# Giám sát tấn công

### Tổng quan

Phần **Attacks** cung cấp khả năng quan sát toàn bộ các hoạt động tấn công được WAF phát hiện.\
Chức năng này giúp người dùng theo dõi nguồn tấn công, xem các request độc hại bị chặn hoặc cho phép, và điều tra các sự cố an ninh.

Phần này bao gồm ba chế độ hiển thị chính:

* **Events** – tổng hợp các sự kiện tấn công theo IP nguồn
* **Logs** – hiển thị chi tiết từng request độc hại
* **Chi tiết tấn công** – hiển thị đầy đủ thông tin của một sự kiện cụ thể

***

### Attacks – Events (Sự kiện)

Tab **Events** cung cấp cái nhìn tổng quan về các cuộc tấn công, được nhóm theo địa chỉ IP của attacker.

Với mỗi IP nguồn, người dùng có thể xem:

* Địa chỉ IP và quốc gia
* Ứng dụng bị nhắm tới
* Số lượng tấn công phát sinh từ IP đó
* Thời gian diễn ra cuộc tấn công
* Thời điểm bắt đầu tấn công

Các bộ lọc cho phép thu hẹp dữ liệu theo:

* IP
* Domain
* Cổng dịch vụ
* Khoảng thời gian

Chế độ này đặc biệt hữu ích để:

* Phát hiện các IP tấn công lặp lại
* Nhận diện các đợt tấn công quy mô lớn hoặc đang diễn ra
* Đánh giá nhanh mức độ nguy hiểm của nguồn tấn công

***

### Attacks – Logs (Nhật ký)

Tab **Logs** cung cấp khả năng theo dõi chi tiết từng request độc hại được WAF phát hiện.

Với mỗi request, người dùng có thể xem:

* Hành động của WAF (Chặn hoặc Cho phép)
* Loại tấn công được phát hiện (ví dụ: XSS, SQL Injection)
* Đường dẫn request đầy đủ, bao gồm payload
* Địa chỉ IP của attacker
* Thời điểm xảy ra request

Các tùy chọn lọc bao gồm:

* Hành động (Blocked / Allowed / Tất cả)
* Cổng
* Địa chỉ IP
* Domain
* Loại tấn công
* Khoảng thời gian

Chế độ này thường được sử dụng để:

* Điều tra chi tiết các mối đe dọa
* Phân tích false positive
* Tinh chỉnh rule bảo mật của WAF

***

### Chi tiết tấn công

Màn hình **Attack Detail** hiển thị đầy đủ thông tin của một request tấn công cụ thể.

Thông tin bao gồm:

* URL đầy đủ kích hoạt phát hiện tấn công
* Hành động của WAF (Chặn hoặc Cho phép)
* Loại tấn công
* Địa chỉ IP và vị trí địa lý của attacker
* Payload bị phát hiện
* Module phát hiện
* Thời điểm xảy ra
* Attack ID

Bên dưới phần tổng quan, hệ thống hiển thị **request HTTP thô**, bao gồm:

* HTTP method
* Header
* Payload

Tùy theo cấu hình hệ thống, tab **Response** cũng có thể được hiển thị.

Chế độ này được sử dụng để:

* Xác minh WAF phát hiện và xử lý tấn công đúng cách
* Hiểu rõ cấu trúc và mục đích của payload độc hại
* Thu thập bằng chứng cho báo cáo sự cố an ninh
* Điều tra các mẫu tấn công lặp lại hoặc nâng cao
