 **Giới thiệu: ** Live CDN là CDN dùng cho nghiệp vụ live streaming.

Để tạo Live CDN, bạn thực hiện như sau 

 **Bước 1:**  Tại tab " **vCDN - Media service** ", chọn " **Live CDN** "

![](images/storage/Live CDN create.jpg)

 **Bước 2:**  Click " **Create CDN** "

![Create Live CDN](images/storage/LIVE_CDN_2.jpg)

 **Bước 3:**  Thiết lập thông tin cho origin (chỉ áp dụng cho luồng tín hiệu theo cơ chế PULL)

![Thiết lập Original Settings](images/storage/LIVE_CDN_3jpg.jpg)


1.  **Selective Origins:** 


    *  **PULL:** bạn sử dụng CDN origin do mình xây dựng, hệ thống vCDN sẽ lấy nội dung từ origin của bạn dưới dạng HLS


    *  **PUSH:** bạn sử dụng CDN origin của vCDN, bạn phải tạo live application (channel app) để publish tín hiệu rtmp (live channel) của mình vào



    
1.  **Origin domain name** : Nhập địa chỉ gốc của luồng tín hiệu phát tại đây 


1.  **Origin ID:**  vCDN sẽ khởi tạo ID tương ứng 


1.  **Enable HTTPS Origin:**  Nếu domain dùng giao thức HTTPS thì chọn vào ô này 


1.  **Multiple origins:**  Nếu có nhiều origin chọn vào đây để nhập. Lưu ý tại đây sẽ chỉ được nhập IP:PORT


    * Lưu ý: Bạn có thể chọn cơ chế load balancing giữa các Origin như sau:



    

![Multiple Origin load balacing](images/storage/LiveCND_multiOrigin.jpg)


* 
    * 
    1.  **Single:**  luôn chọn Origin đầu tiên.
    1.  **Fail Over:**  luôn chọn Origin đầu tiên, các Origin còn lại để backup.
    1.  **Round Robin:**  sử dụng tất cả các Origin

    

    

 **Bước 4 : Thiết lập các thông số cho vCDN** 




*  **CDN name:** Đặt tên gợi nhớ giúp quản lý dễ dàng khi có nhiều CDN. 


*  **Region:** Chọn Việt Nam


*  **Alternate domain names (CNAMES):** Tên domain mà người dùng cuối sẽ truy cập tới để xem nội dung. Ví dụ: [testing.vcdn.vn](http://testing.vcdn.vn/)


*  **Protocols** : 


    * Gồm 2 lựa chọn là HTTP và HTTPS. 


    * Với HTTPS cần chọn thêm SSL 



    

![Default CDN Certificate](images/storage/CERT_DEFAULT.jpg)

 _Default CDN certificate_ 

![Custom CDN Certificate](images/storage/CERT_CUSTOM.jpg)

 _Custom SSL certificate_ 


*  **Raw Format Playback link:** 



Nếu không sử dụng chức năng "Secure Token", link playback của bạn sẽ có format như sau:  **<Protocol>://<Cname|CDN DomainName>/hls<URI resource>/playlist.m3u8** Ví dụ:  **https://abc.com/hls/stream1/playlist.m3u8** Chú thích:
* 
    * Protocol: https
    * Cname: abc.com
    * Prefix-path: /hls (đây là từ khóa bắt buộc của hệ thống)
    * /stream1: là streamname của live channel do bạn tạo.
    * /playlist.m3u8: từ khóa để lấy stream dưới dạng hls

    




*  **Secure token** 



Tùy chọn dùng để ngăn chặn việc liên kết nội dung từ một trang web khác sử dụng nội dung của bạn mà không được phép, không được ủy quyền. Chẳng hạn các website khác sao chép link website để trộm nội dung và lợi dụng băng thông mà bạn trả phí với các nhà cung cấp khác, làm tăng chi phí hoạt động.

Chi tiết hơn về cách dùng Secure Token, bạn có thể tham khảo: [cấu hình Secure Token](https://docs.vngcloud.vn/display/ONVINA/Secure+Token)



 **Bước 5:** Thiết lập các rule cho cache 

Chọn add rule để thêm mới. Hiện vCDN không giới hạn số lượng rule có thể tạo

![Add Rule](images/storage/RULE_ADD.jpg)

Với mỗi rule có thể đặt nhiều điều kiện và xếp thứ tự ưu tiên bằng cách nhấn vào mũi tên để di chuyển. Thông tin chi tiết về các có thể xem tại

Cụ thể hơn về cách hoạt động của Rule, bạn có thể tham khảo thêm tại: [Thiết lập Rule cho CDN](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2721278)

![Add Rule](images/storage/RULE_MORE.jpg)

 **Bước 6:**  Chọn " **Create New** " -> Để tạo một CDN mới

![Add Rule](images/storage/LIVE_CDN_5.jpg)

Tạo thành công → Live CDN sẽ xuất hiện trong danh sách " **All available CDN(s)** " như hình dưới

![Kết quả](images/storage/LiveCDN_Result.jpg)



Theo bạn thì bài hướng dẫn này có giúp ích cho bạn không? Nếu bạn có thắc mắc, vui lòng liên hệ hotline 1900 54 55 69 hoặc email [support@vngcloud.vn](mailto:support@vngcloud.vn) của vCDN để được hỗ trợ nhé.

 **Kế tiếp: ** 





*****

[[category.storage-team]] 
[[category.confluence]] 
