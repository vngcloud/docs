# Bắt đầu với FileStorage

Trong phần này, chúng ta sẽ tìm hiểu về cách sử dụng và quản lý dịch vụ FileStorage theo cách cơ bản nhất, từ đó cung cấp cái nhìn tổng quan hơn đến người sử dụng dịch vụ

## Trước khi bắt đầu

* Để bắt đầu sử dụng FileStorage, người dùng cần có ít nhất **một Virtal Private Cloud (VPC)**, tham khảo hướng dẫn [Virtual Private Cloud (VPC)](../../vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc.md).
* Tìm hiểu cách **truy cập VNG Cloud Portal** với Root User Account hoặc IAM User Account, tham khảo hướng dẫn [How to Login into VNG Cloud](../../identity-and-access-management-iam/cac-loai-dinh-danh-iam/tai-khoan-user-accounts/cach-dang-nhap-vao-vng-cloud.md).

## Khởi tạo tài nguyên

### Người dùng gửi yêu cầu sử dụng dịch vụ File Storage

* **Cách 1: Gửi yêu cầu sử dụng dịch vụ thông qua ticket**
  * Bước 1: Chọn dịch vụ File Storage tại trang chủ
    * Tại trang chủ [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/), tại mục **VNG Cloud Service**, chọn **vStorage**, sau đó chọn **File Storage.**
    * Sau đó, người dùng sẽ được điều hướng đến trang gửi ticket (yêu cầu người dùng phải đăng nhập bằng tài khoản VNG, nếu chưa có tài khoản VNG Cloud, mời tham khảo cách 2)
  * Bước 2: Điền thông tin bắt buộc bao gồm
    * Request Category: Hỗ trợ kỹ thuật (Technical Support)
    * Product: Sản phẩm khác (Other)
    * Ticket information (Subject): Hỗ trợ File Storage
    * Description: Tên file storage, VPC, danh sách địa chỉ IP được phép kết nối
* **Cách 2: Gửi yêu cầu sử dụng đến đội ngũ hỗ trợ (Điện thoại, Email) với nội dung**
  * Tiêu đề: Hỗ trợ kỹ thuật File Storage
  * Nội dung: Tên file storage, Dung lượng sử dụng, VPC, danh sách địa chỉ IP được phép kết nối

### VNG Cloud xử lý yêu cầu

* Bước 1: VNG Cloud liên hệ khách hàng để xác nhận, tư vấn, cũng như rõ hơn về nhu cầu sử dụng
* Bước 2: VNG Cloud cung cấp dịch vụ đến khách hàng, bao gồm các thông tin
  * Tên tài nguyên (từ khách hàng cung cấp)
  * Định danh tài nguyên
  * Dung lượng sử dụng (mặc định 1TB)
  * Thông lượng (mặc định 200MB/s)
  * Danh sách địa chỉ IP được phép kết nối đền tài nguyên File Storage (từ khách hàng cung cấp)
  * Thời gian sử dụng dịch vụ (mặc định 1 tháng kể từ khi khởi tạo thành công)
* Bước 3: VNG Cloud Gửi email thông tin tài nguyên vừa cung cấp đến khách hàng

### Người dùng xác nhận

* Bước 1: Người dùng kiểm tra thông tin tài nguyên vừa cung cấp (hướng dẫn trong phần đính kèm)
* Bước 2: Gửi email xác nhận tài nguyên File Storage cung cấp cho người dùng là đúng theo yêu cầu

## Mở rộng tài nguyên

Trong quá trình sử dụng dịch vụ, VNG Cloud hỗ trợ người dùng mở rộng tài nguyên bằng cách mở rộng dung lượng sử dụng và Throughput. Làm theo hướng dẫn dưới đây để yêu cầu hỗ trợ:

**Bước 1: Người dùng gửi yêu cầu mở rộng tài nguyên đến đội ngũ hỗ trợ bằng việc gửi ticket:**

