# Thêm/ Xóa NAT Port

Inbound rule quy định cổng và giao thức nào được đi qua NAT. Mỗi NAT khi tạo đều có sẵn bộ rule mặc định cho phép các dịch vụ ra ngoài phổ biến từ VPC — DNS (UDP 53), HTTP (TCP 80), HTTPS (TCP 443) và ICMP (ping). Bạn có thể thêm rule khi cần hoặc xóa rule không dùng nữa.

Mở NAT từ danh sách và vào màn hình chi tiết để xem mục Inbound Rules, cùng NAT Gateway IP và Public IP của NAT.

## Thêm cổng NAT

* Ở danh sách NAT, chọn NAT muốn thêm cổng.
* Nhấn tên NAT để mở màn hình chi tiết.
* Vào mục Inbound Rules và nhấn "Create an Inbound Rule".
* Nhập các trường: Protocol, Ether Type, Port range, Description.
* Nhấn "Create".

## Xóa cổng NAT

{% hint style="warning" %}
Không thể xóa các rule do hệ thống tạo (các rule mặc định DNS / HTTP / HTTPS / ICMP).
{% endhint %}

* Ở danh sách NAT, chọn NAT muốn xóa cổng.
* Nhấn tên NAT để mở màn hình chi tiết.
* Vào mục Inbound Rules.
* Tìm rule cần xóa và nhấn biểu tượng xóa.
