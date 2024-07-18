# Sử dụng tính năng transcoding thông qua Sigma Streaming

## **Sigma Streaming là gì?**

**Sigma Media Server Pro Edition** là Nền tảng truyền phát video đa phương tiện có khả năng mở rộng cao với nhiều tính năng bổ sung. Sản phẩm hỗ trợ phát trực tuyến qua HTTP có độ trễ thấp với các giao thức CMAF và HLS. Hệ thống cho phép nhận tín hiệu qua các giao thức như RTMP, SRT, v.v. Tích hợp với camera IP thông qua RTSP hoặc UDP multicast rất liền mạch, hỗ trợ Chuyển mã/đóng gói VOD hoặc kênh Live sang codec H.264, H.265,... và cũng có sẵn mã hóa dựa trên GPU.Sản phẩm này cung cấp 3 giải pháp chính:

* **Sigma Livestream**: cung cấp khả năng truyền phát video trực tiếp liền mạch với độ trễ cực thấp. Hệ thống hỗ trợ các giao thức phát trực tuyến hàng đầu như Dash-CMAF và HLS, đảm bảo khả năng tương thích trên các thiết bị và mạng. Với việc nhận luồng dễ dàng thông qua RTMP. Hệ thống phù hợp cho các sự kiện trực tiếp cần tính ổn định cao. Thêm vào đó, hệ thống phát lại nội dung trực tiếp giúp người dùng có thể xem lại dễ dàng các luồng trực tiếp đã phát. Được hỗ trợ bởi mã hóa dựa trên GPU và đảm bảo truyền phát chất lượng cao.
* **Sigma Media Live**: cung cấp giải pháp chuyển mã kênh tuyến tính hiệu quả, đảm bảo phân phối mượt mà trên nhiều thiết bị và mạng khác nhau. Tận dụng khả năng chuyển mã nâng cao, hệ thống điều chỉnh nội dung một cách liền mạch để có trải nghiệm xem tối ưu.
* **Sigma Media VOD:** cung cấp khả năng chuyển mã mạnh mẽ cho nội dung video theo yêu cầu, cho phép phát lại liền mạch trên các thiết bị và điều kiện mạng khác nhau. Với các tính năng tiên tiến, hệ thống đảm bảo trải nghiệm phát trực tuyến chất lượng cao để xem nội dung theo yêu cầu.

<figure><img src="../../../.gitbook/assets/image (579).png" alt=""><figcaption></figcaption></figure>

Sigma Streaming hiện tại đã có sẵn trên hệ thống vMarketPlace của chúng tôi, hãy thực hiện theo hướng dẫn bên dưới để sử dụng tính năng transcoding.

***

## Các bước thực hiện:

Sử dụng hướng dẫn bên dưới để sử dụng tính năng transcoding thông qua Sigma.

### Khởi tạo Sigma Streaming trên vMarketplace

