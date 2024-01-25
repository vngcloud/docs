Sau một khoảng thời gian dùng tính năng archive, bạn có nhu cầu xử lý với data đã được lưu trữ trên vStorage hay S3 compatible có thể dùng tính năng refill để đưa data trở lại log search.

VNG Cloud khuyến nghị bạn nên tạo một project log mới (ngắn hoặc dài hạn tuỳ nhu cầu) để xử lý data được refill này thay vì sử dụng lại project log đã tạo archive.

Đầu tiên bạn vào xem chi tiết của Log Project bằng cách vào tab Log Project, nhấn stick vào tên Log Project cần thiết lập Archive sau đó nhấn vào nút Refill.

![](images/storage/Screen Shot 2022-07-11 at 10.35.44.png)

Bạn cần điền tên của process refill và chọn source từ vStorage hay S3 compatible tuỳ thuộc vào nguồn archive trước đó đã được lưu ở đâu.

![](images/storage/Screen Shot 2022-07-11 at 10.41.01.png)

Bạn điền các thông tin chi tiết để tiến hành việc refill.

Ví dụ với trường hợp chọn vStorage:


* Bạn cần chọn
    * My container: nếu bucket thuộc sở hữu của tài khoản bạn đang cần refill
    * Custom container: nếu bucket không thuộc sở hữu của tài khoản bạn đang cần refill

    
* Region: thông tin region của vStorage hoặc S3 compatible
* vStorage project: Project storage của vStorage
* vStorage container: bucket sẽ dùng để refill và log project
* Access|Secret key: thông tin cặp key dùng để access data trên vStorage hoặc S3 compatible

Note: một số trường hợp là S3 compatible dùng endpoint là IP bạn cần bật option "Force path stype"

![](images/storage/Screen Shot 2022-07-13 at 16.56.04.png)

Sau đó bạn có thể nhấn nút “Test connection” để kiểm tra việc kết nối đến bucket có thành công hay không. Cuối cùng bạn nhấn Select để đến màn hình review về thông tin kết nối. Nhấn Next để đến màn hình chọn Time range cần refill.

![](images/storage/Screen Shot 2022-07-11 at 10.42.50.png)

![](images/storage/Screen Shot 2022-07-11 at 10.53.53.png)

Bạn cần chọn “time range” data cần refill. Sau đó nhấn nút refill để bắt đầu quá trình refill.

![](images/storage/Screen Shot 2022-07-11 at 10.56.18.png)

![](images/storage/Screen Shot 2022-07-11 at 10.57.52.png)

Process refill sẽ bắt đầu thực hiện cho đến khi báo status “Finished”. Bạn có thể check data đã được refill ở trang log search như các project log khác.

![](images/storage/Screen Shot 2022-07-11 at 11.22.07.png)







*****

[[category.storage-team]] 
[[category.confluence]] 
