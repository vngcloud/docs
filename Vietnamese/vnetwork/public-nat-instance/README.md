# Public NAT Instance

Public NAT instance trên GreenNode là dịch vụ mạng cho phép các máy ảo (instance) trong một subnet riêng (private subnet) kết nối ra internet, đồng thời ngăn chặn các kết nối từ internet chủ động đi vào các máy ảo đó.

Public NAT Instance **V2** là thế hệ mới của dịch vụ. Các Public NAT tạo mới sẽ mặc định là V2; các instance V1 đang có vẫn tiếp tục hoạt động bình thường.

## Điểm mới ở V2

{% hint style="success" %}
**Tính sẵn sàng cao (High Availability)**

V2 hoạt động theo cặp dự phòng (active/standby) và tự động chuyển đổi dự phòng (failover). Khi một node gặp sự cố, lưu lượng vẫn tiếp tục đi qua node còn lại mà không cần thao tác thủ công, loại bỏ điểm lỗi đơn (single point of failure) từng tồn tại ở V1.
{% endhint %}

{% hint style="success" %}
**Tự động định tuyến (Automatic routing)**

Ở V1, người dùng phải đăng nhập vào từng máy ảo để cấu hình route trỏ tới NAT gateway theo cách thủ công. Ở V2, GreenNode **tự động** thêm route mặc định vào bảng định tuyến (route table) của VPC ngay khi NAT được tạo, nhờ đó mọi máy ảo đều ra được internet qua NAT mà **không cần cấu hình trên từng máy ảo**.
{% endhint %}

{% hint style="success" %}
**Hoạt động trên toàn VPC**

Ở V1, chỉ các máy ảo **cùng subnet** với NAT mới đi ra internet qua NAT được. Ở V2, **mọi máy ảo trong cùng VPC (toàn dải /16)** đều có thể ra internet qua NAT — không chỉ subnet của NAT.
{% endhint %}

{% hint style="info" %}
**Phân biệt V1 và V2**

Trong danh sách **Public NAT**, xem cột **HA**: **HA = Yes** nghĩa là NAT thuộc **V2** (tính sẵn sàng cao); **HA = No** nghĩa là NAT **V1**.
{% endhint %}

_Cột HA trên danh sách Public NAT: Yes = V2, No = V1_

## Bảng so sánh tính năng

| Tính năng                               | V1 (cũ)                 | V2                                    |
| --------------------------------------- | ----------------------- | ------------------------------------- |
| Tính sẵn sàng cao / chuyển đổi dự phòng | Một node duy nhất       | Cặp dự phòng, tự động failover        |
| Máy ảo nào dùng được NAT                | Chỉ cùng subnet (/24)   | Toàn VPC (/16)                        |
| Định tuyến cho máy ảo                   | Thủ công, trên từng máy | Tự động, thêm vào route table của VPC |
| Interface public                        | Tự động tạo             | Tự động tạo                           |
| Dịch vụ mở sẵn (từ VPC của bạn)         | DNS, HTTP, HTTPS, ICMP  | DNS, HTTP, HTTPS, ICMP                |
| Thêm / xóa inbound rule                 | Có                      | Có                                    |
