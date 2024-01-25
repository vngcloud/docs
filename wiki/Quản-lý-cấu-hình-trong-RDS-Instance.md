 **Configuration Group**  là tập hợp các biến cấu hình dịch vụ cơ sở dữ liệu của RDS Instance. Thay vì phải sửa file cấu hình và restart dịch vụ như cách truyền thống, bạn có thể thay đổi chỉ bằng vài thao tác nhanh với Configuration Group. Tiện lợi hơn nữa, một Configuration Group có thể được cấu hình cho nhiều RDS Instance. Bạn có thể cấu hình một lần và áp dụng cho hàng loạt RDS Instance.

Bạn truy cập dịch vụ vDBaaS và chuyển sang mục Configuration Group để đến với giao diện quản lý Configuration Groups.

![](images/storage/image2019-6-24_15-34-18.png)





A - Khởi tạo Configuration GroupĐể khởi tạo một Configuration Group, bạn nhấn  **CREATE CONFIGURATION GROUP** .

![](images/storage/image2019-6-24_15-34-30.png)



Tại màn hình khởi tạo, bạn có thể cấu hình:


*  **Configuration Group Name** : tên của Configuration Group.


*  **Engine** : loại Database Engine có thể áp dụng Configuration Group này.


*  **Engine Version** : loại Engine Version có thể áp dụng Configuration Group này. Chỉ các RDS Instance có Database Engine & Version phù hợp với Version này mới có thể áp dụng Configuration Group này.


*  **Descriptions** : thông tin mô tả cho Configuration Group này.



![](images/storage/image2019-6-24_15-34-52.png)



Sau khi chắc chắn các thông tin đã chính xác, bạn nhấn  **CREATE CONFIGURATION GROUP** ở góc phải trên và bạn sẽ thấy Configuration Group đã được tạo ra.

![](images/storage/image2019-6-24_15-35-10.png)



Để cấu hình các giá trị của Configuration Group, bạn nhấp chuột trái vào tên của Configuration Group. Tại đây, bạn có thể xem tất cả các biến cấu hình của Configuration Group này. Mỗi biến bao gồm:


* Name: tên biến


* Value: giá trị cấu hình hiện tại của biến. Mặc định, VNG Cloud không cấu hình bất kì biến nào và giữ nguyên các giá trị mặc định của Database Engine.


* Allowed Values: các giá trị được phép cấu hình cho từng biến.


* Data Type: kiểu dữ liệu của giá trị có thể áp dụng cho biến cấu hình này.



B - Chỉnh sửa các biến cấu hìnhĐể chỉnh sửa các biến cấu hình, tại màn hình chi tiết của Configuration Group, bạn nhấn vào  **EDIT PARAMETER** .

![](images/storage/image2019-6-24_15-35-23.png)



Bạn nhập hoặc chọn giá trị vào biến muốn cấu hình. Bạn có thể tìm kiếm nhanh các biến trong ô  **SEARCH** .

![](images/storage/image2019-6-24_15-35-38.png)



Sau khi nhập hoặc chọn gía trị, bạn có thể nhấn  **Save**  ngay hoặc nhấn  **Preview Changes**  để xem trước các thay đổi, nếu đã chắc chắn bạn nhấn  **Save Changes**  để lưu lại các thay đổi. Để hệ thống thực sự áp dụng các thay đổi, bạn nhấn  **Apply Change**  để hệ thống áp dụng thay đổi lên tất cả các RDS Instance đang được liên kết với  **Configuration Group**  này.

![](images/storage/image2019-6-24_15-35-49.png)



Các RDS Instance đang được liên kết hay chuẩn bị được liên kết với Configuration Group này sẽ được áp dụng các giá trị mới này. Bạn quay lại màn hình quản lý Database để xem qúa trình áp dụng cấu hình mới. Nếu quá trình áp dụng thành công, RDS Instance sẽ có trạng thái ACTIVE.

![](images/storage/image2019-6-24_15-36-3.png)



 **Lưu ý:**  Trong một số truờng hợp, biến cấu hình đòi hỏi cần RESTART lại dịch vụ Database trên RDS Instance, status của RDS Instance lúc này sẽ là  **RESTART_REQUIRED** . Với VNG Cloud, bạn có thể chủ động thời điểm thực hiện thao tác này. Sau khi đã sao lưu các tác vụ trên RDS Instance, bạn click vào  **ACTION** , chọn  **RESTART** để hoàn tất quá trình.

C - Liên kết RDS Instance với Configuration GroupsĐể liên kết RDS Instance với Configuration Group đã có, bạn có hai phương án:


* Liên kết ngay khi RDS Instance được khởi tạo.


* Thực hiện thay đổi cấu hình RDS Instance.



Đối với phương án 1, mời bạn xem lại hướng dẫn [Khởi tạo RDS Instance](https://docs.vinadata.vn/pages/viewpage.action?pageId=2722985).

Đối với phương án 2, bạn có thể thực hiện như sau.

Đầu tiên, bạn đến màn hình quản lý Database, chọn đến RDS Instance và nhấn  **EDIT DATABASE** .

![](images/storage/image2019-6-24_15-36-17.png)



Tại màn hình thay đổi cấu hình RDS Instance, bạn kéo tới mục  **CHANGE CONFIGURATION GROUP** . Tại mục  **New Configuration Group** , bạn chọn đến Configuration Group đã tạo ở trên.

![](images/storage/image2019-6-24_15-36-30.png)



Khi mọi lựa chọn đã chính xác, bạn nhấn nút  **SAVE** ở góc phải trên cùng. Bạn hờ một lát để các biến cấu hình được áp dụng xuống RDS Instance và nếu quá trình thay đổi thành công, RDS Instance sẽ có trạng thái ACTIVE.

![](images/storage/image2019-6-24_15-36-48.png)



 **Lưu ý:**  Trong một số truờng hợp, biến cấu hình đòi hỏi cần RESTART lại dịch vụ Database trên RDS Instance, status của RDS Instance lúc này sẽ là  **RESTART_REQUIRED** . Với VNG Cloud, bạn có thể chủ động thời điểm thực hiện thao tác này. Sau khi đã sao lưu các tác vụ trên RDS Instance, bạn click vào  **ACTION** , chọn  **RESTART** để hoàn tất quá trình.



*****

[[category.storage-team]] 
[[category.confluence]] 
