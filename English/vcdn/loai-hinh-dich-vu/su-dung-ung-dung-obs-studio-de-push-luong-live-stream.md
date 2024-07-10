# Using OBS Studio to Push Live Stream

After creating the service in the Live Entrypoint section, you can use a software to push livestream like OBS Studio:

<figure><img src="../../.gitbook/assets/image (165).png" alt=""><figcaption></figcaption></figure>

* **Step 1**: Open OBS and select Settings

<figure><img src="../../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

* **Step 2:** On Settings, select Stream on the left tab. In which:
  * Service: Custom...
  * Server: [rtmp://vnpt.entrypoint.vcdn.live/xxxxxxxxxxxxxxxx/](rtmp://vnpt.entrypoint.vcdn.live/thongnh5bece1176ba5bb5c3bedff42/) (Live EP domain được cung cấp khi bạn tạo và LiveApp của các bạn có thể tìm thấy tại mục cấu hình Live Entrypoint)
  * Stream Key: demo1?u=xxxxxx\&p=xxxxxxx (Channel (demo1) bạn có thể nhập tùy ý| Username & password bạn nhập lúc khởi tạo Live Entrypoint)

<figure><img src="../../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>

After creating a Live CDN domain mapped with the Live App that has pushed the stream, the created link view will have the following form [https://domaincdn.vcdn.cloud/demo1/index.m3u8](https://mudeqtttpiliv.vcdn.cloud/demo1/index.m3u8).
