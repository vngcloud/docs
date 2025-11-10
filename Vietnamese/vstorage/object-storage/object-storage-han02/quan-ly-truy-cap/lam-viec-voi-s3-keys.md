# Làm việc với S3 Keys

## **Tổng quan**

Trên hệ thống vStorage, S3 key là cặp key bao gồm access key và secret key được vStorage tích hợp và tương thích với các client tool của S3 như s3cmd, s3 SDK,...

***

## Root User Account khởi tạo S3 keys

Để khởi tạo S3 key, làm theo hướng dẫn bên dưới:

1. Đăng nhập vào [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) với tài khoản <mark style="background-color:orange;">Root User Account</mark>.
2. Chọn **Region HAN02.**
3. Chọn biểu tượng  <img src="../../../../.gitbook/assets/image (581).png" alt="" data-size="line"> tại project mà bạn vừa khởi tạo sau đó chọn mục **Identity and Access Management.**
4. Tại mục **List of S3 keys of this project**, chọn **Generate S3 key**.
5. Chọn **Copy** hoặc **Download** để tải xuống thông tin Access Key/Secret Key mà bạn vừa khởi tạo.

<figure><img src="../../../../.gitbook/assets/image (1050).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (1051).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (1052).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Chú ý:**

* Sau khi nhấn tạo S3 key, bạn cần **lưu lại cặp Access Key/Secret Key** để sử dụng, nếu bạn không lưu trữ ngay lúc này thì sau đó không thể lấy được Secret Key của Access Key này.
* <mark style="background-color:orange;">S3 key được khởi tạo bởi</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">**Root User Account**</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">sẽ có toàn quyền truy cập/ thao tác trên các bucket thuộc project này.</mark>
{% endhint %}

***

## IAM User Account khởi tạo S3 keys

Để khởi tạo S3 key, làm theo hướng dẫn bên dưới:

1. Đăng nhập vào [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) với tài khoản <mark style="background-color:orange;">IAM User Account</mark>.
2. Chọn **Region HAN02.**
3. Chọn biểu tượng  <img src="../../../../.gitbook/assets/image (581).png" alt="" data-size="line"> tại project mà bạn vừa khởi tạo sau đó chọn mục **Identity and Access Management.**
4. Tại mục **List of S3 keys of this project**, chọn **Generate S3 key**.
5. Chọn **Copy** hoặc **Download** để tải xuống thông tin Access Key/Secret Key mà bạn vừa khởi tạo.

<figure><img src="../../../../.gitbook/assets/image (1053).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Chú ý:**

* Sau khi nhấn tạo S3 key, bạn cần **lưu lại cặp Access Key/Secret Key** để sử dụng, nếu bạn không lưu trữ ngay lúc này thì sau đó không thể lấy được Secret Key của Access Key này.
* <mark style="background-color:orange;">S3 key được khởi tạo bởi</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">**IAM User Account**</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">sẽ có toàn quyền truy cập/ thao tác trên các bucket/object theo quyền hạn của IAM User Account đó. Ví dụ, nếu IAM User Account của bạn chỉ có quyền Read Object thì S3 keys tạo bởi IAM User Account này cũng chỉ có quyền Read Object.</mark>
{% endhint %}

***

## Thực hiện làm việc với S3 API (hoặc 3rd party software) thông qua S3 keys

### Kết nối 3rd party softwares với vStorage

Sau khi bạn đã thực hiện khởi tạo project và khởi tạo S3 key thành công, lúc này bạn có thể sử dụng các 3rd party softwares để kết nối và làm việc với project của bạn. Các công cụ 3rd party softwares bạn có thể lựa chọn sử dụng có thể là S3cmd, Cyberduck, Rclone, S3 Browser, MinIO Client,...Trong phạm vi tài liệu này, chúng tôi sẽ hướng dẫn bạn kết nối S3 Browser với vStorage. S3 Browser là công cụ được tối ưu hóa cho phép bạn chia sẻ và tải lên tệp tin của mình. Công cụ này có giao diện tương đối đơn giản, dễ sử dụng và đã tương thích với API của dịch vụ lưu trữ vStorage.&#x20;

Để tích hợp công cụ S3 Browser với vStorage, bạn có thể thực hiện theo hướng dẫn bên dưới:

1. Tải công cụ người dùng S3 Browser tại đây [https://s3browser.com/download.aspx](https://s3browser.com/download.aspx).
2. Mở ứng dụng **S3 Browser.** Chọn thư mục **Account, sau đó chọn Add new account**

<figure><img src="../../../../.gitbook/assets/image (585).png" alt="" width="295"><figcaption></figcaption></figure>



3. Màn hình Add New Account hiển thị, lúc này bạn nhập các thông tin như sau:

* **Display name:** Tên hiển thị của account. Ví dụ: Demo\_HAN02
* **Account type**: Chọn **S3 Compatible Storage.**
* **REST Endpoint**: Đường dẫn đến vstorage, đối với Region HAN02 thì đường dẫn là han02.vstorage.vngcloud.vn
* **Access Key ID & Secret Access Key:** Là cặp S3 key bạn đã thực hiện generate tại bước 4 trước đó.

4. Chọn option **Use Secure transfer (SSL/TLS)** vì vStorage chỉ hỗ trợ kênh truyền đã được mã hoá (HTTPS, port 443) để đảm bảo an toàn dữ liệu, vStorage hiện tại không hỗ trợ kênh truyền không mã hoá (HTTP, port 80).
5. Chọn **Add new account.**

<figure><img src="../../../../.gitbook/assets/image (992).png" alt="" width="375"><figcaption></figcaption></figure>

6. Khi kết nối thành công, màn hình S3 Browser sẽ hiển thị như sau:&#x20;

<figure><img src="../../../../.gitbook/assets/image (993).png" alt=""><figcaption></figcaption></figure>



***

## Xóa S3 keys

Để hủy (xóa) một hay nhiều S3 key đã tạo trước đó, hãy làm theo hướng dẫn bên dưới:

1. Đăng nhập vào [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) với tài khoản <mark style="background-color:orange;">Root User Account</mark> hoặc tài khoản <mark style="background-color:orange;">IAM User Account</mark>.
2. Chọn **Region HAN02.**
3. Chọn biểu tượng  <img src="../../../../.gitbook/assets/image (581).png" alt="" data-size="line"> tại project mà bạn vừa khởi tạo sau đó chọn mục **Identity and Access Management.**
4. Tại mục **List of S3 keys of this project**, chọn **S3 key** mà bạn muốn xóa sau đó chọn **Delete.**

Kể từ thời điểm S3 key bị hủy thành công, bạn sẽ không thể sử dụng S3 key này để truy xuất vào vStorage. Hãy thận trọng khi thực hiện thao tác hủy (xóa) tài khoản S3 bởi bạn sẽ không thể khôi phục tài khoản đã xóa này.

<figure><img src="../../../../.gitbook/assets/image (1055).png" alt=""><figcaption></figcaption></figure>

