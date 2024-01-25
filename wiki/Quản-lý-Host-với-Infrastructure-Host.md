 Những server cài đặt Metric Agent được gọi là  **Host** , sau khi cài đặt thành công trên các Server, bạn có thể thấy danh sách các Host đang đẩy Metric về tại trang Infrastructure List/Host

![](images/storage/image2021-5-17_16-51-2.png)

Tại trang này ở mỗi Host bạn sẽ thấy các thông tin như sau:


* Status: trạng thái của server có đang đẩy dữ liệu về hay không, nếu có sẽ là UP, nếu không sẽ là Undertermine
* CPU: thông tin CPU hiện tại
* IOwait: thông tin IOwait hiện tại
* Load: thông tin Load hiện tại
* Apps: danh sách các plugin mà Metric Agent đang bật

Khi nhấn vào khung của 1 Host, sẽ có trang xem chi tiết về Host đó, quy tắc đặt tên dashboard cho Host sẽ là hostname của Host:

![](images/storage/image2021-5-17_16-53-59.png)

Đồng thời nhấn vào tên của Host, bạn sẽ được chuyển sang trang Dashboard, và xem default dashboard của Host này.

![](images/storage/image2021-5-17_16-58-15.png)



 **Chú ý: ** hệ thống vMonitor sẽ mất 1 khoảng thời gian trung bình dưới 1 phút (có thể có trường hợp tệ nhất 5 phút) để cập nhập Host mới sau khi bạn cài Metric Agent.







*****

[[category.storage-team]] 
[[category.confluence]] 
