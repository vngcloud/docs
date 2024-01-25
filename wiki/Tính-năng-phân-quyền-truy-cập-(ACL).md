Bạn có thể cấp quyền Đọc hoặc Đọc + Ghi cho 1 hoặc tất cả user khác. Lưu ý: Người được cấp quyền phải có tài khoản vngcloud 


* Đối với quyền đọc (read): user có thể đọc , tải các object từ container được cấp quyền
* Đối với quyền Ghi (write): user có thêm quyền upload object mới lên container và đồng thời cũng có quyền đọc dữ liệu. (Read + Write)

Để thiết lập phân quyền, có thể thực hiện theo các bước sau 

 **Bước 1:**  Chọn container → Chọn ACL → Chọn add account

![](images/storage/image2020-12-11_14-58-18.png)

 **Bước 2:** Thêm account bằng cách  nhập số điện thoại hoặc email. 

![](images/storage/image2020-4-13_16-43-50.png)

Lưu ý tính năng này chỉ cho phép cấp quyền cho 1 user [portal.vngcloud.vn](http://portal.vngcloud.vn) khác. Nên nếu sđt / email chưa được đăng ký thì sẽ không thêm được 

 **Bước 3:**  Cấp quyền read hoặc wirte. 

![](images/storage/image2020-12-11_14-58-55.png)

Tương tự với Everyone, có thể chọn quyền cho tất cả mọi người

![](images/storage/image2020-12-11_15-1-11.png)

 **Bước 4:**  Chọn update để hoàn tất

![](images/storage/image2020-12-11_14-59-31.png)

Với trường hợp update rule cho Everyone ta cần phải make public container

![](images/storage/image2020-12-11_15-11-7.png)

Allow public access

![](images/storage/image2020-12-11_15-12-28.png)



 **Bước 5** : Kiểm tra lại danh sách ACL trong container , tài khoản mới được add sẽ hiện ra trong danh sách cùng với quyền đã được cấp. 

![](images/storage/image2020-12-11_15-5-27.png)













*****

[[category.storage-team]] 
[[category.confluence]] 
