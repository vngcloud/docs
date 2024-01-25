vMarketplace cung cấp nhiều ứng dụng (app) đã được build sẵn giúp bạn có thể ngay lập tức khởi tạo và cài đặt lên vServer chỉ trong vài bước

 **Bước 1** : Vào giao diện marketplace [https://sdn-portal.vngcloud.vn/mp/marketplace.html](https://sdn-portal.vngcloud.vn/mp/marketplace.html) 

 **Bước 2:**  Chọn app 

![](images/storage/image2019-9-24_0-38-47.png)

 **Bước 3:**  Chọn launch on compute engine. 

![](images/storage/image2019-9-24_0-39-40.png)

 **Bước 4:**  Cấu hình server 


* App name: Mặc định sẽ là tên app và phiên bản, đây cũng là tên server sau khi khởi tạo. 
* OS Image: Hệ điều hành của server 
* Flavor: Mặc định các app đều tương thích với cấu hình nhỏ nhất của Server (1 Core & 1 Ram). 
* Volume: Ổ đĩa boot, tối thiểu 20GB 

![](images/storage/image2019-9-24_0-42-18.png)


* Network setting: Chọn 1 network theo nhu cầu. 
* Security setting: Hiện tại marketplace chỉ cho chọn 1 security group là default. Để đảm bảo có thể kết nối đến app mình đã chọn, bạn cần mở Port (xem cách mở tại [[Access & Security|Access-&-Security]]) theo yêu cầu từng app (xem danh sách port theo app tại [[vMarketplace|vMarketplace]]). 

![](images/storage/image2019-9-24_0-52-5.png)

 **Bước 5:**  Kiểm tra lại thông tin và thực hiện thanh toán 

Chi phí sử dụng marketplace sẽ bao gồm chi phí license của app (nếu có) và chi phí vServer (Flavor + Volume). Hiện tại 100% các app của marketplace đều miễn phí 

Sau khi thanh toán xong, bạn sẽ được redirect về giao diện quản lý vServer, vui lòng đợi 5-10p để server được khởi tạo và app được cài đặt thành công 

![](images/storage/image2019-9-24_0-59-31.png)

 **Bước 6:**  Sau khi hoàn tất cài đặt, bạn có thể thử truy cập ip của ứng dụng để kiểm tra 

![](images/storage/image2019-9-24_1-1-4.png)

Lưu ý: nếu không truy cập được vui lòng kiểm tra lại security group đã cho phép truy cập port tương ứng của app chưa. 

Sau khi truy cập được ứng dụng thành công là đã hoàn tất









*****

[[category.storage-team]] 
[[category.confluence]] 
