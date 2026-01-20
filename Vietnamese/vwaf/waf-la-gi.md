# WAF là gì?

## WAF là gì?

**Web Application Firewall (WAF)** là một giải pháp bảo mật được thiết kế để bảo vệ **ứng dụng web và API** bằng cách giám sát, phân tích, lọc và chặn các lưu lượng HTTP/HTTPS độc hại trước khi chúng truy cập vào máy chủ ứng dụng (origin server).

Khác với các firewall truyền thống hoạt động ở tầng mạng hoặc tầng giao vận (Layer 3 / Layer 4), **WAF hoạt động ở tầng ứng dụng (Layer 7)** và có khả năng hiểu các đặc thù của giao thức web, cấu trúc request và hành vi truy cập.

**Tóm lại:**\
👉 **WAF được đặt phía trước ứng dụng web và đóng vai trò như một cổng bảo mật (security gatekeeper).**

***

## Vì sao bạn cần WAF?

Các ứng dụng web hiện đại phải đối mặt với nhiều mối đe dọa bảo mật, bao gồm:

* **SQL Injection (SQLi)**
* **Cross-Site Scripting (XSS)**
* **Remote Code Execution (RCE)**
* **File Inclusion (LFI/RFI)**
* **Bot abuse**, scraping, credential stuffing
* **Tấn công DDoS tầng ứng dụng**

WAF giúp bạn:

* Bảo vệ ứng dụng **mà không cần thay đổi mã nguồn**
* Giảm thiểu rủi ro bảo mật và nguy cơ rò rỉ dữ liệu
* Đáp ứng các yêu cầu tuân thủ và tiêu chuẩn bảo mật (ví dụ: **PCI-DSS**, quy định an toàn thông tin)
* Nâng cao tính **ổn định**, **khả dụng** và **độ tin cậy** của ứng dụng

***

## WAF hoạt động như thế nào?

**Luồng xử lý lưu lượng điển hình:**

```
Client  →  WAF  →  Ứng dụng Web (Origin Server)
```

Quy trình xử lý request:

1. Client gửi request HTTP/HTTPS
2. WAF tiếp nhận và kiểm tra request theo thời gian thực
3. Các engine phát hiện và bộ rule bảo mật phân tích nội dung request
4. Dựa trên kết quả phân tích, WAF sẽ:
   * Cho phép request đi qua
   * Chặn request
   * Yêu cầu xác minh (CAPTCHA, challenge)
   * Ghi log phục vụ giám sát và kiểm toán

***

## Các khả năng chính của WAF

### 1. Bảo vệ trước các cuộc tấn công

* Bảo vệ theo **OWASP Top 10**
* Phát hiện tấn công zero-day và các mẫu tấn công chưa xác định (dựa trên hành vi)
* Kiểm tra tính hợp lệ của protocol và request

***

### 2. Kiểm soát truy cập (Access Control)

* Danh sách **cho phép / chặn IP** (IP allowlist / denylist)
* Kiểm soát truy cập theo **vị trí địa lý (Geo-based)**
* Giới hạn tốc độ truy cập (**Rate limiting**) theo IP, URL hoặc hành vi người dùng

***

### 3. Quản lý Bot (Bot Management)

* Phát hiện và giảm thiểu bot độc hại
* Cho phép bot hợp lệ (công cụ tìm kiếm, hệ thống giám sát)
* Bảo vệ trang đăng nhập và API khỏi tấn công brute-force

***

### 4. Giám sát lưu lượng & ghi log

* Log request và tấn công theo thời gian thực
* Thông tin chi tiết về sự kiện bảo mật (rule, IP nguồn, payload, hành động)
* Thống kê lưu lượng và xu hướng truy cập

***

### 5 Rule tùy chỉnh (Custom Rules)

* Tạo rule **Allow / Deny / Monitor**
* So khớp theo URL, method, header, tham số, body
* Thiết lập **độ ưu tiên** và **phạm vi áp dụng** linh hoạt

***

### Tổng kết

WAF là lớp bảo vệ quan trọng giúp ứng dụng web và API an toàn trước các mối đe dọa hiện đại.\
Bằng cách kết hợp **phát hiện thông minh**, **kiểm soát truy cập**, **quản lý bot** và **khả năng quan sát lưu lượng**, WAF giúp doanh nghiệp:

* Tăng cường bảo mật
* Giảm thiểu rủi ro vận hành
* Đảm bảo trải nghiệm người dùng ổn định và an toàn
