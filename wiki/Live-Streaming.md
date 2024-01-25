 **Tổng quan** Dịch vụ phát nội dung trực tiếp như sự kiện, chương trình truyền hình, thể thao đến nhiều người trên nền tảng internet.



 **Sơ đồ hoạt động** 

 **Cơ Chế Phân Phối Dữ Liệu** Sử dụng phương pháp [[PU|Phương-Pháp-PULL]][LL](#_Phương_pháp_PULL), [PUS](#_Phương_pháp_PUSH)[[H|Phương-Pháp-PUSH]] chọn tín hiệu đầu vào và tín hiểu đầu ra, đảm bào đường truyền tốt nhất, ổn định nhất, nhiều điểm truy cấp nhất cho dịch vụ live.

 **Tính Năng Dịch Vụ** ![](images/storage/image2021-11-18_8-52-43.png)


* Tùy chọn thời chunk size nhằm tối ưu việc caching và phân phối nội dung
* Hỗ trợ multi [[Origin|Origin]] khi tạo CDN.
* Hỗ trợ tùy chọn[[ HTTPS|Tùy-Chọn-HTTPS-Ở-ORIGIN]] khi kết nối đến Origin.
* [[Hỗ trợ các tính năng bảo mật link đầu ra|Security-Link]]:
* Tùy chỉnh [[cơ chế caching|Tùy-Chỉnh-Các-Tính-Năng-Cache]] phù hợp với loại nội dung.
* Hỗ trợ [[CNAME|CNAME]] cho CDN.
* [[Quản lý và theo dõi các tín hiệu|Quản-Lý-Và-Theo-Dõi-Các-Tín-Hiệu-Được-Đẩy-Đến-Hệ-Thống-Live-Entrypoint]][u](#_Quản_lý_và) được đẩy đến hệ thống Live Entrypoint.
* Hỗ trợ Adaptive bitrate (ABR) sử dụng định dạng video nguồn được mã hóa ở nhiều tốc độ bit. Các codec video được sử dụng phổ biến nhất là H.264 / AVC và H.265 / HEVC. Bộ giải mã âm thanh được sử dụng phổ biến nhất là AAC. Qua đó có thế tương thích với nhiều băng thông người xem trực tuyến có tốc độ khác nhau.


### Hướng dẫn khởi tạo Live Stream CDN

* Bước 1: Tạo 1 tín hiệu đầu vào Live Entrypoint hỗ trợ live Streaming.

     ![](images/storage/image2023-8-15_10-49-53.png)


*  Bước 2: Tạo tín hiệu đầu vào bằng cách điền thông tin tên, tên app, bảo mật tín hiệu đầu vào qua màn hình tạo tín hiều đầu vào (Live Entrypoint).

     ![](images/storage/image2023-8-15_10-52-59.png)

Trong đó: 

(2): Bật/tắt chức năng timeshift cho Live Entrypoint này, mặc định vCDN chỉ hỗ trợ timeshift 30 phút.

(3): Nhập vào các địa chỉ IP được phép gửi tín hiệu RTMP vào hệ thống Live Entrypoint,  _hoặc_ 

(4): Nhập vào thông tin username và password để xác thực khi gửi tín hiệu RTMP vào Live Entrypoint

 _**Mục (3) và (4) bạn phải nhập thông tin 01 trong 02 mục, hoặc cả 02 đều được, không được để trống cả 02 mục._ 

(5): Chọn ISP chính nhận tín hiệu RTMP, khung kế bên thể hiện URL RTMP để bạn push luồng live

(6): Chọn ISP backup nhận tín hiệu RTMP, khung kế bên thể hiện URL RTMP để bạn push luồng live

(7): Lựa chọn media type cho dịch vụ Live

(8): Lựa chọn segment size (thời gian mỗi file nội dung được đóng gói từ tín hiệu RTMP dưới định dạng HLS) cho dịch vụ Live


* Bước 3: Tạo Live Streaming CDN: Chọn menu Live Streaming, nhấn nút tạo CDN (Create):

     ![](images/storage/image2023-8-15_10-54-28.png)


* Bước 4: Tạo nội dung và tùy chọn CDN Live Streaming

     ![](images/storage/image2023-8-15_11-15-50.png)

Trong đó:


1. Nhập tên cho CDN.
1. Dịch vụ Live Streaming CDN cho phép khách hàng sử dụng một trong 2 loại là CDN Packaging và Origin Packaging.
1. Thời gian "băm" của các file "ts" với loại dịch vụ VoD là CDN Packaging.
1. Chọn các thông tin tính năng dịch vụ.
1. Tùy theo người dùng yêu cầu nhập thông [tin chính sách rule cơ bản](#_Chính_sách_rule) hoặc [chính sách rule nâng cao](#_Chính_sách_rule_1) cho CDN.

Bước 5: Khi điền các thông tin đúng và đủ thì nhấn button Submit ở cuối cùng giao diện đợi khoản 5 phút cho hệ thống cái đặt CDN cho người dùng.

Khi tạo cdn xong người dùng có thê cấu hình và truy cập theo Link

       + Đối với link sử dụng HTTPS là https://<vCDN Domain>/ <ChannelName>.

       + Đối với link sử dụng HTTP là https://<vCDN Domain>/ <ChannelName>.



*****

[[category.storage-team]] 
[[category.confluence]] 
