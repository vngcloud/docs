Sau khi mua Log Project, hệ thống sẽ tự động sinh ra certificate cho từng Log Project, certificate này dùng để xác thực Log Agent với hệ thống vMonitor.

Để quản lý các certificate này, bạn cần truy cập vào Integration và chọn Certificate,  ví dụ ở đây sau khi mua Log Project: applog, chúng ta sẽ thấy thông tin certificate cho applog như bên dưới: 

![](images/storage/image2021-5-14_11-50-3.png)

Tại đây bạn có thể thực hiện 2 action:


* Download: tải certificate của Log Project về để tiến hành cài đặt Log Agent
* Re-generate: trong trường hợp bạn nghi ngờ certificate của mình đã bị lộ, bạn nên tiến hành vô hiệu certificate cũ và tạo cái mới nhờ tính năng re-generate, lưu ý rằng: khi bạn chọn re-generate tất cả các Log Agent mà sử dụng certificate cũ sẽ không còn đẩy Log được nữa, bạn cần thay đổi certificate mới.

 **Download Certificate** 

Tại trang Certificate, bạn nhấn nút Download của Log Project mà cần sử dụng:

![](images/storage/image2021-5-14_14-3-57.png)Sau khi tải về và giải nén, bạn sẽ thấy cây thư mục theo hệ điều hành và các Log Agent (filebeat, fluentd, logstash, rsyslog) có thể sử dụng cùng với các certificate file, tại đây bạn có thể sử dụng các file này để cài đặt Log Agent và đẩy Log về.

![](images/storage/image2021-5-14_14-5-10.png)

 **Re-generate Certificate** 

Trong trường hợp bạn bị lộ certificate và muốn thay đổi certificate mới, bạn cần nhấn vào re-generate: 

![](images/storage/image2021-5-14_14-8-40.png)

![](images/storage/image2021-5-14_14-9-24.png)

Sau đó bạn cần Download lại certificate mới để sử dụng.

Sau khi có Cerificate bạn sẽ tới bước cài đặt Log Agent để đẩy Log về hệ thống vMonitor.



*****

[[category.storage-team]] 
[[category.confluence]] 
