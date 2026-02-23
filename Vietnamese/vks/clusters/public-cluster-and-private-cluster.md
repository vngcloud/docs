# Public Cluster và Private Cluster

Dưới đây là các khái niệm hiện tại đang được VKS cung cấp cho bạn:

## **1. Public Cluster** <a href="#id-1.-public-cluster" id="id-1.-public-cluster"></a>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fvbnmi3cReXehXboTd85R%252Fimage.png%3Falt%3Dmedia%26token%3D618fbb97-4bd7-4612-be3a-0e6d3ea40021&width=768&dpr=4&quality=100&sign=9119e8dd&sv=1" alt=""><figcaption></figcaption></figure>

Khi bạn tạo một **Public Cluster với Public Node Group**, hệ thống VKS sẽ:

* Tạo VM với Floating IP (tức là Public IP). Lúc này các VM (Node) này có thể trực tiếp tham gia vào cụm K8S thông qua Public IP này. Bằng cách sử dụng Public Cluster và Public Node Group, bạn có thể dễ dàng tạo các cụm Kubernetes và expose các dịch vụ mà không cần sử dụng Load Balancer. Điều này sẽ góp phần tiết kiệm chi phí cho cụm của bạn.

Khi bạn tạo một **Public Cluster với Private Node Group**, hệ thống VKS sẽ:

* Tạo VM không có Floating IP (tức là không có Public IP). Lúc này các VM (Node) này không thể tham gia trực tiếp vào cụm K8S. Để các VM này có thể tham gia vào cụm K8S, bạn cần sử dụng NAT Gateway (**NATGW**). **NATGW** đóng vai trò như một trạm trung chuyển, cho phép các VM kết nối tới cụm K8S mà không cần Public IP. Với VNG Cloud, chúng tôi khuyến nghị bạn sử dụng Pfsense hoặc Palo Alto làm NATGW cho Cluster của bạn. Pfsense sẽ giúp bạn quản lý lưu lượng mạng đến và đi (inbound và outbound traffic) một cách hiệu quả, đảm bảo an ninh mạng và quản lý truy cập. Ngoài ra, việc sử dụng Private Node Group sẽ giúp bạn kiểm soát các ứng dụng trong cụm an toàn hơn, cụ thể bạn có thể giới hạn quyền truy cập control plane thông qua tính năng Whitelist IP.

## **2. Private Cluster** <a href="#id-2.-private-cluster" id="id-2.-private-cluster"></a>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fj8WSjgnwd7WXKXblh1ex%252Fimage.png%3Falt%3Dmedia%26token%3Dae664224-8486-495b-aab6-5d1d1017edec&width=768&dpr=4&quality=100&sign=8c00454b&sv=1" alt=""><figcaption></figcaption></figure>

Khi bạn tạo một **Private Cluster với Public/Private Node Group**, hệ thống VKS sẽ:

* Để tăng cường bảo mật cho cụm của bạn, chúng tôi đã giới thiệu mô hình private cluster. Tính năng Private Cluster giúp cho cụm K8S của bạn an toàn nhất có thể, tất cả các kết nối đều hoàn toàn riêng tư từ kết nối giữa các node tới control plane, kết nối từ client tới control plane, hay kết nối từ các node tới các sản phẩm. Các dịch vụ khác trong VNG Cloud như: vStorage, vCR, vMonitor, VNG Cloud APIs,... Private Cluster là lựa chọn lý tưởng cho **các dịch vụ yêu cầu kiểm soát truy cập nghiêm ngặt, đảm bảo tuân thủ các quy định về bảo mật và quyền riêng tư dữ liệu**.

## 3. So sánh giữa việc sử dụng Public Cluster và Private Cluster <a href="#id-3.-so-sanh-giua-viec-su-dung-public-cluster-va-private-cluster" id="id-3.-so-sanh-giua-viec-su-dung-public-cluster-va-private-cluster"></a>

