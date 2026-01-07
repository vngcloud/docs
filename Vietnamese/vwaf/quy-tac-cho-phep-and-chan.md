# Quy tắc Cho phép & Chặn

### Tổng quan

Phần **Allow & Deny Rules** cho phép quản trị viên định nghĩa các rule kiểm soát truy cập tùy chỉnh cho ứng dụng.

Các rule này cho phép hoặc chặn IP, dải IP hoặc mẫu lưu lượng **trước khi request đi vào ứng dụng**.

Module này bao gồm:

* **Rules** – nơi tạo và quản lý các rule Allow / Deny
* **Events & Logs** – nơi ghi nhận và hiển thị các hoạt động do rule kích hoạt

***

### Quản lý Rule

Trang **Rules** hiển thị toàn bộ các rule Allow và Deny do người dùng cấu hình.

Mỗi rule bao gồm:

* Tên rule
* Ứng dụng áp dụng
* Loại rule (Allow hoặc Deny)
* Số lần match trong ngày
* Thời điểm tạo rule
* Trạng thái rule (Bật / Tắt)

Đây là khu vực trung tâm để quản lý các rule kiểm soát truy cập.

***

### Loại Rule

#### Rule Allow (Cho phép)

**Allow Rule** cho phép các request thỏa điều kiện được cấu hình.

Các trường hợp sử dụng phổ biến:

* Whitelist IP tin cậy
* Cho phép mạng nội bộ
* Bỏ qua kiểm tra WAF cho một số nguồn truy cập nhất định

***

#### Rule Deny (Chặn)

**Deny Rule** chặn các request thỏa điều kiện được cấu hình.

Các trường hợp sử dụng phổ biến:

* Chặn IP độc hại đã biết
* Ngăn chặn bot hoặc scanner lạm dụng
* Hạn chế truy cập từ khu vực hoặc mạng không mong muốn

***

### Lọc Rule

Menu lọc cho phép hiển thị nhanh:

* Tất cả rule
* Chỉ rule Allow
* Chỉ rule Deny

Giúp việc quản lý số lượng lớn rule trở nên dễ dàng hơn.

***

### Thao tác với Rule

Mỗi rule hỗ trợ các thao tác:

* **Enable / Disable** – bật hoặc tắt rule mà không cần xóa
* **Edit** – chỉnh sửa cấu hình rule
* **Delete** – xóa vĩnh viễn rule

Mọi thay đổi sẽ có hiệu lực **trong vòng 10 giây đến 1 phút** sau khi được áp dụng.

***

### Events & Logs

Phần **Events & Logs** hiển thị các hoạt động được kích hoạt bởi rule Allow hoặc Deny.

Bao gồm hai chế độ hiển thị:

* **Events** – dữ liệu tổng hợp theo IP nguồn
* **Logs** – chi tiết từng request

***

### Events (Sự kiện)

Tab **Events** hiển thị thông tin tổng hợp của các request match rule.

Mỗi dòng bao gồm:

* Địa chỉ IP và quốc gia
* Ứng dụng bị tác động
* Số lần rule được kích hoạt
* Thời gian diễn ra
* Thời điểm bắt đầu sự kiện

Giúp người dùng:

* Phát hiện nguồn truy cập bất thường
* Theo dõi tần suất rule hoạt động
* Nhận diện các đối tượng vi phạm lặp lại

Có thể lọc theo:

* IP
* Domain
* Cổng
* Khoảng thời gian

***

### Logs (Nhật ký)

Tab **Logs** hiển thị từng request cụ thể match rule Allow hoặc Deny.

Thông tin bao gồm:

* Hành động (Cho phép / Chặn)
* URL request
* Loại rule (Allow / Deny)
* IP nguồn
* Thời gian
* Nút xem chi tiết

Chế độ này dùng để kiểm tra chi tiết hành vi rule và lưu lượng bị ảnh hưởng.

Bộ lọc hỗ trợ:

* Hành động (Allowed / Blocked / Tất cả)
* Cổng
* IP
* Domain
* Loại rule
* Khoảng thời gian

***

### Events & Logs – Chi tiết

Nhấn vào nút **Detail** để xem đầy đủ thông tin của một sự kiện do rule kích hoạt.

Màn hình chi tiết hiển thị:

* URL đầy đủ
* Hành động của WAF (Cho phép hoặc Chặn)
* IP và vị trí địa lý
* Module phát hiện (Allow Rule / Deny Rule)
* Tên rule
* Thời gian
* Event ID

Bên dưới là **HTTP request thô**, bao gồm:

* Method và path
* Host header
* User-Agent
* Các header khác

Chế độ này phục vụ:

* Xác minh rule hoạt động đúng
* Điều tra quyết định kiểm soát truy cập
* Thu thập bằng chứng cho audit hoặc sự cố an ninh
