# Video On Demand Streaming

#### **Tổng quan** <a href="#videoondemandstreaming-tongquan" id="videoondemandstreaming-tongquan"></a>

Đảm bảo trải nghiệm người dùng tốt nhất khi lựa chọn và xem video trên các thiết bị qua internet.

Dịch vụ VOD của VNG Cloud giúp doanh nghiệp:

* Tối ưu chi phí.
* Đảm bảo sự linh hoạt, dễ dàng tương thích với đa dạng thiết bị đầu cuối.
* Tăng mức độ hài lòng của khách hàng với dịch vụ.
* Phân tích dữ liệu đa chiều theo thời gian thực.

#### **Cơ Chế Phân Phối Dữ Liệu** <a href="#videoondemandstreaming-cochephanphoidulieu" id="videoondemandstreaming-cochephanphoidulieu"></a>

* Dữ liệu đầu vào:
  * Hệ thống Media Preparation của VNGCloud sẽ thực hiện kết nối đến server Storage của khách hàng để lấy nội dung dưới định dạng MP4, MP3, HLS, MpegDash (các định dạng hỗ trợ play trên môi trường internet).
  * Tùy chọn độ dài mỗi media segment khi packaging thành HLS.
  * Server Media Preparation sẽ tiến hành chuyển đổi file với định dạng MP4, MP3 thành định dạng HLS là định dạng hỗ trợ phát trên các thiết bị OTT. Đối với nội dung trên Origin là HLS/MpegDash thì sẽ để nguyên định dạng như dữ liệu gốc.
  * Sau khi chuyển đổi định dạng thì sẽ tiến hành chuyển file đến các server Edge.
* Dữ liệu đầu ra:
  * Hỗ trợ các chuẩn đầu ra với các loại nội dung như:
    * MP4: https:// \<CDN Domain>/<đường dẫn file MP4 trên origin>.
    * HLS: https:// \<CDN Domain>/<đường dẫn file MP4/SMIL trên origin>/index.m3u8.
    * MpegDash: : https:// \<CDN Domain>/<đường dẫn file manifest trên origin?.
  * Hỗ trợ giao thức HTTPS: mặc định tất cả CDN được tạo ra trên hệ thống đều hỗ trợ SSL trên domain của CDN. Tuy nhiên khách hàng có thể sử dụng tự upload Certificate của riêng mình để sử dụng với tên bất kì (tham khảo tại phần quản lý certificate).
  * Hỗ trợ chuẩn play MP4 Progressive: streaming trực tiếp file MP4 từ origin.
  * Hỗ trợ packaging Adaptive Bitrate thông qua định nghĩa file smil (file đặc tả kỹ thuật của ứng dụng Packaging) được đặt chung với các file MP4 trên server Origin. Hệ thống Media Preparation sẽ tiến hành đọc nội dung của file smil và tiến hành chuyển đổi các file MP4 thành chuẩn HLS hỗ trợ Adaptive Bitrate. Cú pháp link đầu ra dưới dạng:
    * HLS (smil ABR): https:// \<CDN Domain>/<Đường dẫn tới file smil trên origin>/index.m3u8.

***

#### **Tính Năng Dịch Vụ** <a href="#videoondemandstreaming-tinhnangdichvu" id="videoondemandstreaming-tinhnangdichvu"></a>

* Hỗ trợ kết nối trực tiếp đến origin là Object Storage thuộc chuẩn [AWS S3](../chi-tiet-tinh-nang/object-storage-s3.md).
* Tùy chỉnh [cơ chế caching](../chi-tiet-tinh-nang/tuy-chinh-cac-tinh-nang-cache.md) phù hợp với loại nội dung: Caching level.
* Hỗ trợ [Origin](../chi-tiet-tinh-nang/origin.md) khi tạo CDN.
* Hỗ trợ [tùy chọn HTTPS](../chi-tiet-tinh-nang/tuy-chon-https-o-origin.md).
* [Hỗ trợ các tính năng bảo mật link đầu ra](../chi-tiet-tinh-nang/security-link.md):
* Tùy chỉnh [thời gian cache](../chi-tiet-tinh-nang/thoi-gian-cache.md).
* Hỗ trợ tự động [redirect từ HTTP sang HTTPS](../chi-tiet-tinh-nang/tu-dong-redirect-tu-http-sang-https.md).
* Hỗ trợ cơ chế “nhà phát triển” ([Development Mode](../chi-tiet-tinh-nang/development-mode.md))
* Multi Audio Selection: tính năng hỗ trợ tách Audio trong file MP4 (trong trường hợp có nhiều định dạng Audio trong file), tính năng này được hỗ trợ song song cùng với tính năng Adaptive bitrate bằng file smil. Cú pháp link đầu ra tương tự như tính năng Adaptive Bitrate
* HLS (smil ABR): https:// \<CDN Domain>/<Đường dẫn tới file smil trên VNGCloud Storage/Origin >/index.m3u8.

***

#### **Hướng dẫn khởi tạo VOD CDN** <a href="#videoondemandstreaming-huongdankhoitaovodcdn" id="videoondemandstreaming-huongdankhoitaovodcdn"></a>

* Bước 1: Tạo VOD CDN bằng cách chọn menu VOD, chọn button Create CDN.

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045701/image2023-8-15_11-20-4.png?version=1&#x26;modificationDate=1692073205000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Bước 2: Tạo CDN

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045701/image2023-8-15_11-21-52.png?version=1&#x26;modificationDate=1692073312000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Bước 3: Nhập tên cho CDN.
* Bước 4: Chọn cấu hình VOD type bao gồm:
  * CDN Packaging (Hệ thống vCDN sẽ packaging media từ file video gốc của khách hàng).
  * Origin packaging (Origin của khách hàng tự packaging, vCDN chỉ phục vụ).
  * MP4 (vCDN phục vụ trực tiếp file mp4 gốc từ origin cho end-user).
* Bước 5: Thời gian "băm" của các file "ts" với loại dịch vụ VoD là CDN Packaging.
* Tùy chọn các tính năng dịch vụ của VOD
* Tùy theo người dùng yêu cầu nhập thông tin [chính sách rule cơ bản](../chi-tiet-tinh-nang/chinh-sach-rule-co-ban-pagerule.md) hoặc chính sách rule nâng cao cho CDN.
* Khi điền các thông tin đúng và đủ thì nhấn button Submit ở cuối cùng giao diện đợi khoản 5 phút cho hệ thống cái đặt CDN cho người dùng.
* Người dùng có thể truy cập CDN qua vCDN Domain khi đã tạo CDN xong.

***

Khi cấu hình CDN xong người dùng có thể truy cập các CDN VoD theo các link dưới đây:

* MP4: https:// \<CDN Domain>/<đường dẫn file MP4 trên origin>.
* MP3: https:// \<CDN Domain>/<đường dẫn file MP3 trên origin >.
* HLS: https:// \<CDN Domain>/<đường dẫn file MP4/SMIL trên origin>/index.m3u8.
* MpegDash: : https:// \<CDN Domain>/<đường dẫn file manifest trên origin>.

\
