
## OpenVPN
OpenVPN được viết bởi James Yonan và được phát hành theo giấy phép mã nguồn mở GNU GPL. Một số điểm mạnh khi triển khai OpenVPN như:


* Hoạt động tại lớp 2 và lớp 3 trong mô hình OSI có thể vận chuyển các frame, packet và cả NETBIOS (Windows Network Browsing packets) giúp giải quyết được vấn đề thường gặp trong các giải pháp VPN khác.
* Kết nối sử dụng OpenVPN có thể tương thích tốt với hầu hết các thiết bị tường lửa, proxy. Nếu bạn có thể kết nối đến các máy tính từ xa thông qua giao thức HTTPS thì bạn cũng có thể sử dụng OpenVPN để thiết lập đường truyền VPN.
* Có thể hoạt động với giao thức UDP hoặc TCP. OpenVPN sử dụng port 1194 UDP và 443 TCP.
* Hiệu suất sử dụng cao: OpenVPN hỗ trợ nén các dữ liệu tại phía đầu cuối trước khi truyền đi qua môi trường mạng (sử dụng thư viện LZO).
* Hỗ trợ cài đặt trên nhiều nền tảng khác nhau: việc triển khai OpenVPN tại phía server lẫn phía người dùng đều khá dễ dàng so với IPSec. OpenWrt/FreeWrt là những hệ điều hành được tích hợp trên thiết bị phần cứng cũng hoạt động khá ổn định khi sử dụng OpenVPN.

![](images/storage/)

OpenVPN trong pfSense.

Việc cài đặt OpenVPN trong pfSense không quá phức tạp với một số bước cơ bản như sau:


* Tạo CA (Certificate Authority) và Certificates trong System à Manager.
* Tạo user để đăng nhập VPN trong System à User Manager.
* Cấu hình OpenVPN Server tại VPN à OpenVPN với một số thông số như phương pháp xác thực, CA, Certificates, mạng, firewall rule,…
* Cài đặt gói tin openvpn-client-export và trích xuất cấu hình đăng nhập OpenVPN.
* Từ máy tính muốn kết nối VPN, tải file đã export và import vào phần mềm OpenVPN tải từ [openvpn.net](http://openvpn.net), đăng nhập sử dụng tài khoản và mật khẩu đã tạo.


## Cài đặt OpenVPN pfSense
![](images/storage/)

Mô hình kết nối triển khai OpenVPN trên pfSense.

PfSense 2 sẽ là OpenVPN Server, máy tính Windows 7 là OpenVPN Client. Từ giao diện cấu hình web pfSense 2, ta bắt đầu cấu hình OpenVPN, với bước đầu tiên là tạo CA. Ta vào System à Cert. Manager và thêm một CA mới như sau:

![](images/storage/)

Tạo CA.

Sau đó ta chuyển sang tab Certificates để thêm certificate cho OpenVPN Server, ở mục Certificate authority chọn CA đã tạo trước đó, mục Certificate Type chọn Server Certificate:

![](images/storage/)

Tạo certificate cho OpenVPN Server.

Bây giờ chúng ta sẽ tạo VPN User. Vào menu System à User Manager à Users và chọn vào Add:

![](images/storage/)

Thêm user OpenVPN sangpn.

Sau khi hoàn thành, chúng ta cần trở về System à Certificate Manager à Certificates và tạo User Certificate cho user sangpn. Ở mục Certificate Type chọn User Certificate. Sau khi hoàn thành chọn Save để lưu lại:

![](images/storage/)

Tạo certificate cho user sangpn.

Trở về menu System à User Manager à Users và bấm vào Edit của user sangpn và gán certificate vừa tạo cho user này. Ở mục User Certificates, chọn Add và chọn certificate chúng ta vừa tạo để gán:

![](images/storage/)

Thêm certificate cho user sangpn.

Tiếp theo ta cài đặt gói openvpn-client-export cho pfSense để xuất file cấu hình OpenVPN cho user sử dụng. Ta chọn System à Package Manager à Available Packages và nhập openvpn-client-export để tìm kiếm gói và tải về:

![](images/storage/)

Cài đặt gói openvpn-client-export.

Tiếp theo di chuyển đến menu VPN à OpenVPN à và chọn mục Wizards. Ở mục Type of Server, chọn Local User Access và chọn Next để tiếp tục:

![](images/storage/)

Bắt đầu cấu hình OpenVPN Server.

Ở mục Certificate Authority, chúng ta chọn pfsenseCA vừa tạo lúc đầu và tiếp tục chọn Next:

![](images/storage/)

Chọn CA.

Chuyển đến Server Certificate Selection, ở mục Certificate, chọn certificate openvpnCert:

![](images/storage/)

Chọn certification cho OpenVPN Server.

Tiếp theo ta điền thông tin đường mạng riêng (Tunnel Network) cho VPN, Local Network đặt dải LAN, Concurrent Connections nhập số kết nối đồng thời đến OpenVPN Server và chọn Next:

![](images/storage/)

Điền các thông tin về network.

Ta tích chọn tạo các rule firewall tương ứng, chọn Next sau đó Finish để kết thúc quá trình cài đặt:

![](images/storage/)

Tạo các firewall rule tương ứng.

Tiếp theo ta cần xuất file cấu hình OpenVPN để cài đặt trên Client. Ta vào tab Client Export trong OpenVPN, kéo xuống dưới và chọn file thích hợp, ở đây ta chọn Windows Vista and Later. Sau đó copy file cấu hình này và tiến hành cài đặt ở OpenVPN Client:

![](images/storage/)





Xuất file cấu hình cho OpenVPN Client.

Từ máy Windows 7, ta chạy phần mềm OpenVPN với file cấu hình đã import, nhập user và password  đã tạo (sangpn), kết quả đã kết nối tới OpenVPN Server thành công:

![](images/storage/)

Kết nối VPN thành công.

Lúc này ta thử ping đến IP LAN của pfSense 2 thấy đã thông:

![](images/storage/)



*****

[[category.storage-team]] 
[[category.confluence]] 