* 1.1: Truy cập đến trang ticket
* 1.2: Điền thông tin bắt buộc bao gồm
  * Request Category: Hỗ trợ kỹ thuật (Technical Support)
  * Product: Sản phẩm khác (Other)
  * Ticket information (Subject): Mở rộng tài nguyên File Storage
  * Description: Định danh tài nguyên, Yêu cầu mở rộng dung lượng đến (TB), Yêu cầu mở rộng thông lượng đến (Mb/s)

**Bước 2: VNG Cloud xử lý yêu cầu mở rộng tài nguyên**

* 2.1: VNG Cloud liên hệ khách hàng để xác nhận yêu cầu sử dụng.
* 2.2: VNG Cloud mở rộng tài nguyên theo yêu cầu từ khách hàng.
* 2.3: VNG Cloud gửi email thông tin tài nguyên vừa cung cấp đến khách hàng.

**Bước 3: Người dùng xác nhận**

* 3.1: Người dùng kiểm tra thông tin tài nguyên vừa cung cấp (hướng dẫn trong phần đính kèm)
* 3.2: Gửi email xác nhận tài nguyên cung cấp cho người dùng là đúng theo yêu cầu.

Lưu ý: Tài nguyên đã được mở rộng sẽ không hỗ trợ giảm xuống (đối với cả dung lượng và thông lượng)

## Gia hạn tài nguyên

Thời gian sử dụng tài nguyên File Storage mặc định là 30 ngày kể từ khi khởi tạo dịch vụ, 3 ngày trước khi dịch vụ hết hạn sử dụng, VNG Cloud sẽ gửi mail đến người dùng để thông báo tình trạng sử dụng tài nguyên, để gia hạn tài nguyên, vui lòng làm theo hướng dẫn bên dưới:

**Bước 1: Người dùng gửi yêu cầu gia hạn tài nguyên đến đội ngũ hỗ trợ bằng việc gửi ticket:**

* 1.1: Truy cập đến trang ticket
* 1.2: Điền thông tin bắt buộc bao gồm
  * Request Category: Hỗ trợ kỹ thuật (Technical Support)
  * Product: Sản phẩm khác (Other)
  * Ticket information (Subject): Gia hạn tài nguyên File Storage
  * Description: Định danh tài nguyên, Thời gian gia hạn (tháng)

**Bước 2: VNG Cloud xử lý yêu cầu mở rộng tài nguyên**

* 2.1:  VNG Cloud gia hạn tài nguyên. Thời gian sử dụng dịch vụ được cập nhật theo công thức sau **Thời hạn mới = Thời gian kết thúc hiện tại + Thời gian gia hạn**
* 2.3: VNG Cloud gửi email thông tin xác nhận đến khách hàng.

## Xóa tài nguyên

Khi không có nhu cầu khởi tạo tài nguyên, để tránh bị phát sinh chi phí không cần thiết, VNG Cloud khuyến nghị người dùng xóa tài nguyên, làm theo hướng dẫn bên dưới để xóa tài nguyên:

**Bước 1: Người dùng gửi yêu cầu xóa tài nguyên đến đội ngũ hỗ trợ bằng việc gửi ticket:**

* 1.1: Truy cập đến trang ticket
* 1.2: Điền thông tin bắt buộc bao gồm
  * Request Category: Hỗ trợ kỹ thuật (Technical Support)
  * Product: Sản phẩm khác (Other)
  * Ticket information (Subject): Xóa tài nguyên File Storage
  * Description: Định danh tài nguyên

**Bước 2: VNG Cloud xử lý yêu cầu xóa tài nguyên**

* 2.1: VNG Cloud liên hệ khách hàng để xác nhận yêu cầu.
* 2.2:  VNG Cloud xóa tài nguyên.
* 2.3: VNG Cloud gửi email xác nhận đến khách hàng.

Lưu ý: Tài nguyên đã xóa (bao gồm dữ liệu được lưu trữ trên tài nguyên) sẽ không thể khôi phục.
