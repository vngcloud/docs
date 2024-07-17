# Sử dụng tính năng transcoding thông qua Sigma Streaming

## **Sigma Streaming là gì?**

**Sigma Media Server Pro Edition** là Nền tảng truyền phát video đa phương tiện có khả năng mở rộng cao với nhiều tính năng bổ sung. Sản phẩm hỗ trợ phát trực tuyến qua HTTP có độ trễ thấp với các giao thức CMAF và HLS. Hệ thống cho phép nhận tín hiệu qua các giao thức như RTMP, SRT, v.v. Tích hợp với camera IP thông qua RTSP hoặc UDP multicast rất liền mạch, hỗ trợ Chuyển mã/đóng gói VOD hoặc kênh Live sang codec H.264, H.265,... và cũng có sẵn mã hóa dựa trên GPU.Sản phẩm này cung cấp 3 giải pháp chính:

* **Sigma Livestream**: cung cấp khả năng truyền phát video trực tiếp liền mạch với độ trễ cực thấp. Hệ thống hỗ trợ các giao thức phát trực tuyến hàng đầu như Dash-CMAF và HLS, đảm bảo khả năng tương thích trên các thiết bị và mạng. Với việc nhận luồng dễ dàng thông qua RTMP. Hệ thống phù hợp cho các sự kiện trực tiếp cần tính ổn định cao. Thêm vào đó, hệ thống phát lại nội dung trực tiếp giúp người dùng có thể xem lại dễ dàng các luồng trực tiếp đã phát. Được hỗ trợ bởi mã hóa dựa trên GPU và đảm bảo truyền phát chất lượng cao.
* **Sigma Media Live**: cung cấp giải pháp chuyển mã kênh tuyến tính hiệu quả, đảm bảo phân phối mượt mà trên nhiều thiết bị và mạng khác nhau. Tận dụng khả năng chuyển mã nâng cao, hệ thống điều chỉnh nội dung một cách liền mạch để có trải nghiệm xem tối ưu.
* **Sigma Media VOD:** cung cấp khả năng chuyển mã mạnh mẽ cho nội dung video theo yêu cầu, cho phép phát lại liền mạch trên các thiết bị và điều kiện mạng khác nhau. Với các tính năng tiên tiến, hệ thống đảm bảo trải nghiệm phát trực tuyến chất lượng cao để xem nội dung theo yêu cầu.

Sigma Streaming hiện tại đã có sẵn trên hệ thống vMarketPlace của chúng tôi, hãy thực hiện theo hướng dẫn bên dưới để sử dụng tính năng transcoding.

***

## Các bước thực hiện:

Sử dụng hướng dẫn bên dưới để sử dụng tính năng transcoding thông qua Sigma.

### Điều kiện cần:

* Đầu tiên, bạn cần tạo [LiveStream](../live-streaming.md) hoặc [Video on Demand](../video-on-demand-streaming.md) trên hệ thống vCDN theo các hướng dẫn mà chúng tôi đã đề cập ở các trang trên.

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

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### Cấu hình thông số cho Sigma

**Bước 1:** Sau khi khởi tạo Sigma từ vMarketPlace theo hướng dẫn bên trên, bạn có thể truy cập vào giao diện vServer tại [đây](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) để kiểm tra server chạy Sigma đã được khởi tạo xong chưa. **Tiếp theo, bạn mở các sau trên Security Group cho server Sigma vừa tạo.**

* 4000 (TCP): Portal
* 8080 (TCP): HTTP origin (nginx)
* 1935 (TCP): RTMP
* 10080 (UDP): optional cho SRT protocol



**Sau khi server chạy Sigma được khởi tạo thành công**. Để vào GUI của Sigma, bạn cần sử dụng địa chỉ IP của External Interface và truy cập tại link: _http://VM\_External\_IP:4000_.
