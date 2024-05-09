# Pfsense as a NAT Gateway

### 2. Pfsense <a href="#toc165621059" id="toc165621059"></a>

### Khởi tạo Pfsense trên vMarketplace <a href="#toc165621060" id="toc165621060"></a>

Bước 1: Khách hàng cần đặt tên và chọn version cho Pfsense

Bước 2: Chọn cấu hình cho Pfsense

Bước 3: Chọn Volume, Network, Security Group

### II. Truy cập vào GUI Pfsense <a href="#toc165621061" id="toc165621061"></a>

Bước 1: Truy cập vào GUI bằng IP của External Interface đăng nhập với Tên đăng nhập và mật khẩu mặc định là admin/pfsense

* Để lấy thông tin IP này khách hàng vào phần Network Interface của Pfsense để xem thông tin

Bước 2: Tiến hành General Setup, khách hàng vui lòng thực hiện như bên dưới

* Cấu hình cho WAN Interface
* Thay đổi password vào GUI
* Tiến hành reload
* Đã hoàn thành General Setup

Bước 3: Mở rule trên firewall

* Tiến hành Add rule
* Khách hàng có thể mở rule như bên dưới để truy cập vào GUI bằng External Interface.

Lưu ý: Khách hàng nên giới hạn lại Range IP được phép kết nối tới GUI Pfsense để hạn chế user được phép truy cập vào GUI Pfsense

* Chọn save
* Sau đó chọn Apply change

Bước 4: Cấu hình Interface LAN

* Vào phần Interfaces -> Assignments để gắn thêm Interface LAN
* Nhấn vào Add
* Sau đó nhấn vào Save
* Vào phần Interfaces -> Assignments để tiến hành enable LAN Interface
* Khách hàng thực hiện cấu hình như bên dưới
* Cấu hình IP cho LAN
* Sau đó tiến hành add gateway
* Tiến hành save lại

Bước 5: Xem lại thông tin cấu hình

Bước 6: Mở rule đi ra Internet cho interface LAN

* Tại source khách hàng chọn dải IP được phép đi ra Internet

Bước 7: Cấu hình NAT để các vServer có thể đi ra được Internet

* Vào mục Firewall -> NAT
* Chọn mode NAT sau đó tiến hành cấu hình NAT
* Nhấn vào Add để thêm rule
* Chọn source, destination NAT

Bước 8: Tiến hành cấu hình route table trên portal VNG Cloud

Bước 9: Vào vServer tiến hành ping google.com hoặc 8.8.8.8 để kiểm tra

* Trước khi Enable NAT server không ra được internet
* Sau khi cấu hình NAT tiến hành ping 8.8.8.8 để kiểm tra
