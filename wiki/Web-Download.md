 **Giới thiệu:**  Web Download được dùng khi bạn có nhu cầu cải thiện tốc độ load các resources của web (như image, CSS, HTML 5 audio / video, ...). 

Để sử dụng Web Download bạn cần thực hiện 2 việc như sau 


* Khởi tạo Web Download tại [portal.vngcloud.vn](https://portal.vngcloud.vn/). 
* Thay thế các link resource hiện tại trên website của bạn bằng link Web Download / cname vừa tạo ở trên. 

Để khởi tạo Web Download tại [portal.vngcloud.vn](https://portal.vngcloud.vn) bạn cần tài khoản [vngcloud.vn](https://vngcloud.vn/) và credit. Nếu chưa có , có thể đăng ký tại [vngcloud.vn](https://vngcloud.vn/) 

Sau khi có tài khoản Vng Cloud, bạn cần đăng nhập vào [portal.vngcloud.vn](https://portal.vngcloud.vn/) và thực hiện theo các bước bên dưới. 

 **Bước 1:**  Tại tab "vCDN - Media service" chọn Web Download

![](images/storage/image2020-1-13_11-47-35.png)



 **Bướ**  **c 2:** Click nút “ **Create CDN** ” ở màn hình liệt kê các đối tượng đã tạo để tạo mới vCDN Web Download

![Tạo Web Accelerator](images/storage/WEB_ACC_2.jpg)

 **Bướ**  **c 3:** Nhập các thông tin để thiết lập Original

![Thiết lập Original Settings](images/storage/WEB_ACC_3.jpg)


1.  **Origin domain name** : 






1.  **Origin ID:**  vCDN sẽ khởi tạo ID tương ứng 


1.  **Enable HTTPS Origin:**  Nếu domain dùng giao thức HTTPS thì chọn vào ô này 


1.  **Available origins:**  Nếu có nhiều origin chọn vào đây để nhập. Lưu ý tại đây sẽ chỉ được nhập IP:PORT. Sau khi nhập cần tab / enter để hệ thống có thể nhận. 



 **Bước 4** : Thiết lập thông số cho vCDN 

![Thiết lập CDN Settings](images/storage/WEB_ACC_4.jpg)


*  **CDN name:** Đặt tên gợi nhớ giúp bạn quản lý khi có nhiều CDN domains khác nhau. 


*  **Only Cache resources:** Lựa chọn loại resource mà bạn chỉ muốn cache


*  **Region:** Chọn Việt Nam


*  **Alternate domain names (CNAMES) :** Tên domain mà end-user sẽ truy cập tới để xem nội dung. Ví dụ: testing.vcdn.vn


*  **TTL:** thời gian cache tối đa trên hệ thống.


*  **Protocols** :


    * Gồm 2 lựa chọn là HTTP và HTTPS. 


    * Với HTTPS cần chọn thêm SSL theo nhu cầu



    

![Default Certificate](images/storage/CERT_DEFAULT.jpg)

Default CDN certificate

![Custom Certificate](images/storage/CERT_CUSTOM.jpg)

Custom SSL certificate


*  **CDN state** : Chọn disable hoặc enable CDN tại đây. 


*  **Comment**  (optional) 



 **Bước 5:** Thiết lập các rule cho cache 

Chọn add rule để thêm mới. Hiện vCDN không giới hạn số lượng rule có thể tạo

![Add Rule](images/storage/RULE_ADD.jpg)

Với mỗi rule có thể đặt nhiều điều kiện và xếp thứ tự ưu tiên bằng cách nhấn vào mũi tên để di chuyển.

Cụ thể hơn về cách thức hoạt động của Rule, bạn có thể tham khảo: [Hướng dẫn thiết lập Rule cho CDN](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2721278)

![Add Rule](images/storage/RULE_MORE.jpg)

 **Bước 6:**  Chọn “ **Create New** ” -> Để tạo một vCDN Web Download mới

![Click Create New Button](images/storage/WEB_ACC_CREATE.jpg)

Sau đó, màn hình sẽ được tự động chuyển sang trang chính. Sau đó, bạn sẽ nhận được thông báo như sau thể hiện quá trình tạo CDN thành công.

![Thông báo thành công](images/storage/WEB_ACC_SUCCESS.jpg)

Màn hình hiển thị đã khởi tạo thành công.

![](images/storage/WEB_ACC_SUCCESS_2.jpg)





Theo bạn thì bài hướng dẫn này có giúp ích cho bạn không? Nếu bạn có thắc mắc, vui lòng liên hệ hotline 1900 54 55 69 hoặc email [support@vngcloud.vn](mailto:support@vngcloud.vn) của vCDN để được hỗ trợ nhé.



*****

[[category.storage-team]] 
[[category.confluence]] 
