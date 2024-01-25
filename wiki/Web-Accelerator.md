 **Tổng quan** Web Accelerator là giải pháp giúp tăng tốc độ hiển thị nội dung và trải nghiệm người dùng.

 **Sơ đồ hoạt động** ![](images/storage/)

 **Cơ Chế Phân Phối Dữ Liệu** Dịch vụ Web Accelerator cache tất cả các đối tượng đi qua nó không chỉ bao gồm các nội dung tĩnh như Image, javascript, css mà còn có cả HTML code và API. Bên cạnh đó còn thực hiện các cơ chế tự động tối ưu hóa source code và hình ảnh.

 **Tính Năng Dịch Vụ** 
* Hỗ trợ [[CNAME|CNAME]].
* Hỗ trở tùy chỉnh [[Origin|Origin]].
* Hỗ trợ [[tối ưu hóa kích thước file thiết bị đầu cuối|Tối-Ưu-Hóa-Kích-Thước-File-Thiết-Bị-Đầu-Cuối]].
* Hỗ trợ chế độ bảo mật [[HSTS|Tính-Năng-Bảo-Mật-HSTS]].
* Hỗ trợ tùy chỉnh các [[tính năng cache|Tùy-Chỉnh-Các-Tính-Năng-Cache]].
* Hỗ trợ [[tự động redirect từ HTTP sang HTTPS|Tự-Động-Redirect-Từ-HTTP-Sang-HTTPS]].
* Hỗ trợ [[đổi các link HTTP sang HTTPS trong source code|Chuyển-đổi-các-link-HTTP-sang-HTTPS-trong-source-code]].
* Hỗ trợ [[chỉnh sửa CDN đã tạo|Chỉnh-Sửa-CDN-Đã-Tạo]].

 **Cách Tạo Web accelerator CDN** 
* Bước 1: Chọn menu Web accelerator bạn sẽ vô trang thống kê và chỉnh sửa cho Web Accelerator, Chọn button Create để tạo CDN.

![](images/storage/image2023-8-15_11-31-56.png)


* Bước 2: Nhập và tùy chọn tính năng dịch vụ Web Accelerator

![](images/storage/image2023-8-15_11-32-23.png)


* Bước 3: Nhập Domain Name cho CDN khi người dùng nhập domain có sẵn của mình hệ thống sẽ tự tìm và thêm server ở tùy chọn origin. Ví dụ: người dùng có domain “[vnexpress.net](http://vnexpress.net)” thì khi nhập xong chọn ra một field khác sẽ tự dộng thêm server có IP là “111.65.250.2”.


* Bước 4: Nhập và tùy chỉnh các tính năng dịch vụ.
* Bước 5: Tùy theo người dùng yêu cầu nhập thông [[tin chính sách rule cơ bản|Chính-Sách-Rule-Cơ-Bản-(PageRule)]] hoặc [[chính sách rule nâng cao|Chính-Sách-Rule-Nâng-Cao-(AdvanceRule)]] cho CDN.
* Bước 6: Khi điền các thông tin đúng và đủ thì nhấn button Submit ở cuối cùng giao diện đợi khoản 5 phút cho hệ thống cái đặt CDN cho người dùng.
* Bước 7: Người dùng có thể truy cập CDN qua vCDN Domain khi đã tạo CDN xong.



*****

[[category.storage-team]] 
[[category.confluence]] 
