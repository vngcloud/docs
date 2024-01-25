 **Giới thiệu: ** Khi bạn thực hiện Transcode live stream tại Origin của bạn thành các luồng với bitrate khác nhau và Push các luồng đó lên vCDN. ABR sẽ tạo ra 1 link playback duy nhất để người dùng cuối xem live stream, thay vì phải xem các link khác nhau (người dùng sẽ được tự động thay đồi luồng live stream tùy theo chất lượng mạng). 

Để tạo ABR, bạn thực hiện như sau

 **Bước 1** : tại portal → chọn ABR

![](images/storage/ABR create.jpg)

 **Bước 2:**  Chọn “ **Create** ” để tạo mới ABR

![Create ABR](images/storage/ABR_1.jpg)

 **Bước 3:**  Nhập các thông tin cấu hình ABR

![Info](images/storage/ABR_2.jpg)


1. ABR name: tên gợi nhớ, có thể nhập các ký tự A-Z, 0-9


1. No Transcode Application: Chọn “Channel App” đã tạo. Nếu chưa có , xem tại đây [Tạo Channel App](https://docs.vinadata.vn/pages/viewpage.action?pageId=2721935)


1. Apply to CDN(s): Chọn Live CDN muốn dùng. Nếu chưa có, xem tại đây [Tạo Live CDN](https://docs.vinadata.vn/pages/viewpage.action?pageId=2721940)


1. Add stream: Như hình trên là user này đã tạo 3 live channel tương ứng với 3 luồng streaming với các thông số Bitrate, Width, Height khác nhau 



Sau khi hoàn tất, chọn  **”Create”** 

 **Bước 4** : Up stream lên các live channel và dùng Playback URL để verify ABR

![Playback Preview](images/storage/ABR_3.jpg)

Theo bạn thì bài hướng dẫn này có giúp ích cho bạn không? Nếu bạn có thắc mắc, vui lòng liên hệ hotline 1900 54 55 69 hoặc email [support@vngcloud.vn](mailto:support@vngcloud.vn) của vCDN để được hỗ trợ nhé.





*****

[[category.storage-team]] 
[[category.confluence]] 
