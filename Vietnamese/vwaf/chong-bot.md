# Chống Bot

### Tổng quan

Chức năng **Anti-Bot** giúp phát hiện và giảm thiểu các loại lưu lượng tự động có thể gây hại cho ứng dụng, như crawler, scanner, bot brute-force hoặc các client chạy script.

Hệ thống cung cấp các cơ chế giám sát và xác thực nhằm phân biệt giữa **người dùng thật** và **các công cụ tự động**.

Trang **Anti-Bot** hiển thị tất cả các địa chỉ IP đã kích hoạt cơ chế phát hiện bot trên các ứng dụng được bảo vệ.

***

### Tổng quan nhật ký Anti-Bot

Trang này hiển thị các sự kiện phát hiện do Anti-Bot engine tạo ra.

Mỗi dòng đại diện cho hoạt động có dấu hiệu bot từ một địa chỉ IP truy cập vào một ứng dụng cụ thể.

Với mỗi sự kiện, hệ thống hiển thị:

* Địa chỉ IP
* Quốc gia nguồn
* Ứng dụng bị truy cập
* Thông tin phát hiện (Hits / Verified)
* Thời gian diễn ra hoạt động bot
* Thời điểm bắt đầu phát hiện

Thông tin này giúp quản trị viên nhanh chóng nhận diện các mẫu lưu lượng tự động đáng ngờ.

***

### Chi tiết phát hiện

Mỗi sự kiện Anti-Bot bao gồm hai chỉ số quan trọng:

#### Hits

Số lần địa chỉ IP kích hoạt cơ chế kiểm tra Anti-Bot.

Chỉ số Hits tăng khi hành vi client có dấu hiệu tự động, ví dụ:

* Gửi quá nhiều request trong thời gian ngắn
* Truy cập các endpoint nhạy cảm hoặc bất thường
* Thiếu fingerprint trình duyệt
* Header HTTP bất thường hoặc không hợp lệ

***

#### Verified

Số lần hệ thống Anti-Bot xác minh thành công rằng client là **người dùng thật**, không phải bot.

Các phương thức xác minh có thể bao gồm:

* Kiểm tra thử thách trình duyệt
* Phân tích hành vi
* Xác thực fingerprint

Nếu số **Verified** thấp hơn nhiều so với **Hits**, lưu lượng đó nhiều khả năng là bot.

***

### Bộ lọc

Người dùng có thể lọc các sự kiện Anti-Bot theo:

#### IP Address

Lọc theo một địa chỉ IP cụ thể.

#### Application

Chỉ hiển thị hoạt động bot trên một ứng dụng được chọn.

#### Start At / End At

Giới hạn kết quả theo khoảng thời gian.

#### Clear Filters

Xóa toàn bộ điều kiện lọc và quay về danh sách đầy đủ.

Các bộ lọc này giúp việc điều tra lưu lượng bot trở nên nhanh chóng và hiệu quả hơn.

***

### Giải thích các cột trong bảng

#### IP Address

Địa chỉ IP phát sinh hành vi giống bot.\
Thông tin vị trí địa lý được hiển thị để hỗ trợ xác định nguồn truy cập đáng ngờ.

***

#### Application

Ứng dụng mà IP cố gắng truy cập trong quá trình phát hiện bot.

***

#### Detail

Hiển thị:

* Tổng số lần phát hiện bot (**Hits**)
* Tổng số lần xác minh người dùng thật (**Verified**)

Giúp đánh giá nhanh mức độ tin cậy của lưu lượng truy cập.

***

#### Duration

Khoảng thời gian mà sự kiện Anti-Bot diễn ra.

***

#### Start At

Thời điểm hệ thống Anti-Bot lần đầu phát hiện hoạt động tự động đáng ngờ.
