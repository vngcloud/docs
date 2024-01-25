 **Khởi tạo container segment:**  ** ** 

Container segment được khởi tạo cùng với container gốc (tạo thông qua portal) hoặc tạo khi cần lưu segments (tạo qua các client tool).

Các large object khi được upload sẽ được phân ra thành nhiều segments để tải lên. Các segments này được lưu vào 1 container segments. Trong khi đó, container gốc chứa 1 file manifest liên kết với nội dung của các segments. Tên của object segments được giữ nguyên hoặc mã hóa base64 tùy vào cách hành xử của client tool dùng để upload.

vStorage đang hỗ trợ 2 loại container segment với suffix: _segments, +segments. Mỗi client tool sẽ tương tác với mỗi loại container segment này tùy theo đặc tính riêng của client tool.

Ví dụ:

![](images/storage/image2022-8-30_15-19-52.png)



![](images/storage/image2022-8-30_15-17-19.png)

![](images/storage/image2022-8-30_15-20-25.png)

![](images/storage/image2022-8-30_15-20-59.png)

 **Tải tập tin lên container segment:**  ** ** 

Người dùng có thể upload tập tin lên container segment giống như container gốc.

Trường hợp tập tin được upload là một large object, một container segment khác sẽ được tạo cho container này để lưu các object segments

![](images/storage/image2022-8-30_15-32-19.png)

![](images/storage/image2022-8-30_15-32-48.png)

![](images/storage/image2022-8-30_15-33-15.png)



 **Xóa tập tin trong container segment:**  ** ** 

Container segment hỗ trợ tính năng xóa tập tin và thư mục tương tự container gốc. Tuy nhiên, cần cân nhắc khi xóa các tập tin segments vì sẽ làm mất nội dung của tập tin manifest đang lưu ở container gốc. Từ đó làm hỏng tập tin gốc ban đầu được tải lên.



 **Xóa container segment:**  ** ** 

Hiện tại, vStorage chưa hỗ trợ việc xóa container segments.





*****

[[category.storage-team]] 
[[category.confluence]] 
