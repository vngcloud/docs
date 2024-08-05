# Khởi tạo tài nguyên

### Người dùng gửi yêu cầu sử dụng dịch vụ File Storage

* **Cách 1: Gửi yêu cầu sử dụng dịch vụ thông qua ticket**
  * Bước 1: Chọn dịch vụ File Storage tại trang chủ
    * Tại trang chủ [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/), tại mục **VNG Cloud Service**, chọn **vStorage**, sau đó chọn **File Storage.**
    * Sau đó, người dùng sẽ được điều hướng đến trang gửi ticket (yêu cầu người dùng phải đăng nhập bằng tài khoản VNG Cloud, nếu chưa có tài khoản VNG Cloud, mời tham khảo cách 2)
  * Bước 2: Điền thông tin bắt buộc bao gồm
    * Request Category: Hỗ trợ kỹ thuật (Technical Support)
    * Product: Sản phẩm khác (Other)
    * Ticket information (Subject): Hỗ trợ File Storage
    * Description: Tên file storage, VPC, danh sách địa chỉ IP được phép kết nối
* **Cách 2: Gửi yêu cầu sử dụng đến đội ngũ hỗ trợ (Điện thoại, Email) với nội dung**
  * Tiêu đề: Hỗ trợ kỹ thuật File Storage
  * Nội dung: Tên file storage, Dung lượng sử dụng, VPC, danh sách địa chỉ IP được phép kết nối

**Lưu ý:**&#x20;

* Để bắt đầu sử dụng FileStorage, người dùng cần có ít nhất **một Virtal Private Cloud (VPC)**, tham khảo hướng dẫn [Virtual Private Cloud (VPC)](../../../vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc.md).
* Tìm hiểu cách **truy cập VNG Cloud Portal** với Root User Account hoặc IAM User Account, tham khảo hướng dẫn [How to Login into VNG Cloud](../../../identity-and-access-management-iam/cac-loai-dinh-danh-iam/tai-khoan-user-accounts/cach-dang-nhap-vao-vng-cloud.md).

### VNG Cloud xử lý yêu cầu

* Bước 1: VNG Cloud liên hệ khách hàng để xác nhận, tư vấn, cũng như rõ hơn về nhu cầu sử dụng
* Bước 2: VNG Cloud cung cấp dịch vụ đến khách hàng, bao gồm các thông tin
  * Tên tài nguyên (từ khách hàng cung cấp)
  * Định danh tài nguyên
  * Dung lượng sử dụng (mặc định 1TB)
  * Thông lượng (mặc định 20Gbps share)
  * Danh sách địa chỉ IP được phép kết nối đền tài nguyên File Storage (từ khách hàng cung cấp)
  * Thời gian sử dụng dịch vụ (mặc định 1 tháng kể từ khi khởi tạo thành công)
* Bước 3: VNG Cloud Gửi email thông tin tài nguyên vừa cung cấp đến khách hàng

### Người dùng xác nhận

* Bước 1: Người dùng kiểm tra thông tin tài nguyên vừa cung cấp (hướng dẫn trong phần đính kèm)
* Bước 2: Gửi email xác nhận tài nguyên File Storage cung cấp cho người dùng là đúng theo yêu cầu
