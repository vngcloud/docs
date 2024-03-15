# Khởi tạo MDS Instance

Đầu tiên, bạn truy cập Portal của VNG Cloud tại đường dẫn: [https://portal.vngcloud.vn](https://portal.vngcloud.vn/)

Tại giao diện chính, bạn tìm đến dịch vụ **vDB - Database** và chọn dịch vụ hệ lưu trữ dữ liệu trên bộ nhớ (in-memory) **MemoryStore Database.**

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010707/Screenshot%20from%202020-02-21%2000-00-05.png?version=1&#x26;modificationDate=1582218596000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại giao diện quản lý Database, bạn click chọn **Create Database**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010707/Screenshot%20from%202020-02-21%2000-00-45.png?version=1&#x26;modificationDate=1582218597000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Quá trình khởi tạo sẽ trải qua 3 bước: **Select Engine**, **Specify DB details** và **Summary**. Hãy cùng VNG Cloud đi vào chi tiết cả 3 bước trên:

**Bước 1**, bạn chọn **Database Engine** mong muốn, sau đó chọn **Next**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010707/Screenshot%20from%202020-02-21%2000-01-01.png?version=1&#x26;modificationDate=1582218597000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



**Bước 2**, bạn có thể tùy chỉnh các thông tin cấu hình, tên gọi, network, configuration group và backup scheduler.

Tại mục **DB Instance Specifications**, bạn lựa chọn:

* **Engine License**: giấy phép sử dụng database, có thể là phiên bản community hoặc enterprise (tùy từng loại database).
* **Engine Version**: phiên bản database.
* **Flavor**: cấu hình DB Instance, bao gồm số core, lượng RAM và đi kèm dung lượng Free Backup. Lưu ý: nếu tổng dung lượng tất cả các bản backup của bạn vượt quá quota này, bạn sẽ phải trả thêm chi phí cho phần dung lượng backup vượt quá quota.
* **Storage type**: loại ổ cứng lưu trữ.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010707/Screenshot%20from%202020-02-21%2000-01-27.png?version=1&#x26;modificationDate=1582218597000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại mục **Setttings**, bạn có thể cấu hình:

* **Database Name**: tên database sẽ được khởi tạo tự động.
* **DB configuration group** (optional): tên Configuration Group sẽ được áp dụng cho DB Instance này, nếu bạn chưa có nhu cầu tùy chỉnh cấu hình thì có thể bỏ qua trường này.

Tại mục **Network & Security**, bạn lựa chọn **Cloud Network** sẽ sử dụng cho DB Instance này. Mọi DB Instance đều phải kết nối với một Cloud Network. Nếu chưa có Cloud Network nào, bạn có thể tạo một Cloud Network mới với hướng dẫn sau: [Link](https://docs.vinadata.vn/pages/viewpage.action?pageId=2721227).

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010707/Screenshot%20from%202020-02-21%2000-02-26.png?version=1&#x26;modificationDate=1582218598000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại mục **Backup**, bạn có thể cấu hình:

* **Automatic daily backup**: bật/tắt tính năng tự động tạo backup hàng ngày với thời điểm được lựa chọn trước.
* **Backup retention period**: khoảng thời gian lưu trữ các bản backup tự động. Các bản backup tự động được lưu trữ quá thời gian này sẽ được tự động xóa khỏi hệ thống. Thông số này không ảnh huởng đến vòng đời của các bản backup được bạn tạo bằng tay.
* **Backup time**: thời điểm tiến hành tạo bản backup tự động. VNG Cloud khuyến nghị bạn cấu hình thời điểm này vào thời điểm có lượng truy cập hệ thống thấp nhất trong ngày, thường là từ 12AM - 5AM.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010707/Screenshot%20from%202020-02-21%2000-03-10.png?version=1&#x26;modificationDate=1582218598000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
\


Sau khi cấu hình xong, bạn nhấn **Next** để sang bước cuối.

Tại bước **Summary**, bạn rà soát lại các thông tin. Nếu có thay đổi, bạn có thể nhấn **Back**. Khi mọi thông tin đều đã chính xác, bạn nhấn **Create Database**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010707/Screenshot%20from%202020-02-21%2000-03-57.png?version=1&#x26;modificationDate=1582218598000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Trong quá trình khởi tạo, DB Instance sẽ có trạng thái **Building**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010707/Screenshot%20from%202020-02-21%2000-04-45.png?version=1&#x26;modificationDate=1582218598000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



Nếu khởi tạo thành công, DB Instance sẽ có trạng thái **Active**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010707/Screenshot%20from%202020-02-21%2000-08-32.png?version=1&#x26;modificationDate=1582218598000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Khi tick chọn DB Instance, bạn có thể xem lại các thông tin cấu hình chi tiết như Flavor, Endpoint & Port để kết nối,... Bạn có thể tham khảo link sau [Quản lý thông tin MDS Instance](https://docs.vngcloud.vn/pages/viewpage.action?pageId=13010741)

Chúc mừng bạn đã khởi tạo thành công DB Instance trên hệ thống VNG Cloud. Mời bạn đến hướng dẫn [kết nối MDS Instance](https://docs.vngcloud.vn/pages/viewpage.action?pageId=13010730) để bắt đầu sử dụng cơ sở dữ liệu.

