# Public Virtual IP Address cho vMarketplace

## I. Mục đích

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

## II. Mục tiêu tài liệu

Tài liệu này nhằm hướng dẫn khách hàng:

·       Hiểu và sử dụng tính năng Virtual IP Address(es) trên vMarketplace.

·       Sử dụng pfSense như một Internet Gateway.

III. Các bước thực hiện:

1. Standalone Mode (Single Firewall)

Đặc điểm Standalone Mode:

**Ưu điểm:**

* Cấu hình đơn giản, dễ triển khai
* Chi phí thấp (chỉ cần 1 firewall VM)
* Phù hợp cho môi trường dev/test hoặc ứng dụng nhỏ

**Nhược điểm:**

* Không có failover - nếu firewall VM die thì mất kết nối
* Single Point of Failure (SPOF)
* Downtime khi bảo trì hoặc restart firewall

**Luồng traffic:** Internet → VIP (157.20.200.185) → Firewall VM (NAT + Filter) → Servers (192.168.2.7, 192.168.2.5)

Bước 1: Tiến hành khởi tạo Virtual IP Address trên portal VNG Cloud

Truy cập vào [vServer Portal - Create-virtual-ip-address](https://hcm-3.console.vngcloud.vn/vserver/network/virtual-ip-address), chọn Virtual IP Address type là Public Market Place sau đó điền các thông tin theo yêu cầu

<figure><img src=".gitbook/assets/image (466).png" alt=""><figcaption></figcaption></figure>

Bước 2: Tiến hành allow address pair cho VIP với External IP Marketplace

Sau khi tạo xong VIP dạng public marketplace khách hàng tiến hành thực hiện allow address pair bằng cách chọn Add Address Pair Interface để hiển thị pop-up và chọn External IP Marketplace của Pfsense

<figure><img src=".gitbook/assets/image (1) (6).png" alt=""><figcaption></figcaption></figure>

Kiểm tra đã allow address thành công hay chưa

\*Lưu ý: Lưu VIP lại để cấu hình VIP bên trong Pfsense ở các bước sau

<figure><img src=".gitbook/assets/image (476).png" alt=""><figcaption></figcaption></figure>

Bước 3: Tiến hành khởi tạo VIP trong pfsense

Truy cập vào Pfsense vào Firewall -> Virtual IPs sau đó nhấn vào nút Add

Tại giao diện cấu hình Virtual IP tiến hành điền các thông tin theo yêu cầu

\*Tại mục Address(es) khách hàng cần điền địa chỉ của VIP đã khởi tạo trên portal VNG Cloud tại Bước 2

<figure><img src=".gitbook/assets/image (480).png" alt=""><figcaption></figcaption></figure>

Kiểm tra VIP trong pfsense

<figure><img src=".gitbook/assets/image (483).png" alt=""><figcaption></figcaption></figure>

Bước 4: Tạo rule NAT cho IP/Subnet ra internet theo IP chỉ định

1. Chuyển Mode Manual Outbound NAT

<figure><img src=".gitbook/assets/image (485).png" alt=""><figcaption></figcaption></figure>

2. Tạo rule NAT&#x20;

<figure><img src=".gitbook/assets/image (491).png" alt=""><figcaption></figcaption></figure>

3. Cấu hình rule NAT

Tạo rule theo yêu cầu:

Server (192.168.2.5) đứng sau pfsense: Rule đi internet với Virtual IP Address 157.20.200.185

<figure><img src=".gitbook/assets/image (494).png" alt=""><figcaption></figcaption></figure>

Bước 4: Truy cập vào 2 server (192.168.2.7, 192.168.2.5) và sử dụng curl ifconfig.me để kiểm tra kết quả

<figure><img src=".gitbook/assets/image (543).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (544).png" alt=""><figcaption></figcaption></figure>

Lúc này server (192.168.2.7, 192.168.2.5) đã ra được internet với Virtual IP Address, traffic cũng đi qua pfsense, ngoài ra có thể vào webGUI của pfsense bằng Virtual IP address này.&#x20;

<figure><img src=".gitbook/assets/image (542).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (541).png" alt=""><figcaption></figcaption></figure>

2. **High Availability (HA) Mode (2+ Firewall VM)**

**a. Đặc điểm:**

* VIP được chia sẻ giữa **2 hoặc nhiều firewall**
* Có cơ chế failover tự động

**b. Khi nào dùng:**

* Production environment
* Dịch vụ mission-critical (không được phép downtime)
* Yêu cầu SLA cao (99.9% uptime trở lên)

**Ưu điểm:**

* Server chính die → VIP tự động chuyển sang server backup
* Zero downtime hoặc downtime tối thiểu (vài giây)

**Cấu hình phổ biến:**

* **Active-Passive**: 1 server chính xử lý, 1 server dự phòng chờ sẵn
* **Active-Active**: Cả 2 servers cùng xử lý (kết hợp load balancing)

Hiện tại Virtual IP Address cho vMarketplace đang hỗ trợ cấu hình **Active-Passive**













