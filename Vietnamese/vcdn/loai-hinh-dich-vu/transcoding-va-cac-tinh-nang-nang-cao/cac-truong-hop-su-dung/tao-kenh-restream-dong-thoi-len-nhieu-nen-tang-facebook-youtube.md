# Tạo kênh Restream đồng thời lên nhiều nền tảng Facebook, Youtube

Để tạo kênh Restream đồng thời lên nhiều nền tảng, hãy làm theo hướng dẫn sau:

## Cài đặt Sigma Media Server

Đầu tiên, bạn cần cài đặt Sigma Media Server theo các bước tại [đây](../cai-dat-sigma-media-server.md).

## Khởi tạo và cấu hình dịch vụ Media Service để livestream.&#x20;

**Bước 1:** Sau khi đã cài đặt Sigma Media Server thành công, bạn hãy truy cập vào [https://portal.sigma.video/apps](https://portal.sigma.video/apps) với email mà bạn đã đăng ký sử dụng dịch vụ trước đó.

<figure><img src="../../../../.gitbook/assets/image (654).png" alt=""><figcaption></figcaption></figure>

**Bước 2:** Bạn chọn xổ menu **Product** xuống và chọn mục **Media VOD**

<figure><img src="../../../../.gitbook/assets/image (655).png" alt=""><figcaption></figcaption></figure>

**Bước 3:** Tiếp tục bạn chọn tab **VOD**

<figure><img src="../../../../.gitbook/assets/image (656).png" alt=""><figcaption></figcaption></figure>

**Bước 4:** Chọn nút **Add** ở góc phải để tạo job transcoding

<figure><img src="../../../../.gitbook/assets/image (657).png" alt=""><figcaption></figcaption></figure>

**Bước 5:** Chọn một **server** để thực thi job transcoding, mặc định Sigma Media Server mà bạn đã khởi tạo trước đó trên **vMarketPlace** sẽ được chọn.

<figure><img src="../../../../.gitbook/assets/image (658).png" alt=""><figcaption></figcaption></figure>

**Bước 6:** Chọn loại file nguồn cần transcode. Bạn cần nhập vào link [URL](https://han01.vstorage.vngcloud.vn/v1/AUTH\_210ff69ad18d4bfa9920b165ef8ddef4/con\_01/big\_buck\_bunny\_720p\_30mb.mp4) của file nguồn đã được upload lên dịch vụ S3. Ví dụ với vStorage, URL của object sẽ có định dạng tương tự: [https://hcm03.vstorage.vngcloud.vn/v1/AUTH\_123456/cont\_01/pexels\_videos\_1390942%20(2160p).mp4](https://hcm03.vstorage.vngcloud.vn/v1/AUTH\_bcd882dd104f40cb8e20f1cd6bb0b4c6/cont\_01/pexels\_videos\_1390942%20\(2160p\).mp4)

<figure><img src="../../../../.gitbook/assets/image (660).png" alt=""><figcaption></figcaption></figure>

**Bước 7:** Tại mục **Destination**, chọn kiểu output Third-party Storage -> Generic S3 để lưu file kết quả

<figure><img src="../../../../.gitbook/assets/image (661).png" alt=""><figcaption></figcaption></figure>

**Bước 8**: Cấu hình thông tin S3 của bạn

<figure><img src="../../../../.gitbook/assets/image (662).png" alt=""><figcaption></figcaption></figure>

**Bước 9:** Config các **profile** của đầu vào

<figure><img src="../../../../.gitbook/assets/image (663).png" alt=""><figcaption></figcaption></figure>

**Bước 10:** Config các **profile** đầu ra

<figure><img src="../../../../.gitbook/assets/image (664).png" alt=""><figcaption></figcaption></figure>

**Bước 11:** Trong kịch bản này chúng ta sẽ Chọn **HLS**

<figure><img src="../../../../.gitbook/assets/image (665).png" alt=""><figcaption></figcaption></figure>

**Bước 12:** Config các tham số **HLS**

<figure><img src="../../../../.gitbook/assets/image (666).png" alt=""><figcaption></figcaption></figure>

**Bước 13:** Bấm **Create Job** để bắt đầu transcode

<figure><img src="../../../../.gitbook/assets/image (667).png" alt=""><figcaption></figcaption></figure>

**Bước 14**: Trở về tab VOD chúng ta sẽ thấy % xử lý, hoặc thông báo lỗi nếu có của các job đã tạo.

<figure><img src="../../../../.gitbook/assets/image (668).png" alt=""><figcaption></figcaption></figure>

## Khởi tạo và cấu hình dịch vụ vCDN.

**Bước 1:** Bạn thực hiện truy cập [VNG Cloud – ](https://vcdn.vngcloud.vn/)[vCDN](https://vcdn.vngcloud.vn/)[ Portal](https://vcdn.vngcloud.vn/)

**Bước 2:** Khởi tạo một domain CDN dành cho VOD theo hướng dẫn tại [đây](../../video-on-demand-streaming.md).

**Bước 3:** Chọn **Origin** của **CDN** là **S3**

<figure><img src="../../../../.gitbook/assets/image (646).png" alt=""><figcaption></figcaption></figure>

Sau khi quá trình transcode thành công, Quý khách có thể truy cập đến video kết quả bằng link CDN sau: <mark style="color:blue;">**https://\<CDN Domain>/sigma-vod/\<transcode\_job\_id>/master.m3u8**</mark>
