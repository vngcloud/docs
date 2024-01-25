 **Giới thiệu: ** bạn dùng VOD khi cần dịch vụ CDN để phân phối nội dung media của bạn tới người dùng cuối một cách nhanh chóng.

Bạn thực hiện các bước sau để tạo VOD

 **Bước 1:**  Tại tab "vCDN - Media service" chọn VOD

![](images/storage/VOD create.jpg)

 **Bước 2:** Click “ **Create CDN** ”

![Create VOD](images/storage/VOD_2.jpg)

 **Bước 3:** Nhập các thông tin để thiết lập CDN Original




*  **Origin domain name** : 



![Thiết lập Original Settings với Origin là vStorage](images/storage/VOD_3_2.jpg)


*  **Origin ID:**  vCDN sẽ tự khởi tạo ID tương ứng với original đã nhập bên trên. 


*  **Enable HTTPS Origin:**  Nếu domain dùng giao thức HTTPS thì chọn vào ô này 


*  **Available Origins:**  Nhập IP của các CDN Originals tại đây. 


    *  **Lưu ý**  sau khi nhập phải nhấn TAB để input có hiệu lực. Có thể nhập 1 hoặc nhiều IPs để hỗ trợ nhiều origin. 



    
*  **Enable Packaging:** vCDN sẽ hỗ trợ convert định dạng file mp4 thành file hls



 **Bước 4** : Thiết lập thông số cho vCDN VOD

![Thiết lập CDN Settings](images/storage/VOD_4.jpg)


*  **CDN name:** Đặt tên gợi nhớ giúp quản lý khi có nhiều CDN 


*  **Region:** Chọn Việt Nam


*  **Alternate domain names (CNAMES) :** Tên domain mà user sẽ truy cập tới để xem nội dung. Ví dụ: testing.vcdn.vn


*  **TTL:** thời gian cache tối đa trên hệ thống.


*  **Protocols** :


    * Gồm 2 lựa chọn là HTTP và HTTPS.


    * Với HTTPS cần chọn thêm SSL



    

![Default Certificate](images/storage/CERT_DEFAULT.jpg)

 _Default CDN certificate_ 

![Custom Certificate](images/storage/CERT_CUSTOM.jpg)

 _Custom SSL certificate_ 


*  **Raw Format Playback link:** 

Nếu không sử dụng chức năng "Secure Token", link playback của bạn sẽ có format như sau:  **<Protocol>://<Cname|CDN DomainName><URI resource>** 

Ví dụ:  **https://abc.com/film1/20190202/video.mp4** 

Chú thích:


* 
    * Protocol: https
    * Cname: abc.com
    * URI resource:  **/film1/20190202/video.mp4** 

    




*  **Secure token** 



Tùy chọn dùng để ngăn chặn việc liên kết nội dung từ một trang web khác sử dụng nội dung của bạn mà không được phép, không được ủy quyền. Chẳng hạn các website khác sao chép link website để trộm nội dung và lợi dụng băng thông mà bạn trả phí với các nhà cung cấp khác, làm tăng chi phí hoạt động.

Chi tiết hơn về cách sử dụng Secure Token, bạn có thể tham khảo: [cấu hình Secure Token](https://docs.vngcloud.vn/display/ONVINA/Secure+Token)



 **Bước 5:** Thiết lập các rule cho cache 

Chọn "Add rule" để thêm mới. Hiện vCDN không giới hạn số lượng rule có thể tạo

![Add Rule](images/storage/RULE_ADD.jpg)

Với mỗi rule có thể đặt nhiều điều kiện và xếp thứ tự ưu tiên bằng cách nhấn vào mũi tên để di chuyển.

Cụ thể hơn về cách thức hoạt động của Rule, bạn có thể tham khảo: [Thiết lập Rule cho CDN](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2721278)



![Add Rule](images/storage/RULE_MORE.jpg)

 **Bước 6:**  Chọn Create New -> Để tạo một vCDN Web Accelerator mới

![Create](images/storage/WEB_ACC_CREATE.jpg)

Sau đó, màn hình sẽ được tự động chuyển sang trang chính. Sau đó, bạn sẽ nhận được thông báo như sau thể hiện quá trình tạo CDN thành công.

![Thông báo tạo VOD thành công](images/storage/VOD_5.jpg)

Màn hình hiển thị đã khởi tạo thành công.

![Kết quả](images/storage/VOD_Result.jpg)



Theo bạn thì bài hướng dẫn này có giúp ích cho bạn không? Nếu bạn có thắc mắc, vui lòng liên hệ hotline 1900 54 55 69 hoặc email [support@vngcloud.vn](mailto:support@vngcloud.vn) của vCDN để được hỗ trợ nhé.



*****

[[category.storage-team]] 
[[category.confluence]] 
