Để tạo Alarm for Log, bạn cần vào trang Alarm và chọn Create an alarm

![](images/storage/image2021-5-14_18-39-12.png)

Bạn chọn Alarm Type là Log

![](images/storage/image2021-5-14_18-40-2.png)

Tại Alarm conditions bạn cần điền các thông tin sau:


* Chọn Project và câu search query cần thiết
* Alarm type: có 2 lựa chọn là Frequency và Flatline
    * Frequency: thoả mãn khi có ít nhất X event trong khoảng thời gian Y
    * Flatline: thoả mãn khi có ít hơn X event trong khoảng thời gian Y

    
* Alarm condition: điều kiện sẽ đc điều chỉnh theo Alarm type lựa chọn, với frequency sẽ là >, flatline là < 
* Threshold value: giá trị ngưỡng
* Time frame: khoảng dữ liệu mà Alarm sẽ đánh giá.

Ví dụ cần thiết lập cảnh báo là: Nếu trong timeframe: 1p mà có xuất hiện ít nhất 1 dòng Log có trường host:appserver của project: applog thì ta thiết lập như sau:

![](images/storage/image2021-5-14_18-41-18.png)

Sau khi thiết lập điều kiện, bạn sẽ cần chọn hệ thống sẽ thông báo đến đâu, ví dụ nếu Alarm chuyển sang trạng thái OK sẽ cảnh báo tới emailEngineer1, còn nếu Alarm chuyển sang trạng thái in-Alarm sẽ cảnh báo tới emailEngineer1 và smsEngineer1, ta thiết lập như sau:

![](images/storage/image2021-5-14_18-50-30.png)

Cuối cùng bạn cần thiết lập một số thông tin như: Alarm Name, Desc và Severity và nhấn Create để tạo Alarm

![](images/storage/image2021-5-14_18-53-7.png)

 Ban đầu Alarm sẽ có status: Creating và mất 1 khoảng thời gian để hệ thống tạo xong Alarm.

![](images/storage/image2021-5-14_18-55-23.png)

Sau đó Alarm sẽ đánh giá và gửi thông báo tới cho bạn, vì Alarm thoả điều kiện nên Alarm đã chuyển sang status: in-Alarm

![](images/storage/image2021-5-14_19-1-43.png)

Ví dụ thông tin Email nhận được

![](images/storage/image2021-5-14_19-4-16.png)



*****

[[category.storage-team]] 
[[category.confluence]] 
