Mỗi object trong vStorage sẽ được đặt tại 1 lớp lưu trữ  (storage class) tương ứng theo class của Container. Bạn có thể chuyển class của object bằng cách sử dụng tính năng lifecycle. 

![](images/storage/image2019-7-3_14-17-42.png)

VNG Cloud object storage cung cấp 3 storage class là  **Gold** ,  **Silver**  và trong năm 2021 sẽ ra mắt  **vArchive**   **class ** 


*  **Standard class (hay còn gọi là Gold class) :** là lớp lưu trữ dành cho các dữ liệu thường xuyên truy cập như video, media, hình ảnh v…v…
*  **Silver class (New)**  : Lớp lưu trữ silver giúp KH tối ưu chi phí lưu trữ tự động bẳng cách chuyển các dữ liệu ít sử dụng từ gold sang. Silver class được thiết kế nhằm tối ưu chi phí lưu trữ thấp, nhưng vẫn đảm bảo performance đáp ứng được lượng request lớn / traffic lớn / truy cập ngay lập tức tương tự gold, giúp KH vừa tiết kiệm chi phí mà không cần lo lắng về performance của storage. Silver phù hợp với các dữ liệu ít sử dụng như video / film đã qua thời điểm hot, phù hợp với KH đang muốn giảm phí lưu trữ nhưng không xác định được dữ liệu nào ít truy cập. 
*  **Archive class:**  Lớp lưu trữ giá rẻ, bền bỉ cho các dữ liệu dài hạn ít truy cập như Log, backup, hồ sơ v…v…



|  **Standard class  (Gold class)**  |  **Silver class **  |  **Archive class (New)**  | 
| Object storage type | Object storage type | Object storage type | 
| Lớp lưu trữ dành cho các dữ liệu thường xuyên truy cập như video, media, hình ảnh v…v… | Silver class là giải pháp được thiết kế giúp khách hàng tối ưu chi phí lưu trữ tự động mà không bị ảnh hưởng đến performance hay gián đoạn dịch vụ. | Lớp lưu trữ giá rẻ, bền bỉ cho các dữ liệu dài hạn ít truy cập như Log, backup, hồ sơ bệnh án, v…v… | 
| Thời gian truy cập dữ liệu : Ngay lập tức  | Thời gian truy cập dữ liệu : Ngay lập tức  | Thời gian truy cập dữ liệu : chậm, tùy theo độ lớn dữ liệu.  | 
| N/A | URL object sau khi chuyển từ gold sang sẽ  **không thay đổi**  | Thay đổi URL.  | 
| Thời gian xóa dữ liệu, rotate dữ liệu: Ngay lập tức | Thời gian xóa dữ liệu, rotate dữ liệu: Ngay lập tức | Thời gian xóa dữ liệu: Chỉ dữ liệu có thời gian tồn tại đủ 6 tháng mới được xóa.  | 
| Khả năng mở rộng không giới hạn | Khả năng mở rộng không giới hạn | Khả năng mở rộng không giới hạn | 
| 99,99% availability SLA | 99,99% availability SLA | 99,99% availability SLA | 
| Chỉ từ 900đ/GB | Chỉ từ 630đ/GB | Chỉ từ 125đ/GB | 



Các lưu ý :

-   Nếu project vStorage bị delete


*  **Tất cả các class**  cũng sẽ bị delete, các object trong class cũng sẽ bị delete

Class được thể hiện qua type của container. Để lựa chọn đúng class bạn muốn lưu trữ, khi tạo container hãy chọn class mình mong muốn 





*****

[[category.storage-team]] 
[[category.confluence]] 
