# Quản lý ứng dụng WAF

### Tổng quan

Phần **Applications** cho phép người dùng quản lý toàn bộ các ứng dụng (website hoặc dịch vụ) được bảo vệ bởi WAF.

Tại trang này, người dùng có thể:

* Theo dõi trạng thái bảo vệ và chế độ hoạt động
* Kiểm tra cấu hình domain và cổng dịch vụ
* Xem các tính năng bảo mật đang bật
* Theo dõi thời điểm kích hoạt ứng dụng
* Thực hiện các thao tác quản lý ứng dụng

Trang này cung cấp cái nhìn tổng thể về tất cả các ứng dụng đang được WAF bảo vệ.

***

#### Thông tin hiển thị trong danh sách ứng dụng

Mỗi ứng dụng trong danh sách hiển thị các thông tin sau:

* Tên ứng dụng
* Chế độ bảo vệ
* Trạng thái hoạt động
* Domain trỏ về WAF
* Cổng dịch vụ
* Các module bảo mật đang bật
* Thời điểm kích hoạt

***

#### Yêu cầu DNS

WAF chỉ có hiệu lực sau khi hoàn tất cấu hình DNS. Tất cả domain trong ứng dụng phải được trỏ DNS về hệ thống vWAF theo **một trong hai phương thức** dưới đây:

* **CNAME** _(khuyến nghị)_ — trỏ CNAME Record của domain dịch vụ về domain DNS riêng do GreenNode cấp (dạng `<mã-định-tuyến>.waf.greennode.vn`). Với phương thức này, GreenNode có thể chủ động điều chỉnh định tuyến lưu lượng sang zone vWAF phù hợp mà không yêu cầu Quý Khách hàng thay đổi cấu hình DNS.
* **A Record** — trỏ A Record của domain dịch vụ trực tiếp về địa chỉ IP public `103.7.174.2`. Áp dụng cho cả Root Domain (Apex) và các DNS Provider không hỗ trợ CNAME tại Root Domain.

Domain định tuyến CNAME của tài khoản được hiển thị tại khung thông báo phía trên danh sách ứng dụng trên màn hình **Ứng dụng**.

Xem hướng dẫn chi tiết tại Cấu hình DNS cho dịch vụ vWAF.

***

### Thêm ứng dụng

Màn hình **Add Application** cho phép người dùng đăng ký một website hoặc dịch vụ mới để được bảo vệ bởi WAF.

Trước khi kích hoạt bảo vệ WAF, người dùng cần cấu hình:

* Thông tin ứng dụng
* Domain
* Cổng dịch vụ
* Chứng chỉ SSL
* Phương thức truy cập
* Máy chủ backend

***

### Thông tin ứng dụng

#### Tên ứng dụng

Nhập tên mô tả cho ứng dụng.

Tên này chỉ dùng để nhận diện trong dashboard của WAF và không ảnh hưởng đến việc xử lý lưu lượng.

***

#### Domain

Nhập tên miền gốc cần được WAF bảo vệ, không bao gồm http/https hoặc ký tự đại diện (\*) — ví dụ: `example.com`.

* Chọn ô bên dưới nếu bạn muốn bảo vệ thêm tên miền con `www` (ví dụ: `www.example.com`).

***

#### Cổng dịch vụ

Khai báo các cổng dịch vụ mà ứng dụng sử dụng.

Các cổng phổ biến:

* **80** cho HTTP
* **443** cho HTTPS

Mỗi cổng có thể cấu hình HTTP hoặc HTTPS.\
Có thể thêm hoặc xóa cổng khi cần.

***

#### Chứng chỉ SSL

Chọn chứng chỉ SSL dùng cho các kết nối HTTPS.

Các tùy chọn bao gồm:

* Chứng chỉ đã upload
* Chứng chỉ miễn phí do hệ thống cấp
* Chứng chỉ đã từng sử dụng trong tài khoản

Trường này **bắt buộc** nếu có bất kỳ cổng nào được cấu hình HTTPS.

***

#### Phương thức truy cập

**Reverse Proxy**

Đây là chế độ mặc định và **được khuyến nghị sử dụng**.

Ở chế độ **Reverse Proxy**, WAF đứng phía trước máy chủ backend, kiểm tra và lọc toàn bộ lưu lượng trước khi chuyển tiếp request hợp lệ.

Chế độ này hỗ trợ đầy đủ các tính năng bảo mật, bao gồm:

* Phát hiện và chặn tấn công
* Giảm thiểu HTTP flood
* Kiểm soát truy cập theo IP và vị trí địa lý
* Giới hạn tốc độ
* Phát hiện và quản lý bot

***

#### Máy chủ backend (Upstream Servers)

Khai báo các máy chủ backend nơi WAF sẽ chuyển tiếp lưu lượng hợp lệ.

* Mỗi upstream phải là IP hoặc domain
* Không hỗ trợ URL có path

**Ví dụ hợp lệ:**

* `http://192.168.1.10:8080`
* `http://backend.example.com:8080`

Có thể thêm nhiều upstream để dự phòng hoặc cân bằng tải.
