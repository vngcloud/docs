Khi vMonitor Platform thay đổi mẫu của dashboard default cho các resource như: vServer, vLB, vDB, vStorage hay Host, khách hàng có thể chủ động cập nhật lại mẫu dashboard default mới này bằng cách xoá (monitor) resource đi và hệ thống vMonitor Platform sẽ tự động tạo lại với mẫu mới. Hướng dẫn chi tiết bên dưới cho vServer và có thể ứng dụng cho tất cả các resource khác như vLB, vDB, vStorage và Host.



 **Trường hợp 1** : Resource chưa bật Detailed Monitoring

![](images/storage/image2023-6-19_15-52-49.png)

Với trường hợp này khách hàng chỉ cần nhấn vào  **nút icon Delete**  ngay tại Resource cần xoá (monitor), hệ thống sẽ  **tự động sinh lại Resource này và tạo dashboard default mới**  sau 1 khoảng thời gian (dưới 1 phút)

![](images/storage/image2023-6-19_15-54-3.png)

Lúc này bạn kiểm tra tại trang Dashboard sẽ thấy dashboard default với mẫu mới cho Resource này với thời gian tạo mới

![](images/storage/image2023-6-19_15-56-44.png)



 **Trường hợp 2** : Resource đã bật Detailed Monitoring

Tương tự như trường hợp trên bạn cần nhấn vào  **nút icon Delete**  ngay tại Resource cần xoá (monitor), hệ thống sẽ  **tự động sinh lại Resource này và tạo dashboard default mới**  sau 1 khoảng thời gian (dưới 1 phút)

![](images/storage/image2023-6-19_16-2-5.png)

Lưu ý rằng với trường hợp này, hệ thống sẽ tạo lại Resource với chế độ tắt Detailed Monitoring,  **bạn cần phải enable lại Detailed Monitoring** 

![](images/storage/image2023-6-19_16-3-37.png)

![](images/storage/image2023-6-19_16-3-56.png)

Tương tự bạn kiểm tra bên trang dashboard sẽ thấy dashboard default mới được tạo

![](images/storage/image2023-6-19_16-4-57.png)













*****

[[category.storage-team]] 
[[category.confluence]] 
