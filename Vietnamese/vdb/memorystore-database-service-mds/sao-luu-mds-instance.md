# Sao lưu MDS Instance

VNG Cloud vDB hỗ trợ hai cách sao lưu (backup) dữ liệu là: theo nhu cầu (on-demand) và tự động hằng ngày (daily automatic) tại thời điểm được ấn định trước.



* [A. Sao lưu theo nhu cầu (On-demand backup hay Manual backup)](sao-luu-mds-instance.md#saoluumdsinstance-a.saoluutheonhucau-on-demandbackuphaymanualbackup)
* [B. Sao lưu tự động theo ngày (Auto-Daily Backup)](sao-luu-mds-instance.md#saoluumdsinstance-b.saoluutudongtheongay-auto-dailybackup)

### A. Sao lưu theo nhu cầu (On-demand backup hay Manual backup) <a href="#saoluumdsinstance-a.saoluutheonhucau-on-demandbackuphaymanualbackup" id="saoluumdsinstance-a.saoluutheonhucau-on-demandbackuphaymanualbackup"></a>

Khi bạn có nhu cầu tạo bản backup, bạn truy cập dịch vụ VNG Cloud và chọn đến màn hình quản lý backup. Màn hình này sẽ liệt kê tất cả các bản backup (manual & auto) của tất cả các DB Instance có trong tài khoản của bạn.

Bạn nhấn vào **Create Backup**

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010752/image2020-2-21_10-39-36.png?version=1&#x26;modificationDate=1582256377000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại màn hình **Create Backup**, bạn lần lượt lựa chọn các thông tin:

* **Database Instance Name**: chọn DB Instance mà bạn muốn thực hiện backup.
* **Backup Name**: đặt tên cho bản backup này.
* **Backup Type**: với MemoryStore bạn có option thực hiện Full Backup.

Sau khi chắc chắn mọi thông tin đều chính xác, bạn nhấn **Create Backup**.

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/13010752/image2020-2-21_10-40-15.png?version=1&#x26;modificationDate=1582256416000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Nếu hệ thống tiếp nhận thành công, một bản backup sẽ xuất hiện với **Status** là **NEW**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010752/image2020-2-21_10-41-18.png?version=1&#x26;modificationDate=1582256479000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Khi được tạo thành công, bản backup sẽ đổi sang **Status** là **COMPLETED**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010752/image2020-2-21_10-41-51.png?version=1&#x26;modificationDate=1582256512000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Chúc mừng bạn đã tạo thành công một bản MANUAL BACKUP.

\


**Mở rộng**: Ngoài màn hình quản lý Backup, bạn còn có thể tạo bản **Manual Backup** ngay tại màn hình quản lý Database. Khi bạn click chọn một DB Instance bất kì, bạn chuyển tới thẻ **Backup** và cuộn xuống danh sách **Backup list**. Ở đây sẽ liệt kê tất cả các bản backup (manual & auto) tương ứng với DB Instance này. Bạn có thể nhấn **Create Backup** để tiến hành tạo bản Manual Backup ngay tại đây.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010752/image2020-2-21_10-42-36.png?version=1&#x26;modificationDate=1582256556000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Thao tác tiếp theo hoàn toàn tương tự như hướng dẫn ở trên.

### **B. Sao lưu tự động theo ngày (Auto-Daily Backup)** <a href="#saoluumdsinstance-b.saoluutudongtheongay-auto-dailybackup" id="saoluumdsinstance-b.saoluutudongtheongay-auto-dailybackup"></a>

vDBaaS hỗ trợ tính năng tự động sao lưu theo ngày tại thời điểm do bạn ấn định.

Để xem một DB Instance đã được cấu hình tính năng này chưa, bạn truy cập màn hình quản lý Database. Sau đó, bạn click chọn DB Instance muốn kiểm tra, chọn thẻ **Backup** và tìm đến mục **Backup Information**. Nếu **Automatic backup** là **Enabled** tức là bạn đã cấu hình tự động sao lưu hàng ngày cho DB Instance này vào thời điểm **Backup Time** trong ngày.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010752/image2020-2-21_10-43-29.png?version=1&#x26;modificationDate=1582256610000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Để cấu hình tính năng này, bạn có hai phương án:

* Cấu hình luôn trong lúc khởi tạo DB Instance.
* Thay đổi tại giao diện quản lý Database.

Đối với phương án đầu, mời bạn xem lại hướng dẫn Khởi tạo DB Instance tại [Hướng dẫn khởi tạo MDS Instance](khoi-tao-mds-instance.md).

Đối với phương án sau, bạn truy cập màn hình quản lý Database, click chọn DB Instance muốn cấu hình. Sau đó, bạn click chọn **Edit Database**. Tại đây, bạn kéo xuống mục **CHANGE BACKUP SETTINGS** và bạn có thể cấu hình các thông tin:

* **Automatic daily backup:** bật tắt tính năng Automatic daily backup.
* **Backup retention period:** xác định thời gian lưu trữ bản automatic backup. Nhằm giúp bạn tiết kiệm không gian lưu trữ, các bản automatic backup đã quá khoảng thời gian này sẽ bị xóa.
* **Backup time:** thời điểm quá trình tạo automatic backup diễn ra. VNG Cloud khuyến nghị bạn chọn thời điểm này vào khoảng thời gian thấp điểm nhất đối với hệ thống của bạn.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010752/image2020-2-21_10-44-6.png?version=1&#x26;modificationDate=1582256647000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Sau khi chắc chắn rằng các thông tin đã chính xác, bạn nhấn nút **Save** ở góc trên bên phải và chờ một lát để quá trình thay đổi được thực thi.

Bạn có thể tham khảo video sau:
