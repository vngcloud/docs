# \[Rclone] Mount vStorage lên Window server

Rclone là công cụ giúp đồng hoá dữ liệu và thư mục đến nhiều dịch vụ lưu trữ cloud khác nhau, bao gồm AWS S3, Google Cloud, Dropbox, Google Drive, vStorage v..v... Để biết thêm thông tin về Rclone, hãy xem tại : [https://rclone.org/](https://rclone.org/).

Để thực hiện upload lên vStorage sử dụng rclone trên hệ điều hành Window bạn hãy xem thêm tại: [https://vstorage.console.vngcloud.vn/integration/integration](https://vstorage.console.vngcloud.vn/integration/integration).

**Lưu ý:**

* Nếu gặp lỗi thiếu gói winfsp như hình dưới, bạn có thể tải thêm gói tại link này [https://github.com/billziss-gh/winfsp/releases/tag/v1.4.19049](https://github.com/billziss-gh/winfsp/releases/tag/v1.4.19049)

&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/49648973/image2019-11-28_17-55-37.png?version=1&#x26;modificationDate=1675845182000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Bạn không cần phải tạo sẵn đường dẫn local\_path trên máy local khi tiến hành mount.
* Rclone không hỗ trợ mode chạy ngầm (background mode) nên bạn không được đóng cmd trong quá trình sử dụng.

\
