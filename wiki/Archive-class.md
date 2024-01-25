Archive class là lớp lưu trữ thứ 3 của vStorage bên cạnh gold class và silver class. Archive được thiết kế là nơi lưu trữ an toàn, bền bỉ với chi phí cực kỳ thấp, phù hợp với nhu cầu lưu trữ và sao lưu dữ liệu dài hạn.

Với SLA 99.99% và các tính năng bảo mật dữ liệu vArchive có thể đáp ứng được các tiêu chuẩn an toàn dữ liệu của doanh nghiệp.  Chi phí lưu trữ thấp nhất trong 3 class giúp tiết kiệm hơn rất nhiều so với các giải pháp lưu trữ sao lưu khác. Không chỉ vậy vArchive còn hướng đến việc tối ưu sự tiện dụng cho khách hàng thông qua việc dữ liệu sẽ luôn sẵn sàng để tải về ngay lập tức mà không mất bất kỳ thời gian chờ đợi nào. Thêm vào đó việc quản lý dữ liệu dễ dàng trên giao diện web cùng với các tính năng tìm kiếm thuận tiện.

Tương tự các class khác của vStorage, vArchive cũng tương thích với các S3 client tool, sdk giúp khách hàng có thể tiếp tục sử dụng những phần mềm quen thuộc của mình.

 **Archive class policy** 

Để đáp ứng được các tiêu chí về chi phí cực thấp  và chất lượng dịch vụ được phản ánh qua SLA cam kết 99,99%, Archive class có những quy định về việc lưu trữ như sau


* Dữ liệu khi upload lên class này sẽ không được xóa cho đến khi đạt đủ thời gian tồn tại là 6 tháng.
* Đối với các trường hợp upload nhầm, dữ liệu upload không chính xác cần xóa thì khách hàng có 24 tiếng kể từ lúc upload để xóa dữ liệu. Sau thời gian này thì dữ liệu sẽ không được xóa cho đến khi đủ thời gian quy định là 6 tháng như trên.
* Archive class cung cấp và hỗ trợ đầy đủ các tool để sử dụng như Web [portal.vngcloud.vn](http://portal.vngcloud.vn), API, swift client tools (Cyberduck), S3 client tools (rclones, s3cmd, cyberduck) cho các nhu cầu upload, download, mount thành network disk v..v… Tuy nhiên việc  **xóa dữ liệu chỉ có thể** thực hiện tại [portal.vngcloud.vn](http://portal.vngcloud.vn).
* Với nhu cầu restore: Dữ liệu sẽ sẵng sàng để download trong vòng 1-12 tiếng. 

 **Tips khi sử dụng** 


* Hãy chắc chắn dữ liệu bạn đưa lên archive là những dữ liệu cần lưu trữ nhưng ít sử dụng. Vì tuy rằng chi phí lưu trữ của archive là thấp nhất nhưng những thao tác khác sẽ có chi phí cao hơn các lớp lưu trữ Gold / Silver từ 1-2 lần.
* Archive cũng không phù hợp cho việc rotate dữ liệu liên tục vì policy hạn chế không delete data <6 tháng. Nếu bạn có nhu cầu lưu trữ backup nhưng có thời gian rotation hàng tuần, tháng thì silver class sẽ là lựa chọn phù hợp.  

Để sử dụng archive class, khi khởi tạo project chọn Archive class 







*****

[[category.storage-team]] 
[[category.confluence]] 
