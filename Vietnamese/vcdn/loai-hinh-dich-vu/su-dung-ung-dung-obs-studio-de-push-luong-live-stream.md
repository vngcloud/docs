# Sử dụng ứng dụng OBS Studio để push luồng Live Stream

Sau khi khởi tạo dịch vụ ở mục Live Entrypoint thì bạn có thể sử dụng 1 phần mềm dùng để push livestream lên như OBS Studio:&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766992/image2023-8-7_14-11-21.png?version=1&#x26;modificationDate=1691392282000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Bước 1: Mở OBS chọn Settings

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766992/image2023-8-7_14-10-36.png?version=1&#x26;modificationDate=1691392237000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Bước 2: Ở phần Settings các bạn chọn Stream ở Tab bên trái. Trong đó:
  * Service: Custom...
  * Server: [rtmp://vnpt.entrypoint.vcdn.live/xxxxxxxxxxxxxxxx/](rtmp://vnpt.entrypoint.vcdn.live/thongnh5bece1176ba5bb5c3bedff42/) (Live EP domain được cung cấp khi bạn tạo và LiveApp của các bạn có thể tìm thấy tại mục cấu hình Live Entrypoint)
  * Stream Key: demo1?u=xxxxxx\&p=xxxxxxx (Channel (demo1) bạn có thể nhập tùy ý| Username & password bạn nhập lúc khởi tạo Live Entrypoint)

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766992/image2023-8-7_14-8-21.png?version=1&#x26;modificationDate=1691392102000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Sau khi tạo 1 domain Live CDN được mapping với Live App đã push stream thì link view được tạo ra sẽ có dạng [https://domaincdn.vcdn.cloud/demo1/index.m3u8](https://mudeqtttpiliv.vcdn.cloud/demo1/index.m3u8).