Dưới đây là bảng so sánh giữa việc tạo và sử dụng Public Cluster và Private Cluster trên hệ thống VKS:

<table data-header-hidden><thead><tr><th width="201"></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Tiêu chí</strong></td><td><strong>Public Cluster</strong></td><td><strong>Private Cluster</strong></td></tr><tr><td><strong>Kết nối</strong></td><td>Sử dụng địa chỉ IP Public để giao tiếp giữa các node và control plane, giữa client và control plane, giữa các node và các dịch vụ khác trong VNG Cloud.</td><td>Sử dụng địa chỉ IP Private để giao tiếp giữa các node và control plane, giữa client và control plane, giữa các node và các dịch vụ khác trong VNG Cloud.</td></tr><tr><td><strong>Bảo mật</strong></td><td>Bảo mật ở mức trung bình vì các kết nối sử dụng IP Public.</td><td>Bảo mật cao hơn với tất cả các kết nối đều riêng tư và truy cập bị hạn chế.</td></tr><tr><td><strong>Quản lý truy cập</strong></td><td>Khó kiểm soát hơn, có thể quản lý truy cập thông qua tính năng Whitelist</td><td>Kiểm soát truy cập nghiêm ngặt, tất cả các kết nối đều nằm trong mạng riêng của VNG Cloud, qua đó giảm thiểu rủi ro bị tấn công từ mạng bên ngoài.</td></tr><tr><td><strong>Khả năng mở rộng (AutoScaling)</strong></td><td>Dễ dàng mở rộng thông qua tính năng <strong>Auto Scaling</strong>.</td><td>Dễ dàng mở rộng thông qua tính năng <strong>Auto Scaling</strong>.</td></tr><tr><td><strong>AutoHealing</strong></td><td>Tự động phát hiện lỗi và khởi động lại node (<strong>Auto Healing</strong>)</td><td>Tự động phát hiện lỗi và khởi động lại node (<strong>Auto Healing</strong>)</td></tr><tr><td><strong>Khả năng truy cập từ bên ngoài</strong></td><td>Dễ dàng truy cập từ bất kỳ đâu có internet.</td><td>Truy cập từ bên ngoài phải thông qua các giải pháp bảo mật khác.</td></tr><tr><td><strong>Cấu hình và triển khai</strong></td><td>Đơn giản hơn vì không cần thiết lập mạng nội bộ.</td><td>Phức tạp hơn, yêu cầu cấu hình mạng riêng tư và bảo mật.</td></tr><tr><td><strong>Chi phí</strong></td><td>Thường thấp hơn vì không cần thiết lập cơ sở hạ tầng bảo mật phức tạp.</td><td>Chi phí cao hơn do yêu cầu thêm các thành phần bảo mật và quản lý. <strong>Cụ thể, khi sử dụng private cluster, bạn cần trả phí cho 4 private service endpoint được tạo tự động để kết nối tới các dịch vụ trên VNG Cloud.</strong></td></tr><tr><td><strong>Tính linh hoạt</strong></td><td>Cao, dễ dàng thay đổi và truy cập các dịch vụ.</td><td>Linh hoạt hơn trong các ứng dụng yêu cầu bảo mật, nhưng ít linh hoạt hơn cho các ứng dụng cần truy cập từ bên ngoài.</td></tr></tbody></table>

Do đó:

* **Public Cluster**: Phù hợp cho các ứng dụng không yêu cầu bảo mật cao và cần sự linh hoạt, truy cập từ nhiều vị trí. Dễ triển khai và quản lý nhưng có rủi ro bảo mật cao hơn.
* **Private Cluster**: Phù hợp cho các ứng dụng yêu cầu bảo mật cao, tuân thủ nghiêm ngặt các quy định về bảo mật và quyền riêng tư. Cung cấp kết nối ổn định và an toàn, nhưng yêu cầu cấu hình và quản lý phức tạp hơn, cũng như chi phí cao hơn.
