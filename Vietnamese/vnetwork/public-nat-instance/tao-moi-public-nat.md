# Tạo mới Public NAT

* Người dùng login vào [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/) với region = HCM
* Chọn menu “**Public NAT Instance**” tại thanh menu bên trái màn hình
* Chọn chức năng “**Create a Public NAT**”
* Nhập thông tin NAT theo yêu cầu gồm:
  * Tên NAT
  * Gói dịch vụ
  * VPC, Subnet
* Kiểm tra thông tin giá dịch vụ tại phần “**Summary**”
* &#x20;Nhấn “**TẠO PUBLIC NAT**”

Khi NAT được tạo thành công, người dùng sẽ thấy NAT xuất hiện trên màn hình danh sách NAT.

Người dùng cần thực hiện bước cấu hình các VM nào sẽ đi qua NAT bằng cách sử dụng NAT IP gateway theo cú pháp của OS Linux

_`ip route add <internet_ip> via <nat_gateway_ip> dev <interface>`._

* `<internet_ip>`: IP internet, ví dụ : 0.0.0.0/0
* `<nat_gateway_ip>`: IP gate way được cung cấp trên màn hình chi tiết thông tin NAT sau khi NAT được tạo thành công
* dev `<interface>`: Device private interface của VM kết nối với NAT&#x20;

Dưới đây là ví dụ add route trên VM với OS Linux theo cú pháp ở trên: _ip route add 0.0.0.0/0 via 10.0.0.100 dev eth0_

Trong trường hợp đã tồn tại route ra internet thông qua một gateway IP khác thì người dùng phải phải remove route hiện tại và add route mới đến NAT gateway IP.&#x20;

_<mark style="color:blue;">Lưu ý:</mark>_

* _<mark style="color:blue;">Public interface của NAT được tạo tự động khi NAT được tạo thành công, người dùng có thể cấu hình public IP vào các gói</mark>_ [_<mark style="color:blue;">bandwidth</mark>_](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/network/bandwidth-hcm-03/dich-vu-datatransfers-bandwidth) _<mark style="color:blue;">đã mua (nếu có) để tăng băng thông cho NAT.</mark>_
* _<mark style="color:blue;">NAT chỉ kết nối với internet qua port 80, 443</mark>_

