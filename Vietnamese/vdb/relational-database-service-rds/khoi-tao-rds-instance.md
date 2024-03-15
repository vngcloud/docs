# Khởi tạo RDS Instance

Để khởi tạo RDS Instacne, bạn có thể tham khảo video sau:

{% embed url="https://youtu.be/Fh5j6EHb4Gc" %}

Chi tiết các bước làm có trong hướng dẫn bên dưới đây.

Đầu tiên, bạn truy cập Portal của VNG Cloud tại đường dẫn: [https://portal.vngcloud.vn](https://portal.vngcloud.vn/)

Tại giao diện chính, bạn tìm đến dịch vụ **vDB - Database** và chọn dịch vụ **Relational Databases.**

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/Screenshot%20from%202020-02-21%2000-00-05.png?version=1&#x26;modificationDate=1582219155000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại giao diện quản lý Database, bạn click chọn **Create Database**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-32-3.png?version=1&#x26;modificationDate=1561350724000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
\
Quá trình khởi tạo sẽ trải qua 3 bước: **Select Engine**, **Specify DB details** và **Summary**. Hãy cùng VNG Cloud đi vào chi tiết cả 3 bước trên:

**Bước 1**, bạn chọn **Database Engine** mong muốn, sau đó chọn **Next**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-32-52.png?version=1&#x26;modificationDate=1561350773000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
\
**Bước 2**, bạn có thể tùy chỉnh các thông tin cấu hình, tên gọi, master user, network, configuration group và backup.

Tại mục **DB Instance Specifications**, bạn lựa chọn:

* **Engine License**: giấy phép sử dụng database, có thể là phiên bản community hoặc enterprise (tùy từng loại database).
* **Engine Version**: phiên bản database.
* **Flavor**: cấu hình RDS Instance, bao gồm số core, lượng RAM và đi kèm dung lượng Free Backup. Lưu ý: nếu tổng dung lượng tất cả các bản backup của bạn vượt quá quota này, bạn sẽ phải trả thêm chi phí cho phần dung lượng backup vượt quá quota.
* **Storage type**: loại ổ cứng lưu trữ.
* **Storage Size**: kích cỡ ổ cứng lưu trữ dữ liệu (bao gồm data và log của database).

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-33-19.png?version=1&#x26;modificationDate=1561350800000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại mục **Settings,** bạn lựa chọn:

* **DB Instance Name**: tên của RDS Instance
* **Master username**: bạn sẽ dùng user này để quản trị database instance.
* **Master password**: password của master user. VNG Cloud khuyến nghị bạn đặt password đủ mạnh và lưu trữ password này tại nơi an toàn. Để đảm bảo an toàn thông tin, password cần thỏa tất cả yêu cầu tối thiểu như sau:
  * Password phải có độ dài trong khoảng 8-32 kí tự.
  * Các kí tự được cho phép bao gồm: A-Z, a-z, 0-9 và các kí tự đặc biệt.
  * Các kí tự đặc biệt được cho phép bao gồm: !#$%&()\*+-.:<=>?@\[]^\_{|}\~
  * Password phải bắt đầu bằng kí tự chữ cái: A-Z hoặc a-z.
  * Password không được bắt đầu hay kết thúc bằng các kí tự đặc biệt.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-33-33.png?version=1&#x26;modificationDate=1561350814000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Tại mục **Network & Security**, bạn lựa chọn **Cloud Network** sẽ sử dụng cho RDS Instance này. Mọi RDS Instance đều phải kết nối với một Cloud Network. Nếu chưa có Cloud Network nào, bạn có thể tạo một Cloud Network mới với hướng dẫn sau: [Link](https://docs.vinadata.vn/pages/viewpage.action?pageId=2721227).

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-33-45.png?version=1&#x26;modificationDate=1561350826000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Nếu bạn muốn RDS Instance có IP Public và có thể truy cập từ ngoài Internet, bạn cần bật tính năng **Public Accessbility**, nếu bạn muốn RDS Instance chỉ có IP Private và chỉ những Cloud Servers mới có thể truy cập được thì bạn cần tắt tính năng Public Accessibility.

**Lưu ý**: việc lựa chọn có hay không Public Accessibility chỉ được lựa chọn một lần duy nhất tại thời điểm khởi tạo này. Bạn không thể thay đổi thiết lập này về sau. Để tăng cường bảo mật, VNG Cloud cho phép bạn giới hạn các địa chỉ IP tin cậy được phép truy cập vào mỗi RDS Instance thông qua **Security Group Rules**.

\


Tại mục **DB Options**, bạn có thể cấu hình:

* **Database Name**: tên database sẽ được khởi tạo tự động.
* **DB configuration group** (optional): tên Configuration Group sẽ được áp dụng cho RDS Instance này, nếu bạn chưa có nhu cầu tùy chỉnh cấu hình thì có thể bỏ qua trường này.

![](https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24\_11-33-58.png?version=1\&modificationDate=1561350839000\&api=v2)

\


\


Tại mục **Backup**, bạn có thể cấu hình:

* **Automatic daily backup**: bật/tắt tính năng tự động tạo backup hàng ngày với thời điểm được lựa chọn trước.
* **Backup retention period**: khoảng thời gian lưu trữ các bản backup tự động. Các bản backup tự động được lưu trữ quá thời gian này sẽ được tự động xóa khỏi hệ thống. Thông số này không ảnh huởng đến vòng đời của các bản backup được bạn tạo bằng tay.
* **Backup time**: thời điểm tiến hành tạo bản backup tự động. VNG Cloud khuyến nghị bạn cấu hình thời điểm này vào thời điểm có lượng truy cập hệ thống thấp nhất trong ngày, thường là từ 12AM - 5AM.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-34-7.png?version=1&#x26;modificationDate=1561350847000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Sau khi cấu hình xong, bạn nhấn **Next** để sang bước cuối.

Tại bước **Summary**, bạn rà soát lại các thông tin. Nếu có thay đổi, bạn có thể nhấn **Back**. Khi mọi thông tin đều đã chính xác, bạn nhấn **Create Database**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-34-40.png?version=1&#x26;modificationDate=1561350881000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


\


Tiếp đó bạn đọc và nhấn chọn để đồng ý với các Policy của VNG Cloud.

Bạn nhấn **OK** để tiếp tục.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-35-4.png?version=1&#x26;modificationDate=1561350905000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


**Lưu ý**:

Mặc định, RDS Instance tạo ra sẽ có sẵn 3 user:

* 2 user hệ thống là root@localhost & [os\_admin@127.0.0.1](mailto:os\_admin@127.0.0.1).
* 1 master user giúp bạn có thể truy cập và quản lý RDS Instance.

\


Hai user hệ thống được tạo ra để VNG Cloud phục vụ các tác vụ tự động như tạo backup, cấu hình replication, restore… và bạn không cần phải quan tâm những user này. Tuy nhiên, việc bạn xóa 2 user hệ thống này sẽ gây ra lỗi hệ thống cho RDS Instance và khiến các tính năng trên mất tác dụng. VNG Cloud sẽ không chịu trách nhiệm nếu bạn tìm cách xóa 2 user hệ thống nhưng vẫn sẽ hỗ trợ tốt nhất có thể để khôi phục cho bạn cho bạn.

\


\


Sau khi tạo xong, bạn sẽ thấy thông báo để xác nhận hệ thống đã tiếp nhận yêu cầu khởi tạo thành công. Bạn nhấn **Close** để quay lại giao diện quản lý database.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-35-20.png?version=1&#x26;modificationDate=1561350921000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


\


Trong quá trình khởi tạo, RDS Instance sẽ có trạng thái **Building** hay **Build**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-35-29.png?version=1&#x26;modificationDate=1561350930000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Nếu khởi tạo thành công, RDS Instance sẽ có trạng thái **Active**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-35-42.png?version=1&#x26;modificationDate=1561350943000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Khi tick chọn RDS Instance, bạn có thể xem lại các thông tin cấu hình chi tiết như Flavor, Endpoint & Port để kết nối,...

<figure><img src="https://docs.vngcloud.vn/download/attachments/2722985/image2019-6-24_11-50-14.png?version=1&#x26;modificationDate=1561351815000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Chúc mừng bạn đã khởi tạo thành công RDS Instance trên hệ thống VNG Cloud. Mời bạn đến hướng dẫn [kết nối RDS Instance](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2723017) để bắt đầu sử dụng cơ sở dữ liệu.

