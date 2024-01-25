 **Cấu hình chứng chỉ SSL** Để có thể sử dụng chứng chỉ SSL bạn phải có sẵn chứng chỉ SSL hoặc sử dụng chứng chỉ SSL miễn phí được cung cấp bởi Let’s Encrypt. Các certificate được VNG CLOUD lưu tại một nơi bảo mật, an toàn, hệ thống lưu trữ các certificate được mã hóa và không thể truy cập bởi bất cứ ai bao gồm cả các nhân viên của VNG CLOUD.

Có 2 cách để có thể tạo một Certificate:


* Trang quản lý Certificate
* Tạo khi khởi tạo Listener

 **Truy cập vào trang quản lý Certificate:** ![](images/storage/image2020-5-11_11-23-38.png)

Để tạo mới một certificate bạn nhấn chọn  **UPLOAD**  ** CERTIFICATE** .

![](images/storage/image2020-5-11_15-6-6.png)



Nhập các thông tin:


* Friendly Name: Tên của Certificate.
* Certificate: là server certificate domain của bạn (thường có đuôi \*.crt), có định dạng chuẩn PEM.

                 ![](images/storage/image2020-5-11_15-52-15.png)


* Private Key: là khóa riêng của certificate trên (thường có đuôi \*.key), có định dạng chuẩn PEM.

                ![](images/storage/image2020-5-11_15-51-38.png)


* Certificate Chain: là chuỗi certificate bao gồm server certificate và intermediate certificate (nếu có), có định dạng chuẩn PEM.

                ![](images/storage/image2020-5-11_15-53-12.png)

              _Chú ý t_  _hứ tự add chain sẽ như sau:_ 

 _             _ ---BEGIN CERTIFICATE---             \[Your certificate]             ---END CERTIFICATE---             ---BEGIN CERTIFICATE---             \[Intermidate#1 certificate](option)             ---END CERTIFICATE---             ---BEGIN CERTIFICATE---            \[Intermidate#2 certificate](option)             ---END CERTIFICATE---


* Passphrase: trong trường hợp khóa riêng (private key) có mật khẩu thì cần nhập mật khẩu của khóa riêng, ngược lại bỏ trống trường này.
* Expiration: ngày hết hạn của Certificate.

Sau khi nhập đầy đủ các thông tin của certificate, nhấn  **IMPORT** .







Trang quản lý SSL Certificate như trên, lúc này bạn sẽ thấy được danh sách các Certificate đã được upload, cùng với ngày khởi tạo và hết hạn của Certificate.





*****

[[category.storage-team]] 
[[category.confluence]] 
