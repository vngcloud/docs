Sau khi khởi tạo dịch vụ ở mục Live Entrypoint thì bạn có thể sử dụng 1 phần mềm dùng để push livestream lên như OBS Studio: 

![](images/storage/image2023-8-7_14-11-21.png)


* Bước 1: Mở OBS chọn Settings

![](images/storage/image2023-8-7_14-10-36.png)


* Bước 2: Ở phần Settings các bạn chọn Stream ở Tab bên trái. Trong đó:
    * Service: Custom...
    * Server: [rtmp://vnpt.entrypoint.vcdn.live/xxxxxxxxxxxxxxxx/](rtmp://vnpt.entrypoint.vcdn.live/thongnh5bece1176ba5bb5c3bedff42/) (Live EP domain được cung cấp khi bạn tạo và LiveApp của các bạn có thể tìm thấy tại mục cấu hình Live Entrypoint)
    * Stream Key: demo1?u=xxxxxx&p=xxxxxxx (Channel (demo1) bạn có thể nhập tùy ý| Username & password bạn nhập lúc khởi tạo Live Entrypoint)

    

![](images/storage/image2023-8-7_14-8-21.png)

Sau khi tạo 1 domain Live CDN được mapping với Live App đã push stream thì link view được tạo ra sẽ có dạng [https://domaincdn.vcdn.cloud/demo1/index.m3u8](https://mudeqtttpiliv.vcdn.cloud/demo1/index.m3u8).















*****

[[category.storage-team]] 
[[category.confluence]] 
