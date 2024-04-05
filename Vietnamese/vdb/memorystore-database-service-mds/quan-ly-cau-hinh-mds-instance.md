# Quản lý cấu hình MDS Instance

**Configuration Group** là tập hợp các biến cấu hình dịch vụ cơ sở dữ liệu của MDS Instance. Thay vì phải sửa file cấu hình và restart dịch vụ như cách truyền thống, bạn có thể thay đổi chỉ bằng vài thao tác nhanh với Configuration Group. Tiện lợi hơn nữa, một Configuration Group có thể được cấu hình cho nhiều MDS Instance. Bạn có thể cấu hình một lần và áp dụng cho hàng loạt MDS Instance.

Bạn truy cập dịch vụ MemoryStore database và chuyển sang mục Configuration Group để đến với giao diện quản lý Configuration Groups.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_10-54-46.png?version=1&#x26;modificationDate=1582257286000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* [A - Khởi tạo Configuration Group](quan-ly-cau-hinh-mds-instance.md#quanlycauhinhmdsinstance-a-khoitaoconfigurationgroup)
* [B - Chỉnh sửa các biến cấu hình](quan-ly-cau-hinh-mds-instance.md#quanlycauhinhmdsinstance-b-chinhsuacacbiencauhinh)
* [C - Liên kết MDS Instance với Configuration Groups](quan-ly-cau-hinh-mds-instance.md#quanlycauhinhmdsinstance-c-lienketmdsinstancevoiconfigurationgroups)

### A - Khởi tạo Configuration Group <a href="#quanlycauhinhmdsinstance-a-khoitaoconfigurationgroup" id="quanlycauhinhmdsinstance-a-khoitaoconfigurationgroup"></a>

Để khởi tạo một Configuration Group, bạn nhấn **CREATE CONFIGURATION GROUP**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_10-57-52.png?version=1&#x26;modificationDate=1582257472000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Tại màn hình khởi tạo, bạn có thể cấu hình:

* **Configuration Group Name**: tên của Configuration Group.
* **Engine**: loại Database Engine có thể áp dụng Configuration Group này.
* **Engine Version**: loại Engine Version có thể áp dụng Configuration Group này. Chỉ các MDS Instance có Database Engine & Version phù hợp với Version này mới có thể áp dụng Configuration Group này.
* **Descriptions**: thông tin mô tả cho Configuration Group này.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_10-58-35.png?version=1&#x26;modificationDate=1582257516000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Sau khi chắc chắn các thông tin đã chính xác, bạn nhấn **CREATE CONFIGURATION GROUP** ở góc phải trên và bạn sẽ thấy Configuration Group đã được tạo ra.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_10-59-2.png?version=1&#x26;modificationDate=1582257543000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


### B - Chỉnh sửa các biến cấu hình <a href="#quanlycauhinhmdsinstance-b-chinhsuacacbiencauhinh" id="quanlycauhinhmdsinstance-b-chinhsuacacbiencauhinh"></a>

Để cấu hình các giá trị của Configuration Group, bạn nhấp chuột trái vào tên của Configuration Group. Tại đây, bạn có thể xem tất cả các biến cấu hình của Configuration Group này. Mỗi biến bao gồm:

* Name: tên biến
* Value: giá trị cấu hình hiện tại của biến. Mặc định, VNG Cloud không cấu hình bất kì biến nào và giữ nguyên các giá trị mặc định của Database Engine.
* Allowed Values: các giá trị được phép cấu hình cho từng biến.
* Data Type: kiểu dữ liệu của giá trị có thể áp dụng cho biến cấu hình này.

Để chỉnh sửa các biến cấu hình, tại màn hình chi tiết của Configuration Group, bạn nhấn vào **EDIT PARAMETER**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_10-59-46.png?version=1&#x26;modificationDate=1582257586000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Bạn có thể tìm kiếm nhanh các biến trong ô **SEARCH**. Tại biến muốn cấu hình, bạn nhập hoặc chọn giá trị mong muốn.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_11-0-42.png?version=1&#x26;modificationDate=1582257643000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Sau khi nhập hoặc chọn gía trị, bạn có thể nhấn **Save** ngay hoặc nhấn **Preview Changes** để xem trước các thay đổi, nếu đã chắc chắn bạn nhấn **Save** để lưu lại các thay đổi. Để hệ thống thực sự áp dụng các thay đổi, bạn nhấn **Apply Change** để hệ thống áp dụng thay đổi lên tất cả các MDS Instance đang được liên kết với **Configuration Group** này.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_11-1-16.png?version=1&#x26;modificationDate=1582257677000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Các MDS Instance đang được liên kết hay chuẩn bị được liên kết với Configuration Group này sẽ được áp dụng các giá trị mới này. Bạn quay lại màn hình quản lý Database để xem qúa trình áp dụng cấu hình mới. Nếu quá trình áp dụng thành công, MDS Instance sẽ có trạng thái ACTIVE.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_11-3-18.png?version=1&#x26;modificationDate=1582257799000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


**Lưu ý:** Trong một số truờng hợp, biến cấu hình đòi hỏi cần RESTART lại dịch vụ Database trên MDS Instance, status của MDS Instance lúc này sẽ là **RESTART\_REQUIRED**. Với VNG Cloud, bạn có thể chủ động thời điểm thực hiện thao tác này. Sau khi đã sao lưu các tác vụ trên MDS Instance, bạn click vào **ACTION**, chọn **RESTART** để hoàn tất quá trình.

### C - Liên kết MDS Instance với Configuration Groups <a href="#quanlycauhinhmdsinstance-c-lienketmdsinstancevoiconfigurationgroups" id="quanlycauhinhmdsinstance-c-lienketmdsinstancevoiconfigurationgroups"></a>

Để liên kết MDS Instance với Configuration Group đã có, bạn có hai phương án:

* Liên kết ngay khi MDS Instance được khởi tạo.
* Thực hiện thay đổi cấu hình MDS Instance.

Đối với phương án 1, mời bạn xem lại hướng dẫn [Khởi tạo MDS Instance](https://docs.vngcloud.vn/pages/viewpage.action?pageId=13010707).

Đối với phương án 2, bạn có thể thực hiện như sau.

Đầu tiên, bạn đến màn hình quản lý Database, chọn đến MDS Instance và nhấn **EDIT DATABASE**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_11-3-56.png?version=1&#x26;modificationDate=1582257837000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Tại màn hình thay đổi cấu hình MDS Instance, bạn kéo tới mục **CHANGE CONFIGURATION GROUP**. Tại mục **New Configuration Group**, bạn chọn đến Configuration Group đã tạo ở trên.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_11-4-25.png?version=1&#x26;modificationDate=1582257866000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Khi mọi lựa chọn đã chính xác, bạn nhấn nút **SAVE** ở góc phải trên cùng. Bạn chờ một lát để các biến cấu hình được áp dụng xuống MDS Instance và nếu quá trình thay đổi thành công, MDS Instance sẽ có trạng thái ACTIVE.

<figure><img src="https://docs.vngcloud.vn/download/attachments/13010785/image2020-2-21_11-5-2.png?version=1&#x26;modificationDate=1582257903000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
**Lưu ý:** Trong một số truờng hợp, biến cấu hình đòi hỏi cần RESTART lại dịch vụ Database trên MDS Instance, status của MDS Instance lúc này sẽ là **RESTART\_REQUIRED**. Với VNG Cloud, bạn có thể chủ động thời điểm thực hiện thao tác này. Sau khi đã sao lưu các tác vụ trên MDS Instance, bạn click vào **ACTION**, chọn **RESTART** để hoàn tất quá trình.

\