**Bước 1:** Truy cập vào [https://marketplace.console.vngcloud.vn/](https://marketplace.console.vngcloud.vn/)

**Bước 2:** Tại màn hình chính, thực hiện tìm kiếm **Sigma**, tại dịch vụ **Sigma Stream**, chọn **Launch**.

**Bước 3:** Lúc này, bạn cần thiết lập cấu hình cho **Sigma.** Cụ thể, bạn cần chọn:

* **Loại Instance (CPU, RAM, GPU).**
* **Loại và kích cỡ Volume, IOPS**
* **Network:**
  * **VPC**
  * **Security Group**

mà bạn mong muốn sử dụng cho server của bạn. Ngoài ra bạn cũng cần chọn Một Server Group đã tồn tại hoặc chọn **Dedicated SOFT ANTI AFFINITY group** để chúng tôi tự động tạo một server group mới.

**Bước 4:** Tiến hành thanh toán như các tài nguyên bình thường trên VNG Cloud.

Lúc này, hệ thống vServer sẽ khởi tạo một Server tương ứng với cấu hình mà bạn lựa chọn. Hãy chờ đợi tới khi việc tạo server hoàn thành và tiếp tục các bước sau đây.

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

### Cấu hình thông số cho Sigma Server và khởi tạo Channel trên Sigma Media

**Bước 1:** Sau khi khởi tạo Sigma từ vMarketPlace theo hướng dẫn bên trên, bạn có thể truy cập vào giao diện vServer tại [đây](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) để kiểm tra server chạy Sigma đã được khởi tạo xong chưa. **Tiếp theo, bạn cần mở các sau trên Security Group cho server Sigma vừa tạo.**&#x20;

* 4000 (TCP): Portal
* 8080 (TCP): HTTP origin (nginx)
* 1935 (TCP): RTMP
* 10080 (UDP): optional cho SRT protocol

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

**Bước 2:** Sau khi server chạy Sigma được khởi tạo thành công. Để vào GUI của Sigma, bạn cần sử dụng địa chỉ IP của External Interface và truy cập tại link: _**http://VM\_External\_IP:4000**_

**Bước 3:** Tại GUI của Sigma, bạn chọn nút **Register Server**

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Bước 4: Bạn nhập Email/ Password nếu có hoặc chọn Đăng nhập nhanh với Github hoặc Google. Ở đây, tôi lựa chọn đăng nhập với tài khoản Google

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Bước 5: Sau khi hệ thống thực hiện authentiation thành công, bạn cần nhập các thông tin cơ bản cho Sigma bao gồm:

* Name
* Phone Number
* Role
* Company

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>



**Bước 6:** Nhập server name. Server name này bạn có thể lấy từ portal VNGCloud. Ví dụ bên dưới tôi dùng server Demo\_Sigma đã tạo trước đó.

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Bước 7: Bạn có thể điều chỉnh bật/ tắt các configuration bao gồm:

* Bật/ Tắt sử dụng Ingest App bằng cách chọn vào biểu tượng ON, OFF
* Bật/ Tắt sử dụng Origin App bằng cách chọn vào biểu tượng ON, OFF
* Cài đặt Data Dir bằng cách chọn vào nút Pick
* Chọn Submit.

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Bước 8: Tại màn hình cảnh báo việc deploy server, bạn chọn **Yes**

**Bước 9: Tiếp tục chọn Done, lúc này màn hình sẽ hiển thị như sau, bạn hãy tiếp tục bấm chọn App Editor.**

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Sau khi truy cập vào Portal Sigma Media, bạn sẽ thấy thông tin server đã tạo trước đó từ vMarketplace và thông tin License tương ứng.

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Bước 10: Tại Portal Sigma Media, chọn menu Product, sau đó chọn mục Livestream, tiếp tục chọn tab Channel

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Bước 11: Bạn tiếp tục chọn Add Channel, tại đây, bạn có thể nhập/ chọn:

* Name: tên kênh live stream của bạn
* Description: mô tả cho kênh nếu có
* Tags: nhãn đánh dấu kênh nếu có
* <mark style="color:red;">**Chọn Advance configuration: trong mục này bạn sẽ cấu hình những thông tin cho việc Transcoding, ví dụ trong hình dưới, tôi caasus hình transcoding với 2 transcode profile 480p và 720p**</mark>
* Chọn Save để lưu thông tin Channel.

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Bước 12: Sau khi channel được tạo thành công, bạn hãy lấy thông tin trong mục Information Setting để thực hiện thiết lập project mới trên OBS Studio

<figure><img src="../../../.gitbook/assets/image (572).png" alt=""><figcaption></figcaption></figure>

### Khởi tạo Live Stream/ Video on Demand Streaming trên vCDN

Bước 13: Bạn truy cập trở lại portal vCDN tại [đây](https://vcdn.vngcloud.vn/live-cdn/list.html), chọn mục Live Stream, chọn Create New

<figure><img src="../../../.gitbook/assets/image (574).png" alt=""><figcaption></figcaption></figure>

Bước 14: Thực hiện nhập/ chọn các thông tin cơ bản giống như hướng dẫn khởi tạo Live Stream mà chúng tôi đã hướng dẫn ở các tài liệu bên trên. Chú ý:

* Tại mục Type bạn cần chọn Origin Packaging.

<figure><img src="../../../.gitbook/assets/image (575).png" alt=""><figcaption></figcaption></figure>

* Tại mục HTTP Origin, bạn cần nhập IP Address là địa chỉ External IP của server Sigma của bạn theo định dạng: External IP:8080. Sau đó chọn Add Server.

<figure><img src="../../../.gitbook/assets/image (576).png" alt=""><figcaption></figcaption></figure>

* Tại mục CORS Configuration, bạn cho phép Allow Origin từ mọi nguồn bằng cách nhập \*

<figure><img src="../../../.gitbook/assets/image (577).png" alt=""><figcaption></figcaption></figure>

### Sử dụng OBS Studio để push luồng Live Stream và kiểm tra hoạt động của việc transcoding

Bạn mở ứng dụng OBS Studio, và làm theo hướng dẫn theo các bước tại [đây](su-dung-tinh-nang-transcoding-thong-qua-sigma-streaming.md#su-dung-obs-studio-de-push-luong-live-stream-va-kiem-tra-hoat-dong-cua-viec-transcoding) để sử dụng OBS Studio push luồng live stream. Trong ví dụ bên dưới tôi đã kết nối và push live stream thành công.

<figure><img src="../../../.gitbook/assets/image (573).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (578).png" alt=""><figcaption></figcaption></figure>

Sau khi tạo 1 domain Live CDN được mapping với Live App đã push stream thì link view được tạo ra sẽ có dạng [https://domaincdn.vcdn.cloud/demo1/index.m3u8](https://mudeqtttpiliv.vcdn.cloud/demo1/index.m3u8).

Ví dụ, trong trường hợp trên, khi người dùng truy cập vào link trên, người dùng sẽ xem livestream và có thể chọn Quality là&#x20;

