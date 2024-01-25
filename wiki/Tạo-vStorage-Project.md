 **Hướng dẫn tạo Project**  **Bước 1:**  Đăng nhập vào [portal.vngcloud.vn](http://portal.vinadata.vn). Nếu bạn chưa có tài khoản, đăng ký miễn phí tại [https://portal.vngcloud.vn/register.html](https://portal.vinadata.vn/register.html)

 **Bước 2: ** Chọn Object Storage tại tab vStorage

![](images/storage/image2022-4-19_10-39-56.png)

 **Bước 3: Tạo project** 

Chọn Region (Vùng) 

Tại tab account,  **chọn Region**  theo nhu cầu sử dụng và chọn  **"Add project"** 

![](images/storage/image2020-4-8_15-49-11.png)


* Vị trí gần hơn thì sẽ hỗ trợ tốc độ tốt hơn.
* Hiện tại vStorage chỉ đang hỗ trợ 2 regions là HCM01 và HAN01

Tại trang tạo project, nhập các thông tin: 

![](images/storage/image2022-9-6_13-34-58.png)




1.  **Project Name** 
    * Lưu ý: tên của project trong Region không được trùng nhau. Ví dụ Region HCM 01 có project 1 rồi, thì user sẽ không được đặt tên project 1 nữa. Vì vậy VNG Cloud khuyến khích user sử dụng tên project / sản phẩm của để đặt

    

     2.  **Ch**  **ọ**  **n các gói có s**  **ẵ**  **n ho**  **ặ**  **c Customize theo nhu c**  **ầ**  **u ** 


* Dung lượng: Được tính theo GB.  
* Chọn class 
    * Gold: Phù hợp với nhu cầu lưu trữ media, làm original cho CDN, có lượng lớn người truy cập. 
    * Silver: Phù hợp với nhu cầu lưu trữ backup, các dữ liệu không có lượng truy cập quá lớn. 
    * Archive: Phù hợp với nhu cầu lưu trữ lâu dài, tối thiểu 6 tháng, ít sử dụng. 

    



 **3. Price quota monthly: ** Tùy theo lựa chọn ở bước 2, thông tin về tổng giá tiền thanh toán sẽ liệt kê ở đây. Ngoài ra bạn cũng có thể lựa chọn thời gian sử dụng từ 1 tháng đến 1 năm tùy theo nhu cầu. 

Sau khi hoàn tất lựa chọn, nhấn add project để tiếp tục. Bạn sẽ thấy pop up như hình dưới:

Xác nhận lại các thông tin về quota và thời hạn sử dụng, nếu thông tin chính xác nhấn chọn OK để đưa vào giỏ hàng 

![](images/storage/image2021-5-7_17-10-25.png)

Tại giỏ hàng chọn pay để tiếp tục đến thông tin thanh toán (payment information)

Tại payment information, nếu bạn có sẵn balance thì tick chọn vào option "Using the available balance ..... to pay" và chọn Pay để hoàn tất thanh toán 

Nếu chưa có sẵn balance, chọn Pay bạn sẽ được đưa đến giao diện nạp tiền vào tài khoản VNG Cloud (thêm balance) 

Sau khi thanh toán thành công Project vừa tạo sẽ hiện ra như hình dưới:

![](images/storage/image2019-5-23_23-20-14.png)

 **L**  **ư**  **u ý: ** 

 **V**  **ớ**  **i l**  **ầ**  **n đ**  **ầ**  **u tiên t**  **ạ**  **o project trong 1 Region** , User sẽ nhận 1 email gửi username & password đến email đăng ký tài khoản portal VNG Cloud như bên dưới

![](images/storage/image2019-5-23_23-20-25.png)

Khi user sử dụng Swift client tool truy cập object storage sẽ cần input username & pass này.

Tương ứng với mỗi region sẽ có 1 cặp user name & password dùng để lấy quyền truy cập vào project trong region



*****

[[category.storage-team]] 
[[category.confluence]] 
