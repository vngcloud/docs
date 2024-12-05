# Access Management

## Tài khoản truy cập

Trên region HCM04, bạn có thể sử dụng 2 loại tài khoản để truy cập vào vStorage. Chi tiết 2 loại này bao gồm:

* **Root user account:** Là tài khoản [khởi tạo đầu tiên](https://register.vngcloud.vn/signup) để truy cập vào VNG Cloud với đầy đủ quyền truy cập vào tất cả dịch vụ tài nguyên trên VNG Cloud.
* **S3 key:** Là cặp s3 key có access key và secret key được vStorage tích hợp để có tính tương thích với các client tool của S3 như s3cmd, s3 SDK,...

### Root user account

**Khởi tạo tài khoản người dùng Root (Root User Account)**

Để khởi tạo tài khoản người dùng Root, bạn vui lòng đăng ký tài khoản tại trang đăng ký [https://register.vngcloud.vn/signup](https://register.vngcloud.vn/signup).

Sau khi khởi tạo tài khoản người dùng Root, bạn thu thập thông tin sau để truy cập và làm việc với tài nguyên sử dụng tài khoản người dùng Root:

* Địa chỉ email được sử dụng để tạo tài khoản người dùng Root.
* Mật khẩu cho của tài khoản người dùng Root.

Để thực hiện đăng nhập sử dụng vStorage với tài khoản Root, hãy xem thêm tại [Truy cập tài nguyên sử dụng tài khoản người dùng Root](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-truy-cap-tai-nguyen-vstorage/truy-cap-tai-nguyen-su-dung-tai-khoan-nguoi-dung-root).

***

**Hủy tài khoản người dùng Root (Root User Account)**

Để hủy tài khoanr Root, bạn cần liên hệ với chúng tôi thông qua việc tạo một ticket yêu cầu hủy tài khoản. Chi tiết xem thêm tại [Hướng dẫn hủy tài khoản](https://docs.vngcloud.vn/vng-cloud-document/v/vn/huong-dan-su-dung-tai-khoan/huong-dan-huy-tai-khoan).

### S3 key

Để khởi tạo S3 key, làm theo hướng dẫn bên dưới:

1. Đăng nhập vào [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).
2. Chọn **Region HCM04.**
3. Chọn biểu tượng <img src="../../../.gitbook/assets/image%20(581).png" alt="" data-size="line"> tại project mà bạn vừa khởi tạo sau đó chọn mục S3 key.
4. Tại mục S3 key, chọn **Generate S3 key**.
5. Chọn **Copy** hoặc **Download** để tải xuống thông tin Access Key/Secret Key mà bạn vừa khởi tạo.

<figure><img src="../../../.gitbook/assets/image%20(582).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image%20(583).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Chú ý:**

* Sau khi nhấn tạo S3 key, bạn cần **lưu lại cặp Access Key/Secret Key** để sử dụng, nếu bạn không lưu trữ ngay lúc này thì sau đó không thể lấy được Secret Key của Access Key này.
{% endhint %}

## Quản lý truy cập

Trên region HCM04, chúng tôi cung cấp cho bạn các tính năng phân quyền truy cập riêng lẻ tới từng bucket hoặc object được mô tả qua sơ đồ bên dưới. Chi tiết bao gồm:

<details>

<summary>Chuyển chế độ công khai bucket</summary>

Bạn có thể chuyển chế độ của bucket từ riêng tư thành công khai để cho phép bất kỳ ai cũng có thể truy cập vào bucket để xem, tải xuống, tải lên tất cả tệp tin, object thuộc bucket được công khai. Để biết thêm thông tin, hãy xem tại [Làm việc với bucket](cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/)

</details>

<details>

<summary>Chuyển chế độ riêng tư container</summary>

Bạn có thể chuyển chế độ của bucket từ công khai thành riêng tư để dừng việc chia sẻ công khai bucket trên môi trường điện toán đám mây. Bạn sẽ không thể truy cập vào bucket thông qua đường dẫn URL mà cần chứng thực quyền truy cập. Để biết thêm thông tin, hãy xem tại [Làm việc với bucket](cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/)

</details>

<details>

<summary>Phân quyền truy cập ACLs container</summary>

Bạn có thể cấp quyền Đọc, Ghi hoặc Đọc và Ghi cho 1 hoặc tất cả Root user khác. (Root user được cấp quyền truy cập qua ACLS phải là tài khoản được cấp quyền trên hệ thống VNG Cloud của chúng tôi). Để biết thêm thông tin, hãy xem tại [Làm việc với bucket](cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/)

</details>

<details>

<summary>Chia sẻ tài nguyên CORS</summary>

Bạn có thể cho phép một website truy cập vào tài nguyên trên container. Để biết thêm thông tin, hãy xem tại [Làm việc với bucket](cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/)

</details>

<details>

<summary>Chia sẻ object qua TempURL</summary>

Bạn có thể chia sẻ việc truy cập vào 1 hoặc nhiều object thông qua đường dẫn TempURL. Để biết thêm thông tin, hãy xem tại [Làm việc với ](cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/)[object.](cac-tinh-nang-cua-object-storage/lam-viec-voi-object-va-directory.md)

</details>
