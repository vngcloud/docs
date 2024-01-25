Khi bạn mong muốn chuyển 1 read replica thành standalone, bạn có thể sử dụng tính năng Promote to Standalone trên Portal, chọn DB Instance có  **role: slave** , chọn  **ACTION** 



Chọn **Promote to Standalone** 

![](images/storage/image2021-6-14_16-29-18.png)

Trước khi xác nhận promote, chúng tôi khuyến cáo rằng bạn nên dừng việc ghi dữ liệu vào master và đợi đến khi read replica đã đồng bộ toàn bộ dữ liệu, mặc khác sẽ có tỉ lệ read replica không có đủ dữ liệu đã được ghi tại master, chú ý rằng quá trình promotion này có thể mất 1 khoảng thời gian để hoàn thành và sau quá trình này, read replicas sẽ trở thành standalone, và quá trình replication giữa master và slave sẽ dừng lại:

![](images/storage/image2021-6-14_16-33-23.png)

Sau khi promote thành công, read replica đã chuyển thành **role:standalone**  và có thể ghi được, đồng thời DB Instance có role master trước đó cũng chuyển thành role:standalone vì không còn ai replicate từ nó nữa

![](images/storage/image2021-6-14_16-34-35.png)

![](images/storage/image2021-6-14_16-35-29.png)





*****

[[category.storage-team]] 
[[category.confluence]] 
