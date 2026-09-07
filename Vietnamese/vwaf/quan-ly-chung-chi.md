# Quản lý chứng chỉ

### Tổng quan

Phần **Certificates** cho phép bạn quản lý toàn bộ chứng chỉ SSL/TLS được sử dụng bởi các ứng dụng được WAF bảo vệ.

Chứng chỉ giúp đảm bảo kết nối HTTPS an toàn, bảo vệ tính toàn vẹn dữ liệu và ngăn chặn việc nghe lén hoặc chỉnh sửa lưu lượng.

Module này cung cấp một nơi tập trung để:

* Theo dõi trạng thái chứng chỉ
* Upload chứng chỉ tùy chỉnh
* Gán chứng chỉ cho ứng dụng
* Gia hạn hoặc thay thế chứng chỉ sắp hết hạn

> **⚠️ Thông báo thay đổi:** GreenNode **đã ngừng cấp chứng chỉ SSL/TLS miễn phí (Let's Encrypt)**. Tùy chọn _Lấy chứng chỉ miễn phí_ không còn khả dụng khi thêm chứng chỉ mới.
>
> * Với các ứng dụng mới, Quý Khách hàng vui lòng **upload chứng chỉ SSL/TLS của riêng mình**.
> * Các chứng chỉ miễn phí **đã được cấp trước đó vẫn tiếp tục hoạt động**, vẫn hiển thị trong danh sách với `Type = FREE` và vẫn có thể gán cho ứng dụng.
> * GreenNode khuyến nghị Quý Khách hàng **chủ động chuẩn bị chứng chỉ thay thế trước ngày hết hạn** của các chứng chỉ miễn phí đang dùng, để tránh gián đoạn dịch vụ HTTPS. Theo dõi cột **Expire On** trong danh sách chứng chỉ.

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

#### Chứng chỉ miễn phí _(đã ngừng cấp mới)_

> Trước đây WAF hỗ trợ tự động cấp chứng chỉ miễn phí qua Let's Encrypt. **Tính năng này đã ngừng cung cấp** — Quý Khách hàng không thể yêu cầu cấp chứng chỉ miễn phí mới.
>
> * Các chứng chỉ đã cấp trước đó vẫn hiển thị trong danh sách với `Type = FREE` và vẫn sử dụng được cho ứng dụng.
> * Khi chứng chỉ loại này đến hạn, Quý Khách hàng cần **upload chứng chỉ thay thế** (xem mục _Chứng chỉ upload_).

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

Xác định chứng chỉ là `UPLOADED` (chứng chỉ do Quý Khách hàng upload) hay `FREE` (chứng chỉ miễn phí được cấp trước khi tính năng này ngừng cung cấp). Chứng chỉ mới luôn có loại `UPLOADED`.

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

Trang Add Certificate cho phép thêm chứng chỉ SSL/TLS mới cho WAF bằng cách **upload chứng chỉ của riêng Quý Khách hàng**.

Tùy chọn yêu cầu WAF cấp chứng chỉ miễn phí tự động đã ngừng cung cấp.

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

### Các trường trong form Add Certificate

#### Domain (bắt buộc)

Nhập một hoặc nhiều domain để cấp hoặc upload chứng chỉ.

* Có thể phân tách domain bằng dấu cách hoặc xuống dòng
* Hỗ trợ wildcard (`*`)
