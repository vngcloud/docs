
# Default MTU:
Default MTU của Pfsense là  **1500** . Bạn cần chỉnh thông số này cho phù hợp cấu hình của VNG Cloud là  **1450** .

Để update thông số này, bạn truy cập vào WebGUI. Bạn tham khảo link sau để bật WebGUI: [[Khởi tạo Pfsense trên HCM03|Khởi-tạo-Pfsense-trên-HCM03]].

Tại WebGui:


*  **Bước 1:**  Truy cập vào giao diện quản lý của pfsense, chọn tab interfaces và cấu hình lần lượt cho mạng WAN (hoặc LAN đang sử dụng).




*  **Bước 2:** Tại mục MTU, bạn điền thông số 1450.



Cuối cùng, nhấn  **_Save _** để lưu lại cấu hình.

Bạn thực hiện lần lượt cho các Interfaces đang sử dụng. 

Nếu có khó khăn trong quá trình sử dụng, vui lòng liên hệ VNGCloud Support.





*****

[[category.storage-team]] 
[[category.confluence]] 
