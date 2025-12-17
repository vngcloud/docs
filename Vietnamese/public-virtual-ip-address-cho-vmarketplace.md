---
description: I. Mục đích
---

# Public Virtual IP Address cho vMarketplace

Virtual IP được sử dụng chủ yếu để:

**1. Đảm bảo High Availability (HA)**

* Khi server chính gặp sự cố, VIP tự động chuyển sang server dự phòng
* Dịch vụ vẫn hoạt động liên tục, người dùng không bị gián đoạn

**2. Load Balancing**

* Phân phối traffic đến nhiều server backend
* Tối ưu hiệu suất và tránh quá tải

**3. Đơn giản hóa quản lý**

* Người dùng chỉ cần truy cập một IP duy nhất
* Admin có thể thay đổi server backend mà không ảnh hưởng đến client

II. Mục tiêu tài liệu

Tài liệu này nhằm hướng dẫn khách hàng:

·       Hiểu và sử dụng tính năng Virtual IP Address(es) trên vMarketplace.

·       Sử dụng pfSense như một Internet Gateway.

III. Các bước thực hiện:

1. Standalone Mode (Single Firewall)

Đặc điểm Standalone Mode:

**✓ Ưu điểm:**

* Cấu hình đơn giản, dễ triển khai
* Chi phí thấp (chỉ cần 1 firewall VM)
* Phù hợp cho môi trường dev/test hoặc ứng dụng nhỏ

**✗ Nhược điểm:**

* Không có failover - nếu firewall VM die thì mất kết nối
* Single Point of Failure (SPOF)
* Downtime khi bảo trì hoặc restart firewall

**🔄 Luồng traffic:** Internet → VIP (157.20.200.185) → Firewall VM (NAT + Filter) → Application Server (192.168.2.5)

Bước 1: Tiến hành khởi tạo Virtual IP Address trên portal VNG Cloud

Truy cập vào [vServer Portal - Create-virtual-ip-address](https://hcm-3.console.vngcloud.vn/vserver/network/virtual-ip-address), chọn Virtual IP Address type là Public Market Place sau đó điền các thông tin theo yêu cầu

<figure><img src=".gitbook/assets/image (466).png" alt=""><figcaption></figcaption></figure>

Bước 2: Tiến hành allow address pair cho VIP với External IP Marketplace

Sau khi tạo xong VIP dạng public marketplace khách hàng tiến hành thực hiện allow address pair bằng cách chọn Add Address Pair Interface để hiển thị pop-up và chọn External IP Marketplace của Pfsense

<figure><img src=".gitbook/assets/image (1) (6).png" alt=""><figcaption></figcaption></figure>
