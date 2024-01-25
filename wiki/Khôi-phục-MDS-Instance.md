VNG Cloud vDB hỗ trợ bạn khôi phục (Restore) lại một MDS Instance mới từ bản sao lưu (Backup) trước đó. Quá trình khôi phục này không phụ thuộc vào cách tạo ra bản backup đó (Manual Backup hay Automactic Daily Backup).

Để thực hiện tiến trình khôi phục, bạn truy cập màn hình quản lý Backup.

Tại đây, bạn click chọn vào bản Backup mà bạn muốn khôi phục, chọn Action  **Restore** .

![](images/storage/image2020-2-21_10-45-27.png)



Quá trình Restore cũng gần tương tự như quá trình Tạo một MDS Instance mới.

Tại màn hình khôi phục MDS Instance, bạn cũng có thể lựa chọn các thông tin về cấu hình MDS Instance mới tại các thông tin  **Flavor** ,  **Storage Type**  &  **Storage Size**  trong mục  **MDS Instance Specifications** .

Tại mục  **Settings** , bạn có thể đặt tên cho MDS Instance mới này.

![](images/storage/image2020-2-21_10-46-5.png)



Tại mục  **Network & Security** , bạn có lựa chọn Cloud Network & bật/tắt khả năng truy cập từ Internet ( **Public Accessibility** ). Cloud Network ở đây có thể giống hoặc khác Cloud Network của MDS Instance cũ.

![](images/storage/image2020-2-21_10-47-23.png)



Tại mục DB Options, bạn có thể lựa chọn  **DB Configuration Group (Optional)**  cho MDS Instance này. Lựa chọn này cũng có thể giống hoặc khác so với MDS Instance cũ.

![](images/storage/image2020-2-21_10-46-57.png)



Sau khi chắc chắn các thông tin đã chính xác, bạn nhấp nút  **Restore Backup**  ở góc phải trên.

Sau đó, bạn quay lại màn hình quản lý Database, sẽ thấy xuất hiện một MDS Instance đang được khởi tạo.

![](images/storage/image2020-2-21_10-48-22.png)



Trạng trái của MDS Instance mới này cũng sẽ thay đổi từ Building/Build sang Active nếu thành công.

Khi khôi phục thành công, MDS Instance mới sẽ có trạng thái  **Active** .

![](images/storage/image2020-2-21_10-51-24.png)



Chúc mừng bạn đã khôi phục dữ liệu thành công với tính năng Restore của vDBaaS.

Bạn có thể tham khảo video sau:



6001200https://www.youtube.com/embed/ZpN6fekI3EkINLINE





*****

[[category.storage-team]] 
[[category.confluence]] 
