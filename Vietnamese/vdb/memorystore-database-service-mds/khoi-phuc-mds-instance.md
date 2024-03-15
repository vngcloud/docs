# Khôi phục MDS Instance

VNG Cloud vDB hỗ trợ bạn khôi phục (Restore) lại một MDS Instance mới từ bản sao lưu (Backup) trước đó. Quá trình khôi phục này không phụ thuộc vào cách tạo ra bản backup đó (Manual Backup hay Automactic Daily Backup).

Để thực hiện tiến trình khôi phục, bạn truy cập màn hình quản lý Backup.

Tại đây, bạn click chọn vào bản Backup mà bạn muốn khôi phục, chọn Action **Restore**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010764/image2020-2-21_10-45-27.png?version=1&#x26;modificationDate=1582256727000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Quá trình Restore cũng gần tương tự như quá trình Tạo một MDS Instance mới.

Tại màn hình khôi phục MDS Instance, bạn cũng có thể lựa chọn các thông tin về cấu hình MDS Instance mới tại các thông tin **Flavor**, **Storage Type** & **Storage Size** trong mục **MDS Instance Specifications**.

Tại mục **Settings**, bạn có thể đặt tên cho MDS Instance mới này.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010764/image2020-2-21_10-46-5.png?version=1&#x26;modificationDate=1582256766000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại mục **Network & Security**, bạn có lựa chọn Cloud Network & bật/tắt khả năng truy cập từ Internet (**Public Accessibility**). Cloud Network ở đây có thể giống hoặc khác Cloud Network của MDS Instance cũ.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010764/image2020-2-21_10-47-23.png?version=1&#x26;modificationDate=1582256843000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại mục DB Options, bạn có thể lựa chọn **DB Configuration Group (Optional)** cho MDS Instance này. Lựa chọn này cũng có thể giống hoặc khác so với MDS Instance cũ.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010764/image2020-2-21_10-46-57.png?version=1&#x26;modificationDate=1582256818000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Sau khi chắc chắn các thông tin đã chính xác, bạn nhấp nút **Restore Backup** ở góc phải trên.

Sau đó, bạn quay lại màn hình quản lý Database, sẽ thấy xuất hiện một MDS Instance đang được khởi tạo.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010764/image2020-2-21_10-48-22.png?version=1&#x26;modificationDate=1582256903000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Trạng trái của MDS Instance mới này cũng sẽ thay đổi từ Building/Build sang Active nếu thành công.

Khi khôi phục thành công, MDS Instance mới sẽ có trạng thái **Active**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010764/image2020-2-21_10-51-24.png?version=1&#x26;modificationDate=1582257085000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Chúc mừng bạn đã khôi phục dữ liệu thành công với tính năng Restore của vDBaaS.

Bạn có thể tham khảo video sau:

{% embed url="https://youtu.be/ZpN6fekI3Ek" %}
