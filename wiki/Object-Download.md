 **Tổng quan** Dịch vụ Object Download của VNG Cloud giúp doanh nghiệp: tối ưu chi phí, đảm bảo sự linh hoạt, dễ dàng tương thích với đa dạng thiết bị đầu cuối, từ đó, tăng mức độ hài lòng của khách hàng với dịch vụ với khả năng phân tích dữ liệu đa chiều theo thời gian thực.


### Sơ đồ hoạt động
![](images/storage/)

 **Cơ Chế Phân Phối Dữ Liệu** 
* Dữ liệu đầu vào:
    * Hệ thống Origin Gateway của VNGCloud sẽ thực hiện kết nối đến origin server hoặc Storage của khách hàng để lấy nội dung được yêu cầu từ client với bất kì loại định dạng gì như: js, css, image, tff v.v
    * Nếu nội dung được yêu cầu có kích thước lớn thì hệ thống Origin Gateway sẽ tiến hành tạo ra nhiều request nhỏ 5MB và kéo song song đến origin để tăng tốc độ tải cũng như phục vụ user ngay khi có những dữ liệu đầu tiên (Byte-range download).
    * Dữ liệu từ Origin Gateway sẽ được gửi đến các Edge để phục vụ người dùng.

    
* Dữ liệu đầu ra.
    * Hỗ trợ giao thức HTTPS: mặc định tất cả CDN được tạo ra trên hệ thống đều hỗ trợ SSL trên domain của CDN. Tuy nhiên khách hàng có thể sử dụng tự upload Certificate của riêng mình để sử dụng với tên bất kì (tham khảo tại phần quản lý certificate).
    * Hỗ trợ HTTP/2: tăng tốc độ kết nối vào truyền dữ liệu trên trình duyệt.

    

 **Tính Năng Dịch Vụ** 
* Các tính năng [[bảo mật link đầu ra|Security-Link]].
* Tùy chỉnh [[cơ chế caching|Tùy-Chỉnh-Các-Tính-Năng-Cache]] phù hợp với loại nội dung.
* Hỗ trợ [[CNAME|CNAME]] cho CDN.
* Hỗ trợ tính năng bảo mật [[HSTS|Tính-Năng-Bảo-Mật-HSTS]].
* Tùy chỉnh [[thời gian cache|Thời-Gian-Cache]] tối đa.
* Hỗ trợ cơ chế “nhà phát triển” ([[Development Mode|Development-Mode]]).
* Hỗ trợ tùy chỉnh [[Origin|Origin]].
* Hỗ trợ [[tùy chọn HTTPS|Tùy-Chọn-HTTPS-Ở-ORIGIN]] khi kết nối đến Origin.
* Hỗ trợ kết nối trực tiếp đến origin là [[Object Storage thuộc chuẩn AWS S3|S3-Origin]].

 **Hướng dẫn khởi tạo Object download CDN** 
* Bước 1: Chọn menu Object Download, chọn button tạo CDN:

![](images/storage/image2023-8-15_11-29-54.png)


* Bước 2: Điền thông tin chi tiết, tùy chình tính năng dịch vụ ở màn hình tạo CDN.

![](images/storage/image2023-8-15_11-30-25.png)


* Bước 3: Nhập tên CDN.
* Bước 4: Tùy chỉnh các tính năng của CDN.
* Bước 5: Tùy theo người dùng yêu cầu nhập thông [[tin chính sách rule cơ bản|Chính-Sách-Rule-Cơ-Bản-(PageRule)]] hoặc [[chính sách rule nâng cao|Chính-Sách-Rule-Nâng-Cao-(AdvanceRule)]] cho CDN.
* Bước 6: Khi điền các thông tin đúng và đủ thì nhấn button Submit ở cuối cùng giao diện đợi khoản 5 phút cho hệ thống cái đặt CDN cho người dùng.
* Bước 7: Người dùng có thể truy cập CDN qua vCDN Domain khi đã tạo CDN xong.





*****

[[category.storage-team]] 
[[category.confluence]] 
