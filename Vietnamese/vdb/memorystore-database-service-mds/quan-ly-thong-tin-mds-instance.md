# Quản lý thông tin MDS Instance

VNG Cloud cung cấp các giao diện (dashboard) giúp bạn quản lý các Database (hay DB Instance), các bản Backup & các Configuration Group một cách hiệu quả và tiện dụng.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010741/image2020-2-21_10-26-8.png?version=1&#x26;modificationDate=1582255568000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Hãy cùng điểm qua các Dashboard này.

* [A - Giao diện quản lý Database](quan-ly-thong-tin-mds-instance.md#quanlythongtinmdsinstance-a-giaodienquanlydatabase)
*
*

### A - Giao diện quản lý Database <a href="#quanlythongtinmdsinstance-a-giaodienquanlydatabase" id="quanlythongtinmdsinstance-a-giaodienquanlydatabase"></a>

Giao diện quản lý Database cho phép bạn có cái nhìn tổng quát về tất cả các Database (DB Instance) hiện có cũng như thông tin chi tiết cho từng DB Instance. Bạn có thể thực hiện tạo mới một Database khi click chọn **CREATE DATABASE** (Nút số 1).

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010741/image2020-2-21_10-29-26.png?version=1&#x26;modificationDate=1582255767000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Khi bạn click chọn từng DB Instance, bạn có thể:

* Thực hiện các **ACTION** quản lý vòng đời của DB Instance như: **START**, **STOP**, **RESTART** hay **DELETE**. (Vùng số 2).
* Thay đổi các thông tin cấu hình của DB Instance tại **EDIT DATABASE**. (Nút số 3).
* Xem chi tiết thông tin cấu hình từng DB Instance (Vùng số 4).\


Tại vùng số 4, bạn sẽ có 4 tab quản lý:

* **CONFIGURATION**: bao gồm thông tin tổng quan về DB Instance như **DB Name**, loại **Database Engine**, **Engine Version** cũng như thông tin cấu hình tính toán, bộ nhớ và lưu trữ.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010741/image2020-2-21_10-30-39.png?version=1&#x26;modificationDate=1582255839000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


* **CONNECTIVITY & SECURITY:** cho bạn các thông tin về **Endpoint & Port** để kết nối đến. Mọi DB Instance sẽ có một **Private Endpoint** tương ứng với **Cloud Network**. Nếu bạn có chọn **Enable Public Accessibility** trong quá khởi tạo, bạn sẽ có thêm một **Public Endpoint** cho phép truy cập từ Internet. Bên cạnh đó, bạn có thể giới hạn những địa chỉ IP tin cậy mới được truy cập DB Instance thông qua **Security Group Rules**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010741/image2020-2-21_10-31-15.png?version=1&#x26;modificationDate=1582255876000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



* **BACKUP**: cho bạn thông tin về cấu hình **Daily Automatic Backup** cũng như thời điểm thực hiện **Daily Automatic Backup** (nếu có). Ngoài ra, mục **Backup list** cũng liệt kê toàn bộ các bản Backup tương ứng với DB Instance này. Bạn cũng có thể thực hiện tạo Manual Backup thông qua nút **Create Backup.**

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010741/image2020-2-21_10-31-35.png?version=1&#x26;modificationDate=1582255896000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



* **BILLING INFORMATION**: cho bạn các thông tin về Billing cho DB Instance này.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010741/image2020-2-21_10-36-7.png?version=1&#x26;modificationDate=1582256168000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
