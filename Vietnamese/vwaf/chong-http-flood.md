# Chống HTTP Flood

### Tổng quan

Chức năng **Rate Limiting** giúp bảo vệ ứng dụng khỏi lưu lượng truy cập quá mức hoặc mang tính lạm dụng bằng cách giới hạn số lượng request mà một client có thể gửi trong một khoảng thời gian xác định.

Đây là cơ chế phòng thủ quan trọng để chống lại:

* Tấn công HTTP Flood
* Tấn công brute-force
* Hành vi scan tự động
* Các đợt tăng lưu lượng bất thường

Trang **Rate Limiting** cung cấp khả năng theo dõi các client vượt quá ngưỡng cấu hình và hành động mà WAF đã áp dụng.

***

### Tổng quan trang Rate Limiting

Trang này hiển thị danh sách tất cả các địa chỉ IP đã kích hoạt rule giới hạn tần suất trên các ứng dụng được bảo vệ.

Với mỗi IP, người dùng có thể xem:

* Địa chỉ IP và vị trí địa lý
* Ứng dụng bị tác động
* Thông tin rule đã kích hoạt (số request và khoảng thời gian)
* Thời gian bị chặn
* Tổng số request bị chặn
* Thời điểm bắt đầu sự kiện
* Trạng thái hiện tại (Blocked / Unblocked)

Thông tin này giúp nhanh chóng xác định client lạm dụng và đánh giá hiệu quả của các rule giới hạn tần suất.

***

### Bộ lọc

Để thu hẹp danh sách sự kiện Rate Limiting, hệ thống hỗ trợ các bộ lọc sau:

#### IP Address

Chỉ hiển thị các sự kiện phát sinh từ một IP cụ thể.

#### Application

Lọc theo ứng dụng được bảo vệ.

#### Start At / End At

Lọc sự kiện theo khoảng thời gian.

#### Clear Filters

Xóa toàn bộ bộ lọc và quay về danh sách đầy đủ.

Các bộ lọc này giúp việc điều tra trở nên dễ dàng hơn khi có số lượng lớn IP bị giới hạn.

***

### Chi tiết bảng Rate Limiting

Mỗi dòng trong bảng hiển thị các thông tin chẩn đoán chính:

#### IP Address

Địa chỉ IP của client vượt quá ngưỡng giới hạn.\
Thông tin quốc gia được hiển thị để tham khảo ngữ cảnh địa lý.

#### Application

Ứng dụng đang nhận lưu lượng truy cập quá mức từ IP đó.

#### Detail

Tóm tắt rule đã kích hoạt, ví dụ:

> “2 requests trong 10 giây – Basic Access Limit được kích hoạt”

Thông tin này cho biết:

* Số request đã nhận
* Khoảng thời gian tính toán
* Rule giới hạn nào đã chặn lưu lượng

#### Blocked

Tổng số request bị chặn trong suốt sự kiện.

#### Start At

Thời điểm bắt đầu áp dụng giới hạn tần suất.

#### State

Trạng thái hiện tại của IP:

* **Blocked** – IP vẫn đang bị áp dụng giới hạn
* **Unblocked** – thời gian phạt đã kết thúc

***

### Thao tác hàng loạt

Trang Rate Limiting cho phép quản trị viên thực hiện các thao tác hàng loạt.

#### Unblock All

Gỡ bỏ ngay lập tức tất cả các IP đang bị chặn bởi Rate Limiting.

Tính năng này hữu ích trong các trường hợp:

* Điều chỉnh hoặc cập nhật ngưỡng giới hạn
* Kiểm thử rule và hành vi lưu lượng
* Reset trạng thái sau bảo trì hoặc sự cố an ninh
