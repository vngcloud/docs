VNG Cloud cung cấp các giao diện (dashboard) giúp bạn quản lý các Database (hay DB Instance), các bản Backup & các Configuration Group một cách hiệu quả và tiện dụng.

![](images/storage/image2020-2-21_10-26-8.png)



Hãy cùng điểm qua các Dashboard này.



A - Giao diện quản lý DatabaseGiao diện quản lý Database cho phép bạn có cái nhìn tổng quát về tất cả các Database (DB Instance) hiện có cũng như thông tin chi tiết cho từng DB Instance. Bạn có thể thực hiện tạo mới một Database khi click chọn  **CREATE DATABASE**  (Nút số 1).

![](images/storage/image2020-2-21_10-29-26.png)



Khi bạn click chọn từng DB Instance, bạn có thể:


* Thực hiện các  **ACTION** quản lý vòng đời của DB Instance như:  **START** ,  **STOP** ,  **RESTART** hay  **DELETE** . (Vùng số 2).
* Thay đổi các thông tin cấu hình của DB Instance tại  **EDIT DATABASE** . (Nút số 3).
* Xem chi tiết thông tin cấu hình từng DB Instance (Vùng số 4).



Tại vùng số 4, bạn sẽ có 4 tab quản lý:


*  **CONFIGURATION** : bao gồm thông tin tổng quan về DB Instance như  **DB Name** , loại  **Database Engine** ,  **Engine Version**  cũng như thông tin cấu hình tính toán, bộ nhớ và lưu trữ.

![](images/storage/image2020-2-21_10-30-39.png)




*  **CONNECTIVITY & SECURITY:**  cho bạn các thông tin về  **Endpoint & Port** để kết nối đến. Mọi DB Instance sẽ có một  **Private Endpoint** tương ứng với  **Cloud Network** . Nếu bạn có chọn  **Enable Public Accessibility** trong quá khởi tạo, bạn sẽ có thêm một  **Public Endpoint**  cho phép truy cập từ Internet. Bên cạnh đó, bạn có thể giới hạn những địa chỉ IP tin cậy mới được truy cập DB Instance thông qua  **Security Group Rules** .

![](images/storage/image2020-2-21_10-31-15.png)




*  **BACKUP** : cho bạn thông tin về cấu hình  **Daily Automatic Backup**  cũng như thời điểm thực hiện  **Daily Automatic Backup**  (nếu có). Ngoài ra, mục  **Backup list**  cũng liệt kê toàn bộ các bản Backup tương ứng với DB Instance này. Bạn cũng có thể thực hiện tạo Manual Backup thông qua nút  **Create Backup.** 

![](images/storage/image2020-2-21_10-31-35.png)




*  **BILLING INFORMATION** : cho bạn các thông tin về Billing cho DB Instance này.

![](images/storage/image2020-2-21_10-31-55.png)



B - Giao diện quản lý BackupGiao diện quản lý Backup cho bạn cái nhìn tổng quan về tất cả các bản Backup hiện có cũng như thông chi tiết cho từng bản Backup (vùng số 3).

![](images/storage/image2020-2-21_10-34-59.png)



Bạn có thể tạo mới bản Manual Backup thông qua nút  **CREATE BACKUP**  (Nút số 1). Khi click chọn một Backup, bạn có thể thực hiện các  **ACTION** như  **RESTORE** (khôi phục lại một DB Instance mới dựa trên bản Backup này),  **DELETE** (xóa bản Backup). (Vùng số 2). Cách tạo backup và thực hiện restore bạn xem tiếp tại bài viết sau



C- Giao diện quản lý Configuration GroupConfiguration Group là tập hợp các biến cấu hình dịch vụ cơ sở dữ liệu của DB Instance. Thay vì phải sửa file cấu hình và restart dịch vụ như cách truyền thống, khi sử dụng vDBaaS bạn có thể thay đổi chỉ bằng vài thao tác nhanh với Configuration Group. Tiện lợi hơn nữa, một Configuration Group có thể được cấu hình cho nhiều DB Instance. Bạn có thể cấu hình một lần và áp dụng cho hàng loạt DB Instance.

Giao diện quản lý Configuration Group liệt kê tất cả các Configuration Group hiện có cũng như thông tin loại  **Database Engine**  và  **Engine Version**  có thể áp dụng Configuration Group này cũng như các DB Instance đang liên kết ( **Associated DB Instances** ).

![](images/storage/image2020-2-21_10-35-41.png)



Bạn có thể tạo Configuration Group mới cũng như  **DELETE** khi tick chọn từng Configuration Group. Khi bấm vào từng Configuration Group Name, bạn có xem tất cả các biến cấu hình cũng như  **EDIT** và áp dụng các biến này ( **APPLY CHANGES** ) xuống các DB Instance đang được liên kết. Chi tiết cách sử dụng Configuration Group, bạn có thể tham khảo bài viết "Cách sử dụng Configuration Group".

![](images/storage/image2020-2-21_10-36-7.png)







*****

[[category.storage-team]] 
[[category.confluence]] 
