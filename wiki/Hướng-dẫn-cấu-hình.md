
* [Pre Cache](https://docs.vngcloud.vn/pages/viewpage.action?pageId=9175761)

Bạn sử dụng Pre Cache khi bạn cần Cache trước Resource (vd: Video có dung lượng lớn) từ Origin của bạn lên CDN (Web Download, VOD) để phục vụ lượng lớn User (CDN có sẵn Resource để phục vụ User một cách nhanh nhất).

 **_Lưu ý:_**  tính năng Pre Cache được áp dụng với Web Download, VOD.


* [Purge Cache](https://docs.vinadata.vn/pages/viewpage.action?pageId=2721280)

Bạn sử dụng Purge Cache khi bạn cập nhật nội dung Original domain, và cần CDN cập nhật lại nội dung ở Cache tức thì (đồng bộ nội dung cache giữa CDN node với Original của bạn), bạn có thể tiến hành Purge Cache (xoá cache).

 **_Lưu ý:_**  tính năng Purge Cache được áp dụng với Web Download, VOD.


* [Allow Specific Referer (HTTP referer)](https://docs.vinadata.vn/pages/viewpage.action?pageId=2721284)

Cho phép bạn thiết lập quyền truy cập của một hoặc nhiều URI đến domain CDN web của bạn.


* [Cross-origin resource sharing (CORS)](https://docs.vinadata.vn/pages/viewpage.action?pageId=2721282)

CORS cho phép các web scripts tương tác cởi mở hơn với nội dung bên ngoài tên miền gốc, dẫn đến sự tích hợp tốt hơn giữa các dịch vụ web.


* [Thiết lập các Rule cho CDN](https://docs.vinadata.vn/pages/viewpage.action?pageId=2721278)

Rule có thể thiết lập trong lúc khởi tạo (như các hướng dẫn khởi tạo ở trên) hoặc tại edit setting.


* [IP Protection](https://docs.vinadata.vn/pages/viewpage.action?pageId=2721291) 

vCDN đã hỗ trợ tính năng thiết lập truy cập dựa theo IP. Theo đó, bạn có thể cho phép một hoặc nhiều IP được phép truy cập vào hệ thống hoặc không được phép


* [Geo Blocking](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2721288)

vCDN cho phép bạn thiết lập truy cập dựa trên vùng lãnh thổ. Nghĩa là bạn có thể cho phép hoặc không cho phép user từ các vùng lãnh thổ được chỉ định truy cập vào tài nguyên của bạn.


* [Secure Token](https://docs.vngcloud.vn/display/ONVINA/Secure+Token)

Tùy chọn khi tạo CDN (VOD, Live CDN) giúp ngăn chặn việc liên kết nội dung từ một trang web khác sử dụng nội dung của bạn mà không được phép, không được ủy quyền. Chẳng hạn các website khác sao chép link website để trộm nội dung và lợi dụng băng thông mà bạn trả phí với các nhà cung cấp khác, làm tăng chi phí hoạt động.



*****

[[category.storage-team]] 
[[category.confluence]] 
