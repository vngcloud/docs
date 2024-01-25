Để tạo processor group từ Library bạn chọn " **Processor Group Library** " sẽ thấy hiện tại VNG Cloud hỗ trợ thư viện cho 2 ứng dụng phổ biến là Apache, Nginx

![](images/storage/image2022-12-13_12-45-26.png)

Nhấn  **Duplicate this group**  để tạo Processor Group từ Library này

![](images/storage/image2022-12-13_15-33-54.png)

Bạn sẽ cần điền các thông tin:

 **Group name** : tên processor group

 **Description** : mô tả processor group này

 **Pipeline flow:**  là các source và destination log project

 **Filter** : lọc các log thoả mãn điều kiện thì mới vào processor group này để xử lý, nếu là \* sẽ matching tất cả Log trong source log project



![](images/storage/image2022-12-13_15-34-35.png)

Ví dụ ở trên chọn source log project: rawlog và destination log project: structurelog, chọn Duplicated để tạo, hệ thống sẽ tự động Process Group và các Processor

![](images/storage/image2022-12-13_15-35-9.png)

Như hình trên bạn sẽ thấy Processor Group: apache đã được tự động tạo với 3 processor: grok-parser, geo-ip-parser, user-agent-parser để parse dữ liệu raw log apache thành dữ liệu có cấu trúc từ log project rawlog →structurelog.

Để kiểm tra xem quá trình parse logs có thành công hay không, thử đẩy apache log với format COMBINEDAPACHELOG vào log project rawlog

 **1.1.1.1 - grah [12/Nov/2021:14:25:32 -0000] "GET /sematext.png HTTP/1.1" 200 3423 "http://www.sematext.com/index.html" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.74 Safari/537.36 Edg/79.0.309.43"** 

Bạn có thể thấy tại source log project: rawlog thì log đang ở dạng chưa được xử lý như trên, tất cả nội dung nằm trong field message

![](images/storage/image2022-12-13_15-43-51.png)

Còn ở destination log project: structurelog thì log đã được parse ra thành có cấu trúc, có đầy đủ các field như referrer, verb, geoip,..., giúp quá trình tìm kiếm và phân tích log cực kì dễ dàng

![](images/storage/image2022-12-13_15-46-30.png)



Chúc mừng bạn đã tạo thành công Processor Group từ Library



*****

[[category.storage-team]] 
[[category.confluence]] 
