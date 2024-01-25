Đầu tiên, bạn truy cập Portal của VNG Cloud tại đường dẫn: [https://portal.vngcloud.vn](https://portal.vngcloud.vn/)

Tại giao diện chính, bạn tìm đến dịch vụ  **vDB - Database ** và chọn dịch vụ hệ lưu trữ dữ liệu trên bộ nhớ (in-memory)  **MemoryStore Database.** 

![](images/storage/Screenshot from 2020-02-21 00-00-05.png)





Tại giao diện quản lý Database, bạn click chọn  **Create Database** .

![](images/storage/Screenshot from 2020-02-21 00-00-45.png)





Quá trình khởi tạo sẽ trải qua 3 bước:  **Select Engine** ,  **Specify DB details**  và  **Summary** . Hãy cùng VNG Cloud đi vào chi tiết cả 3 bước trên:

 **Bước 1** , bạn chọn  **Database Engine**  mong muốn, sau đó chọn  **Next** .

![](images/storage/Screenshot from 2020-02-21 00-01-01.png)



 **Bước 2** , bạn có thể tùy chỉnh các thông tin cấu hình, tên gọi, network, configuration group và backup scheduler.

Tại mục  **DB Instance Specifications** , bạn lựa chọn:


*  **Engine License** : giấy phép sử dụng database, có thể là phiên bản community hoặc enterprise (tùy từng loại database).


*  **Engine Version** : phiên bản database.


*  **Flavor** : cấu hình DB Instance, bao gồm số core, lượng RAM và đi kèm dung lượng Free Backup. Lưu ý: nếu tổng dung lượng tất cả các bản backup của bạn vượt quá quota này, bạn sẽ phải trả thêm chi phí cho phần dung lượng backup vượt quá quota.


*  **Storage type** : loại ổ cứng lưu trữ.



![](images/storage/Screenshot from 2020-02-21 00-01-27.png)





Tại mục  **Setttings** , bạn có thể cấu hình:


*  **Database Name** : tên database sẽ được khởi tạo tự động.


*  **DB configuration group**  (optional): tên Configuration Group sẽ được áp dụng cho DB Instance này, nếu bạn chưa có nhu cầu tùy chỉnh cấu hình thì có thể bỏ qua trường này.



Tại mục  **Network & Security** , bạn lựa chọn  **Cloud Network**  sẽ sử dụng cho DB Instance này. Mọi DB Instance đều phải kết nối với một Cloud Network. Nếu chưa có Cloud Network nào, bạn có thể tạo một Cloud Network mới với hướng dẫn sau: [Link](https://docs.vinadata.vn/pages/viewpage.action?pageId=2721227).

![](images/storage/Screenshot from 2020-02-21 00-02-26.png)





Tại mục  **Backup** , bạn có thể cấu hình:


*  **Automatic daily backup** : bật/tắt tính năng tự động tạo backup hàng ngày với thời điểm được lựa chọn trước.


*  **Backup retention period** : khoảng thời gian lưu trữ các bản backup tự động. Các bản backup tự động được lưu trữ quá thời gian này sẽ được tự động xóa khỏi hệ thống. Thông số này không ảnh huởng đến vòng đời của các bản backup được bạn tạo bằng tay.


*  **Backup time** : thời điểm tiến hành tạo bản backup tự động. VNG Cloud khuyến nghị bạn cấu hình thời điểm này vào thời điểm có lượng truy cập hệ thống thấp nhất trong ngày, thường là từ 12AM - 5AM.



![](images/storage/Screenshot from 2020-02-21 00-03-10.png)







Sau khi cấu hình xong, bạn nhấn  **Next** để sang bước cuối.

Tại bước **Summary** , bạn rà soát lại các thông tin. Nếu có thay đổi, bạn có thể nhấn  **Back** . Khi mọi thông tin đều đã chính xác, bạn nhấn  **Create Database** .

![](images/storage/Screenshot from 2020-02-21 00-03-57.png)





Trong quá trình khởi tạo, DB Instance sẽ có trạng thái  **Building** .

![](images/storage/Screenshot from 2020-02-21 00-04-45.png)





Nếu khởi tạo thành công, DB Instance sẽ có trạng thái  **Active** .

![](images/storage/Screenshot from 2020-02-21 00-08-32.png)





Khi tick chọn DB Instance, bạn có thể xem lại các thông tin cấu hình chi tiết như Flavor, Endpoint & Port để kết nối,... Bạn có thể tham khảo link sau [[Quản lý thông tin MDS Instance|Quản-lý-thông-tin-MDS-Instance]]

Chúc mừng bạn đã khởi tạo thành công DB Instance trên hệ thống VNG Cloud. Mời bạn đến hướng dẫn [[kết nối MDS Instance|Kết-nối-MDS-Instance]] để bắt đầu sử dụng cơ sở dữ liệu.











*****

[[category.storage-team]] 
[[category.confluence]] 
