# Quản lý thông tin RDS Instance

VNG Cloud vDB cung cấp các giao diện (dashboard) giúp bạn quản lý RDS Instance, các bản Backup & các Configuration Group một cách hiệu quả và tiện dụng.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2019-6-24_14-31-31.png?version=1&#x26;modificationDate=1561361492000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Hãy cùng điểm qua các Dashboard này.

* [A - Giao diện quản lý Database](quan-ly-thong-tin-rds-instance.md#quanlythongtinrdsinstance-a-giaodienquanlydatabase)
* [B - Giao diện quản lý Backup](quan-ly-thong-tin-rds-instance.md#quanlythongtinrdsinstance-b-giaodienquanlybackup)
* [C- Giao diện quản lý Configuration Group](quan-ly-thong-tin-rds-instance.md#quanlythongtinrdsinstance-c-giaodienquanlyconfigurationgroup)

### A - Giao diện quản lý Database <a href="#quanlythongtinrdsinstance-a-giaodienquanlydatabase" id="quanlythongtinrdsinstance-a-giaodienquanlydatabase"></a>

Giao diện quản lý Database cho phép bạn có cái nhìn tổng quát về tất cả các RDS Instance hiện có cũng như thông tin chi tiết cho từng RDS Instance. Bạn có thể thực hiện tạo mới một Database khi click chọn **CREATE DATABASE** (Nút số 1).

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2019-6-24_14-31-47.png?version=1&#x26;modificationDate=1561361508000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Khi bạn click chọn từng RDS Instance, bạn có thể:

* Thực hiện các **ACTION** quản lý vòng đời của RDS Instance như: **START**, **STOP**, **RESTART** hay **DELETE**. (Vùng số 2).
* Thay đổi các thông tin cấu hình của RDS Instance tại **EDIT DATABASE**. (Nút số 3).
* Xem chi tiết thông tin cấu hình từng RDS Instance (Vùng số 4).



Khi bạn Click vào **EDIT DATABASE** (nút số 3), bạn sẽ đi đến giao diện thay đổi vDB:

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2023-6-16_15-10-32.png?version=1&#x26;modificationDate=1686903032000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

tại đây bạn có thể **EDIT**:

* Database Instance Flavor: thay đổi cấu hình Flavor (CPU/Memory, cũng như Free Backup Storage Quota đi kèm).
* Database Instance Storagre: thay đổi Storage Type (IOPS) và Storage Size.
* Configuration Group: gắn/tháo liên kết với Configuration Group.
* Database Settings: thay đổi Password của Master User, bật/tắt Public Access từ Internet (gắn/tháo Public IP), điều chỉnh bật/tắt Automatic daily backup cũng như thiết lập thời gian chạy Daily Backup.\


Tại vùng số 4, bạn sẽ có 4 tab quản lý:

* **CONFIGURATION**: bao gồm thông tin tổng quan về RDS Instance như **DB Name**, loại **Database Engine**, **Engine Version** cũng như thông tin cấu hình tính toán, bộ nhớ và lưu trữ.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2019-6-24_14-32-7.png?version=1&#x26;modificationDate=1561361527000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


* **CONNECTIVITY & SECURITY:** cho bạn các thông tin về **Endpoint & Port** để kết nối đến. Mọi RDS Instance sẽ có một **Private Endpoint** tương ứng với **Cloud Network**. Nếu bạn có chọn **Enable Public Accessibility** trong quá khởi tạo, bạn sẽ có thêm một **Public Endpoint** cho phép truy cập từ Internet. Bên cạnh đó, bạn có thể giới hạn những địa chỉ IP tin cậy mới được truy cập RDS Instance thông qua **Security Group Rules**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2019-6-24_14-32-21.png?version=1&#x26;modificationDate=1561361542000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


* **BACKUP**: cho bạn thông tin về:
  * **Automatic Backup** đã được Enable hay đang Disabled.
  * **Backup Time:** thời điểm thực hiện.
  * **Backup Usage**: dung lượng lưu trữ đã sử dụng trong FREE backup quota bạn được sử dụng.

Ngoài ra, mục **Backup list** cũng liệt kê toàn bộ các bản Backup tương ứng với RDS Instance này. Bạn cũng có thể thực hiện tạo Manual Backup thông qua nút **Create Backup.**

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/Screenshot%202023-06-16%20150659.png?version=1&#x26;modificationDate=1686902849000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* **BILLING INFORMATION**: cho bạn các thông tin về Billing cho RDS Instance này.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2019-6-24_14-41-48.png?version=1&#x26;modificationDate=1561362109000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### B - Giao diện quản lý Backup <a href="#quanlythongtinrdsinstance-b-giaodienquanlybackup" id="quanlythongtinrdsinstance-b-giaodienquanlybackup"></a>

Giao diện quản lý Backup cho bạn cái nhìn tổng quan về tất cả các bản Backup hiện có cũng như thông chi tiết cho từng bản Backup (vùng số 3).

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2019-6-24_14-34-13.png?version=1&#x26;modificationDate=1561361653000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Bạn có thể tạo mới bản Manual Backup thông qua nút **CREATE BACKUP** (Nút số 1). Khi click chọn một Backup, bạn có thể thực hiện các **ACTION** như **RESTORE** (khôi phục lại một RDS Instance mới dựa trên bản Backup này), **DELETE** (xóa bản Backup). (Vùng số 2). Cách tạo backup và thực hiện restore bạn xem tiếp tại bài viết sau.

\


Nếu dung lượng lưu trữ bản backup miễn phí (Free Backup Storage Quota) của bạn đã đầy. Bạn có thể click chọn mua thêm ở mục **Buy Backup Storage**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2023-6-16_15-15-38.png?version=1&#x26;modificationDate=1686903338000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Sau khi mua, bạn có thể theo dõi dung lượng đã sử dụng, **Resize** hay **Delete** Paid Backup Storagre này.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2023-6-16_15-17-6.png?version=1&#x26;modificationDate=1686903427000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


### C- Giao diện quản lý Configuration Group <a href="#quanlythongtinrdsinstance-c-giaodienquanlyconfigurationgroup" id="quanlythongtinrdsinstance-c-giaodienquanlyconfigurationgroup"></a>

Configuration Group là tập hợp các biến cấu hình dịch vụ cơ sở dữ liệu của RDS Instance. Thay vì phải sửa file cấu hình và restart dịch vụ như cách truyền thống, khi sử dụng vDBaaS bạn có thể thay đổi chỉ bằng vài thao tác nhanh với Configuration Group. Tiện lợi hơn nữa, một Configuration Group có thể được cấu hình cho nhiều RDS Instance. Bạn có thể cấu hình một lần và áp dụng cho hàng loạt RDS Instance.

Giao diện quản lý Configuration Group liệt kê tất cả các Configuration Group hiện có cũng như thông tin loại **Database Engine** và **Engine Version** có thể áp dụng Configuration Group này cũng như các RDS Instance đang liên kết (**Associated RDS Instances**).

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2019-6-24_14-34-26.png?version=1&#x26;modificationDate=1561361667000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Bạn có thể tạo Configuration Group mới cũng như **DELETE** khi tick chọn từng Configuration Group. Khi bấm vào từng Configuration Group Name, bạn có xem tất cả các biến cấu hình cũng như **EDIT** và áp dụng các biến này (**APPLY CHANGES**) xuống các RDS Instance đang được liên kết. Chi tiết cách sử dụng Configuration Group, bạn có thể tham khảo bài viết "Cách sử dụng Configuration Group".

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723044/image2019-6-24_14-49-15.png?version=1&#x26;modificationDate=1561362556000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
