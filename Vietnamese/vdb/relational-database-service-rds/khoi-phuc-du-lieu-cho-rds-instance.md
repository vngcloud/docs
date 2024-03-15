# Khôi phục dữ liệu cho RDS Instance

VNG Cloud vDB hỗ trợ bạn khôi phục (Restore) lại một RDS Instance mới từ bản sao lưu (Backup) trước đó. Quá trình khôi phục này không phụ thuộc vào loại Backup (Full Backup hay Incremetal Backup) hay cách tạo ra bản backup đó (Manual Backup hay Automactic Daily Backup).

Để thực hiện tiến trình khôi phục, bạn truy cập màn hình quản lý Backup.

Tại đây, bạn click chọn vào bản Backup mà bạn muốn khôi phục, chọn Action **Restore**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723085/image2019-6-24_15-11-33.png?version=1&#x26;modificationDate=1561363893000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



Quá trình Restore cũng gần tương tự như quá trình **Khởi tạo một RDS Instance** mới. Bạn có thể tùy chỉnh cấu hình Flavor (CPU/Memory), Storage Type và Storage Size.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723085/image2019-6-24_15-11-47.png?version=1&#x26;modificationDate=1561363907000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại mục **Settings**, bạn có thể đặt tên cho RDS Instance mới này.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723085/image2019-6-24_15-12-5.png?version=1&#x26;modificationDate=1561363926000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại mục **Network & Security**, bạn có lựa chọn Cloud Network & bật/tắt khả năng truy cập từ Internet (**Public Accessibility**). Cloud Network ở đây có thể giống hoặc khác Cloud Network của RDS Instance cũ.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723085/image2019-6-24_15-12-16.png?version=1&#x26;modificationDate=1561363937000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại mục DB Options, bạn có thể lựa chọn **DB Configuration Group (Optional)** cho RDS Instance này. Lựa chọn này cũng có thể giống hoặc khác so với RDS Instance cũ.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723085/image2019-6-24_15-12-28.png?version=1&#x26;modificationDate=1561363949000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Sau khi chắc chắn các thông tin đã chính xác, bạn nhấp nút **Restore Backup** ở góc phải trên.

Sau đó, bạn quay lại màn hình quản lý Database, sẽ thấy xuất hiện một RDS Instance đang được khôi phục.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723085/image2019-6-24_15-12-41.png?version=1&#x26;modificationDate=1561363962000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Trạng trái của RDS Instance mới này cũng sẽ thay đổi từ Building/Build sang Active nếu thành công.

Thông tin **Master User,** **Databases** sẽ được giữ nguyên như cũ.

Khi khôi phục thành công, RDS Instance mới sẽ có trạng thái **Active**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723085/image2019-6-24_15-12-55.png?version=1&#x26;modificationDate=1561363975000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Chúc mừng bạn đã khôi phục dữ liệu thành công với tính năng Restore của vDBaaS.

Bạn có thể tham khảo video sau:
