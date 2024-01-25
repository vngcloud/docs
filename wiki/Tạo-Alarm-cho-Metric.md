Để tạo Alarm cho Metric, bạn cần vào trang Alarm và chọn Create an alarm

![](images/storage/image2021-5-14_18-39-12.png)

Bạn chọn Alarm type là Metric

![](images/storage/image2021-5-17_17-54-33.png)

Tại Metric bạn cần chọn metric và filter, ví dụ ở đây chúng ta cần alarm trên metric cpu.usage_idle của host appserver

Tại Condition bạn cần chỉ định


* alarm condition: điều kiện phép toán
* threshold value: giá trị ngưỡng
* check times: kiểm tra bao nhiêu lần mới chuyển trạng thái và cảnh báo
* interval: bao nhiêu lâu hệ thống alarm sẽ đánh giá một lần

Ví dụ ở đây chúng ta cần Alarm trên metric cpu.usage_idle của host appserver, cứ 5p Alarm sẽ chạy đánh giá một lần, nếu CPU usage idle của host: appserver < 20%, hệ thống sẽ chuyển trạng thái và bắn cảnh báo. 

![](images/storage/image2021-5-17_17-57-54.png)

Sau khi thiết lập điều kiện, bạn sẽ cần chọn hệ thống sẽ thông báo đến đâu, ví dụ nếu Alarm chuyển sang trạng thái OK sẽ cảnh báo tới emailEngineer1, còn nếu Alarm chuyển sang trạng thái in-Alarm sẽ cảnh báo tới emailEngineer1 và smsEngineer1, ta thiết lập như sau:

![](images/storage/image2021-5-17_18-4-10.png)

Cuối cùng bạn cần thiết lập một số thông tin như: Alarm Name, Desc và Severity và nhấn Create để tạo Alarm

![](images/storage/image2021-5-17_18-5-38.png)



Sau khi tạo xong, ban đầu Alarm sẽ ở status: undertermine cho đến lần đánh giá tiếp theo Alarm sẽ chuyển trạng thái tương ứng, ví dụ ở đây Alarm đã chuyển sang trạng thái OK

![](images/storage/image2021-5-17_18-23-45.png)

Và bắn 1 email thông báo tới notification đã được đăng kí: 

![](images/storage/image2021-5-17_18-24-59.png)

Bạn có thể coi chi tiết Alarm bằng cách nhấn vô tên của Alarm

![](images/storage/image2021-5-17_18-25-42.png)

Chúc mứng bạn đã tạo thành công Alarm cho metric 







*****

[[category.storage-team]] 
[[category.confluence]] 
