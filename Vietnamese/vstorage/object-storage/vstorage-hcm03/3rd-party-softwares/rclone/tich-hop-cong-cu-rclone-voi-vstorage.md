# Tích hợp công cụ Rclone với vStorage

Để xem hướng dẫn tích hợp công cụ Rclone với vStorage, bạn có thể thực hiện qua vStorage Portal theo hướng dẫn bên dưới:&#x20;

1. Đăng nhập vào [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).
2. Chọn thư mục **Tích hợp.**
3. Chọn biểu tượng **Rclone**.
4. Tại mục **Cấp quyền**, bạn cần điền thông tin cần thiết để cấu hình Rclone của bạn nhằm tích hợp với vStorage bao gồm:
   1. Chọn một **Giao thức** mà bạn muốn thực hiện tích hợp Rclone với vStorage. Hiện tại chúng tôi hỗ trợ cho bạn 2 giao thức bao gồm S3 hoặc HTTPS.
   2. Chọn một **Region** chứa project mà bạn muốn thực hiện truy xuất dữ liệu tới trong danh sách các Region mà chúng tôi cung cấp.
   3. Chọn một **Project** trong danh sách các project đang tồn tại trong Region mà bạn chọn trước đó. Nếu danh sách project hiển thị chưa đầy đủ, bạn có thể chọn , chúng tôi sẽ tải lại danh sách project mới nhất tại thời điểm bạn thực hiện hành động này.
   4. Chọn một **Access key** trong danh sách các access key đang tồn tại thuộc project mà bạn chọn trước đó.
   5. Nhập **Secret key** tương ứng của **Access key** vừa chọn. Cặp access key và secret key được bạn tạo và quản lý thông qua hệ thống vIAM. Bạn có thể chọn [Nhấn vào đây để vào vIAM và quản lý s3 keys](https://hcm-3.console.vngcloud.vn/iam/vstorage-credentials/s3) để chúng tôi điều hướng bạn tới hệ thống vIAM và chi tiết là các màn hình quản lý S3 keys. Để biết thêm thông tin về S3 keys, hãy xem tại [Khởi tạo vStorage Credentials](../../quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials/).
5. Sau khi hoàn tất chọn cấu hình **Cấp quyền**, chọn **Cấu hình Rclone** để chuyển tới màn hình **Cấu hình**. Bạn luôn có thể quay lại đây để thay đổi thông tin **Cấp quyền** của mình, sau đó chọn lại **Cấu hình Rclone** để cập nhật cách sử dụng theo thông số mới của bạn. Bạn có thể xem hướng dẫn cách cài đặt, cấu hình Rclone ngay trên màn hình này. Chi tiết tham khảo thêm tại: [Tích hợp vStorage.](https://vstorage.console.vngcloud.vn/integration/integration)

<figure><img src="../../../../../.gitbook/assets/Tich_hop_Rclone.gif" alt=""><figcaption></figcaption></figure>
