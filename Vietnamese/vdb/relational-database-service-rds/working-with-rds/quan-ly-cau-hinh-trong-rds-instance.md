# Quản lý cấu hình trong RDS Instance

**Configuration Group** là tập hợp các biến cấu hình dịch vụ cơ sở dữ liệu của RDS Instance. Thay vì phải sửa file cấu hình và restart dịch vụ như cách truyền thống, bạn có thể thay đổi chỉ bằng vài thao tác nhanh với Configuration Group. Tiện lợi hơn nữa, một Configuration Group có thể được cấu hình cho nhiều RDS Instance. Bạn có thể cấu hình một lần và áp dụng cho hàng loạt RDS Instance.

Bạn truy cập dịch vụ vDBaaS và chuyển sang mục Configuration Group để đến với giao diện quản lý Configuration Groups.

* [A - Khởi tạo Configuration Group](quan-ly-cau-hinh-trong-rds-instance.md#quanlycauhinhtrongrdsinstance-a-khoitaoconfigurationgroup)
* [B - Chỉnh sửa các biến cấu hình](quan-ly-cau-hinh-trong-rds-instance.md#quanlycauhinhtrongrdsinstance-b-chinhsuacacbiencauhinh)
* [C - Liên kết RDS Instance với Configuration Groups](quan-ly-cau-hinh-trong-rds-instance.md#quanlycauhinhtrongrdsinstance-c-lienketrdsinstancevoiconfigurationgroups)

### A - Khởi tạo Configuration Group <a href="#quanlycauhinhtrongrdsinstance-a-khoitaoconfigurationgroup" id="quanlycauhinhtrongrdsinstance-a-khoitaoconfigurationgroup"></a>

Để khởi tạo một Configuration Group, bạn nhấn **CREATE CONFIGURATION GROUP**.

Tại màn hình khởi tạo, bạn có thể cấu hình:

* **Configuration Group Name**: tên của Configuration Group.
* **Engine**: loại Database Engine có thể áp dụng Configuration Group này.
* **Engine Version**: loại Engine Version có thể áp dụng Configuration Group này. Chỉ các RDS Instance có Database Engine & Version phù hợp với Version này mới có thể áp dụng Configuration Group này.
* **Descriptions**: thông tin mô tả cho Configuration Group này.

Sau khi chắc chắn các thông tin đã chính xác, bạn nhấn nút **CREATE** và bạn sẽ thấy Configuration Group đã được tạo ra.

Để cấu hình các giá trị của Configuration Group, bạn nhấp chuột trái vào tên của Configuration Group. Tại đây, bạn có thể xem tất cả các biến cấu hình của Configuration Group này. Mỗi biến bao gồm:

* Name: tên biến
* Value: giá trị cấu hình hiện tại của biến. Mặc định, GreenNode không cấu hình bất kì biến nào và giữ nguyên các giá trị mặc định của Database Engine.
* Allowed Values: các giá trị được phép cấu hình cho từng biến.
* Data Type: kiểu dữ liệu của giá trị có thể áp dụng cho biến cấu hình này.

### B - Chỉnh sửa các biến cấu hình <a href="#quanlycauhinhtrongrdsinstance-b-chinhsuacacbiencauhinh" id="quanlycauhinhtrongrdsinstance-b-chinhsuacacbiencauhinh"></a>

Để chỉnh sửa các biến cấu hình, tại màn hình chi tiết của Configuration Group, bạn nhấn vào **EDIT PARAMETER**.

Bạn nhập hoặc chọn giá trị vào biến muốn cấu hình. Bạn có thể tìm kiếm nhanh các biến trong ô **SEARCH**.

Sau khi nhập hoặc chọn gía trị, bạn có thể nhấn **Save** ngay hoặc nhấn **Preview Changes** để xem trước các thay đổi, nếu đã chắc chắn bạn nhấn **Save Changes** để lưu lại các thay đổi. Để hệ thống thực sự áp dụng các thay đổi, bạn nhấn **Apply Change** để hệ thống áp dụng thay đổi lên tất cả các RDS Instance đang được liên kết với **Configuration Group** này.

Các RDS Instance đang được liên kết hay chuẩn bị được liên kết với Configuration Group này sẽ được áp dụng các giá trị mới này. Bạn quay lại màn hình quản lý Database để xem qúa trình áp dụng cấu hình mới. Nếu quá trình áp dụng thành công, RDS Instance sẽ có trạng thái ACTIVE.

**Lưu ý:** Trong một số truờng hợp, biến cấu hình đòi hỏi cần RESTART lại dịch vụ Database trên RDS Instance, status của RDS Instance lúc này sẽ là **RESTART\_REQUIRED**. Với GreenNode, bạn có thể chủ động thời điểm thực hiện thao tác này. Sau khi đã sao lưu các tác vụ trên RDS Instance, bạn click vào **ACTION**, chọn **RESTART** để hoàn tất quá trình.

### C - Liên kết RDS Instance với Configuration Groups <a href="#quanlycauhinhtrongrdsinstance-c-lienketrdsinstancevoiconfigurationgroups" id="quanlycauhinhtrongrdsinstance-c-lienketrdsinstancevoiconfigurationgroups"></a>

Để liên kết RDS Instance với Configuration Group đã có, bạn có hai phương án:

* Liên kết ngay khi RDS Instance được khởi tạo.
* Thực hiện thay đổi cấu hình RDS Instance.

Đối với phương án 1, mời bạn xem lại hướng dẫn [Khởi tạo RDS Instance](khoi-tao-rds-instance.md).

Đối với phương án 2, bạn có thể thực hiện như sau.

Đầu tiên, bạn đến màn hình quản lý Database, chọn RDS Instance bạn muốn cấu hình bằng cách nhấn vào icon ba chấm và nhấn chọn **Edit Configuration Group** hoặc bạn có thể vào chi tiết RDS Instance và chọn icon **Edit Configuration Group (góc bên phải phía trên)**

<figure><img src="../../.gitbook/assets/image (443).png" alt=""><figcaption></figcaption></figure>

Tại mục **DB configuration group**, bạn chọn Configuration Group đã tạo ở trên.

Khi mọi lựa chọn đã chính xác, bạn nhấn nút **SAVE** . Bạn chờ một lát để các biến cấu hình được áp dụng xuống RDS Instance và nếu quá trình thay đổi thành công, RDS Instance sẽ có trạng thái ACTIVE.

**Lưu ý:** Trong một số truờng hợp, biến cấu hình đòi hỏi cần RESTART lại dịch vụ Database trên RDS Instance, status của RDS Instance lúc này sẽ là **RESTART\_REQUIRED**. Với GreenNode, bạn có thể chủ động thời điểm thực hiện thao tác này. Sau khi đã sao lưu các tác vụ trên RDS Instance, bạn click vào **ACTION**, chọn **RESTART** để hoàn tất quá trình.

<br>
