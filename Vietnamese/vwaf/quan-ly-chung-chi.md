# Quản lý chứng chỉ

### Tổng quan

Phần **Certificates** cho phép bạn quản lý toàn bộ chứng chỉ SSL/TLS được sử dụng bởi các ứng dụng được WAF bảo vệ.

Chứng chỉ giúp đảm bảo kết nối HTTPS an toàn, bảo vệ tính toàn vẹn dữ liệu và ngăn chặn việc nghe lén hoặc chỉnh sửa lưu lượng.

Module này cung cấp một nơi tập trung để:

* Theo dõi trạng thái chứng chỉ
* Cấp chứng chỉ miễn phí
* Upload chứng chỉ tùy chỉnh
* Gán chứng chỉ cho ứng dụng
* Gia hạn hoặc thay thế chứng chỉ sắp hết hạn

***

### Tổng quan danh sách chứng chỉ

Trang danh sách hiển thị tất cả chứng chỉ gắn với tài khoản.

Mỗi chứng chỉ bao gồm các thông tin:

* Certificate ID
* Loại chứng chỉ (Free hoặc Uploaded)
* Domain
* Ứng dụng đang sử dụng
* Đơn vị phát hành
* Ngày hết hạn
* Thao tác quản lý

Trang này giúp quản trị viên nhanh chóng nắm được tình trạng SSL/TLS của toàn bộ hệ thống.

***

### Loại chứng chỉ

#### Chứng chỉ miễn phí (Tự động cấp)

Chứng chỉ miễn phí được WAF tự động cấp thông qua **Let’s Encrypt**, sử dụng phương thức xác thực **HTTP-01**.

Đặc điểm chính:

* Miễn phí
* Tự động gia hạn **trước 30 ngày khi hết hạn**
* Yêu cầu domain trỏ DNS A về IP public của WAF
* Không cần thao tác thủ công với key hoặc file chứng chỉ

***

#### Chứng chỉ upload

Cho phép người dùng upload chứng chỉ SSL/TLS của riêng mình.

Phù hợp với các trường hợp:

* CA nội bộ hoặc CA doanh nghiệp
* Chứng chỉ EV
* Chứng chỉ wildcard
* Chứng chỉ đa domain

Khi upload, bạn cần cung cấp:

* Private key
* Chuỗi chứng chỉ (định dạng PEM)

***

### Giải thích các cột trong danh sách chứng chỉ

#### ID

Mã định danh duy nhất của chứng chỉ.

#### Type

Xác định chứng chỉ là **FREE** hay **UPLOADED**.

#### Domain

Danh sách domain được chứng chỉ bảo vệ.

#### Applications

Các ứng dụng WAF đang sử dụng chứng chỉ này.

#### Issued By

Đơn vị hoặc hệ thống phát hành chứng chỉ.

#### Expire On

Ngày và giờ hết hạn của chứng chỉ.

Các chứng chỉ sắp hết hạn cần được gia hạn kịp thời để tránh gián đoạn dịch vụ.

#### Action

Các thao tác quản lý bao gồm:

* View
* Renew / Replace
* Delete

***

### Thêm chứng chỉ

Trang **Add Certificate** cho phép thêm chứng chỉ SSL/TLS mới cho WAF.

Bạn có thể:

* Upload chứng chỉ của riêng mình
* Hoặc yêu cầu WAF cấp chứng chỉ miễn phí tự động

***

### Chọn loại chứng chỉ

#### Upload chứng chỉ

Chọn tùy chọn này để upload chứng chỉ SSL của bạn.

Cần cung cấp:

* File private key
* File chứng chỉ
* (Tùy chọn) Chuỗi chứng chỉ trung gian

Định dạng hỗ trợ: **PEM**

***

#### Lấy chứng chỉ miễn phí

Chọn tùy chọn này để WAF tự động cấp chứng chỉ miễn phí thông qua **Let’s Encrypt**.

***

### ⚠️ Lưu ý quan trọng – Trước khi lấy chứng chỉ miễn phí

**Trước khi yêu cầu cấp chứng chỉ miễn phí cho một domain, bạn BẮT BUỘC phải thực hiện các bước sau:**

* **Tạo application trước trên WAF với chính domain đó**.
* Cấu hình application sử dụng **cổng 80 (HTTP)**.
* **KHÔNG gán bất kỳ chứng chỉ SSL nào** cho application tại thời điểm này.
* Đảm bảo domain đã được cấu hình **DNS A record trỏ về IP public của WAF: `103.7.174.2`**.
* Chờ DNS được cập nhật hoàn toàn.

Các bước trên là **bắt buộc** để hệ thống thực hiện xác thực **Let’s Encrypt HTTP-01**.\
Nếu application chưa được tạo với **port 80 và không có cert**, việc cấp chứng chỉ miễn phí sẽ **không thành công**.

***

### Các trường trong form Add Certificate

#### Domain (bắt buộc)

Nhập một hoặc nhiều domain để cấp hoặc upload chứng chỉ.

* Có thể phân tách domain bằng dấu cách hoặc xuống dòng
* Hỗ trợ wildcard (`*`) cho chứng chỉ upload

***

#### Email Address

_(Bắt buộc với chứng chỉ miễn phí)_

Được sử dụng để:

* Nhận thông báo từ Let’s Encrypt
* Xác thực quyền sở hữu domain

***

### Yêu cầu xác thực (Chứng chỉ miễn phí)

Các yêu cầu bắt buộc trong quá trình cấp chứng chỉ:

* Tất cả domain phải trỏ DNS A về IP public của WAF: `103.7.174.2`
* Domain phải truy cập được từ Internet
* WAF thực hiện xác thực **HTTP-01**
* Chứng chỉ được gia hạn tự động trước khi hết hạn

Nếu DNS hoặc kết nối không chính xác, chứng chỉ sẽ không thể được cấp.
