VNG Cloud vDB hỗ trợ hai cách sao lưu (backup) dữ liệu là: theo nhu cầu (on-demand) và tự động hằng ngày (daily automatic) tại thời điểm được ấn định trước.





A. Sao lưu theo nhu cầu (On-demand backup hoặc Manual backup)Khi bạn có nhu cầu tạo bản backup, bạn truy cập dịch vụ VNG Cloud vDB và chọn đến màn hình quản lý backup. Màn hình này sẽ liệt kê tất cả các bản backup (manual & auto) của tất cả các RDS Instance có trong tài khoản của bạn.

Bạn nhấn vào  **Create Backup** 

![](images/storage/image2019-6-24_15-0-48.png)

Tại màn hình  **Create Backup** , bạn lần lượt lựa chọn các thông tin:


*  **Database Instance Name** : chọn RDS Instance mà bạn muốn thực hiện backup.


*  **Backup Name** : đặt tên cho bản backup này.


*  **Backup Type** : ở đây bạn có 2 lựa chọn là:


    *  **Full Backup** : vDB sẽ backup toàn bộ dữ liệu của bạn.


    *  **Incremetal Backup** : vDB sẽ chỉ backup những sự thay đổi trong database của bạn. Dung lượng của bản Incremetal Backup sẽ nhẹ hơn rất nhiều so với một bản Full Backup. Tuy vậy, bản Incremetal Backup đòi hỏi bạn đã tạo ít nhất một bản Full Backup trước đó cho RDS Instance này.



    
*  **Backup Parents** : nếu ở Backup Type bạn chọn là Incremetal Backup, thì ở đây bạn phải chỉ định một Backup Parent cho bản Incremetal Backup này. Backup Parent có thể là một bản Full Backup hoặc một bản Incremetal Backup được tạo trước đó.



 **Lưu ý** : Incremetal Backup lệ thuộc bản Backup Parent. Nếu bạn xóa Backup Parent, các bản Incremetal Backup của bản Backup đó sẽ bị vô hiệu và bị xóa theo.

Sau khi chắc chắn mọi thông tin đều chính xác, bạn nhấn  **Create Backup** .

![](images/storage/image2019-6-24_15-1-6.png)

Nếu hệ thống tiếp nhận thành công, một bản backup sẽ xuất hiện với  **Status** là  **NEW** .

![](images/storage/image2019-6-24_15-1-18.png)

Khi được tạo thành công, bản backup sẽ đổi sang  **Status** là  **COMPLETED** .

![](images/storage/image2019-6-24_15-1-33.png)

Chúc mừng bạn đã tạo thành công một bản MANUAL BACKUP với vDB.



 **Mở rộng** : Ngoài màn hình quản lý Backup, bạn còn có thể tạo bản  **Manual Backup**  ngay tại màn hình quản lý Database. Khi bạn click chọn một RDS Instance bất kì, bạn chuyển tới thẻ  **Backup** và cuộn xuống danh sách  **Backup list** . Ở đây sẽ liệt kê tất cả các bản backup (manual & auto) tương ứng với RDS Instance này. Bạn có thể nhấn  **Create Backup**  để tiến hành tạo bản Manual Backup ngay tại đây.

![](images/storage/image2019-6-24_15-1-53.png)

Thao tác tiếp theo hoàn toàn tương tự như hướng dẫn ở trên.

 **B. Sao lưu tự động theo ngày (Auto-Daily Backup)** vDB hỗ trợ tính năng tự động sao lưu theo ngày tại thời điểm do bạn ấn định.

Để xem một RDS Instance đã được cấu hình tính năng này chưa, bạn truy cập màn hình quản lý Database. Sau đó, bạn click chọn RDS Instance muốn kiểm tra, chọn thẻ  **Backup** và tìm đến mục  **Backup Information** . Nếu  **Automatic backup** là  **Enabled** tức là bạn đã cấu hình tự động sao lưu hàng ngày cho RDS Instance này vào thời điểm  **Backup Time**  trong ngày.

![](images/storage/image2019-6-24_15-2-10.png)

Để cấu hình tính năng này, bạn có hai phương án:


* Cấu hình luôn trong lúc khởi tạo RDS Instance.


* Thay đổi tại giao diện quản lý Database.



Đối với phương án đầu, mời bạn xem lại hướng dẫn Khởi tạo RDS Instance tại [Hướng dẫn khởi tạo RDS Instance](https://docs.vinadata.vn/pages/viewpage.action?pageId=2722985).

Đối với phương án sau, bạn truy cập màn hình quản lý Database, click chọn RDS Instance muốn cấu hình. Sau đó, bạn click chọn  **Edit Database** . Tại đây, bạn kéo xuống mục  **CHANGE BACKUP SETTINGS** và ** ** bạn có thể cấu hình các thông tin:


*  **Automatic daily backup:** bật tắt tính năng Automatic daily backup.


*  **Backup retention period:** xác định thời gian lưu trữ bản automatic backup. Nhằm giúp bạn tiết kiệm không gian lưu trữ, các bản automatic backup đã quá khoảng thời gian này sẽ bị xóa.


*  **Backup time:** thời điểm quá trình tạo automatic backup diễn ra. VNG Cloud khuyến nghị bạn chọn thời điểm này vào khoảng thời gian thấp điểm nhất đối với hệ thống của bạn.



![](images/storage/image2019-6-24_15-2-25.png)

Sau khi chắc chắn rằng các thông tin đã chính xác, bạn nhấn nút  **Save** ở góc trên bên phải và chờ một lát để quá trình thay đổi được thực thi.

Bạn có thể tham khảo video sau:



6001200https://www.youtube.com/embed/g6X2YWBl010INLINE





*****

[[category.storage-team]] 
[[category.confluence]] 
