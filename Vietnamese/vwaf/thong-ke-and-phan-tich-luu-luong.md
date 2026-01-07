# Thống kê & Phân tích lưu lượng

## Hướng dẫn sử dụng Thống kê lưu lượng WAF

Trang **Thống kê lưu lượng** cung cấp cái nhìn tổng quan về toàn bộ lưu lượng HTTP/HTTPS đi qua hệ thống Web Application Firewall (WAF) trong một khoảng thời gian xác định.\
Chức năng này giúp người dùng theo dõi lưu lượng truy cập, tình trạng bảo mật, tỷ lệ lỗi và hành vi của client.

***

### Tổng quan

Chức năng Thống kê lưu lượng cho phép bạn:

* Theo dõi tổng số request và request bị chặn
* Phân tích tỷ lệ lỗi 4xx và 5xx
* Xác định nguồn truy cập và đặc điểm client
* Phát hiện sớm các bất thường hoặc dấu hiệu tấn công
* Đánh giá hiệu quả của các rule bảo vệ WAF

***

### Bộ lọc & Phạm vi hiển thị

#### Chọn ứng dụng – **Tất cả ứng dụng**

Cho phép lọc dữ liệu thống kê theo:

* Một ứng dụng cụ thể đang được WAF bảo vệ, hoặc
* **Tất cả ứng dụng** để xem dữ liệu tổng hợp của toàn bộ hệ thống

Tính năng này đặc biệt hữu ích khi quản lý nhiều ứng dụng trên cùng một WAF.

#### Chọn khoảng thời gian – **1 ngày**

Cho phép lọc dữ liệu theo các mốc thời gian, ví dụ:

* 1 ngày
* 7 ngày
* 1 tháng

Toàn bộ chỉ số và biểu đồ sẽ được cập nhật tương ứng với khoảng thời gian được chọn.

***

### Phân tích lưu lượng

#### Các chỉ số chính

| Chỉ số         | Mô tả                                                      |
| -------------- | ---------------------------------------------------------- |
| **Requests**   | Tổng số request HTTP/HTTPS được WAF xử lý                  |
| **Views**      | Số lượt xem trang được tính từ các request hợp lệ          |
| **Visitors**   | Số lượng người truy cập duy nhất (dựa trên cookie hoặc IP) |
| **Unique IP**  | Số lượng địa chỉ IP khác nhau truy cập hệ thống            |
| **Blocked**    | Số request bị WAF chặn                                     |
| **IP Address** | Số IP đã phát sinh request bị chặn                         |

Các chỉ số này cung cấp cái nhìn tổng thể về lưu lượng và mức độ hoạt động bảo mật.

***

### Thống kê lỗi & chặn

#### Lỗi 4xx

Số request trả về lỗi phía client, ví dụ:

* 403 Forbidden
* 404 Not Found

#### Tỷ lệ lỗi (Error Rate)

Tỷ lệ phần trăm request lỗi 4xx so với tổng số request.

#### 4xx bị chặn

Các request bị WAF chủ động chặn và trả về mã lỗi 4xx (thường là 403).

#### Tỷ lệ bị chặn (Blocked Rate)

Tỷ lệ phần trăm request bị WAF chặn trên tổng số request.

#### Lỗi 5xx

Số request gặp lỗi phía server, bao gồm:

* 500 Internal Server Error
* 502 Bad Gateway
* 504 Gateway Timeout

#### Tỷ lệ lỗi 5xx

Tỷ lệ phần trăm lỗi server trên tổng request.\
Tỷ lệ cao thường cho thấy vấn đề ở backend ứng dụng hoặc hạ tầng, không phải do WAF chặn.

***

### Query Per Second (QPS)

Hiển thị số lượng request được xử lý mỗi giây.

**Mục đích sử dụng:**

* Phát hiện đột biến lưu lượng
* Nhận diện nguy cơ DDoS hoặc bot traffic
* Theo dõi xu hướng tải hệ thống theo thời gian

***

### Trạng thái request (Requests)

Hiển thị số lượng request theo thời gian.

**Hữu ích trong việc:**

* Phát hiện lưu lượng tăng đột biến bất thường
* Phân tích hành vi người dùng
* Nhận diện truy cập tự động hoặc script

***

### Trạng thái chặn (Blocked)

Hiển thị số lượng request bị WAF chặn theo thời gian.

**Hữu ích trong việc:**

* Phát hiện các đợt tấn công
* Đánh giá hiệu quả của các rule bảo mật
* Xác định thời điểm hệ thống bảo vệ hoạt động mạnh nhất

***

### Vị trí địa lý (Geo Location)

Hiển thị nguồn gốc địa lý của các request, phân theo quốc gia hoặc khu vực.

**Lợi ích:**

* Phân tích phân bố lưu lượng theo vùng
* Phát hiện truy cập bất thường từ các khu vực không mong đợi
* Hỗ trợ xây dựng chính sách chặn theo địa lý

***

### Thông tin client – User Agent

Hiển thị thông tin client truy cập, bao gồm:

* Hệ điều hành (Windows, Linux, macOS)
* Trình duyệt (Chrome, Firefox, Safari)
* Công cụ hoặc client tự động (curl, wget, bot tùy chỉnh)

Thông tin này giúp phân biệt giữa người dùng thật và các truy cập tự động hoặc độc hại.

***

### Trạng thái phản hồi (Response Status)

Phân loại request theo nhóm mã phản hồi HTTP:

* **2xx** – Thành công
* **3xx** – Chuyển hướng
* **4xx** – Lỗi phía client
* **5xx** – Lỗi phía server

Phần này giúp đánh giá nhanh tình trạng hoạt động của ứng dụng và kết quả xử lý request.

***

### Tổng kết

Trang **Thống kê lưu lượng** là bảng điều khiển giám sát trung tâm cho các ứng dụng được bảo vệ bởi WAF.\
Thông qua việc phân tích lưu lượng, lỗi, request bị chặn và hành vi client, người dùng có thể:

* Theo dõi tình trạng hoạt động của ứng dụng
* Phát hiện và phản ứng sớm với các cuộc tấn công
* Tối ưu cấu hình rule WAF
* Nâng cao khả năng quan sát và bảo mật hệ thống
