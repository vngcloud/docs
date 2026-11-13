# Security Group

Security Group (SG) đóng vai trò firewall, kiểm soát traffic vào và ra máy chủ (VM). Khi bạn tạo cluster và expose ứng dụng qua load balancer, VKS tự động tạo và gắn một số SG lên worker node để cluster hoạt động. Trang này mô tả các SG đó, các rule bên trong, và những gì VKS tự động khôi phục nếu bạn thay đổi.

Trên một worker node thường có các SG sau:

| SG | Ai tạo | Định dạng tên | Số lượng |
|---|---|---|---|
| Node SG của cluster | VKS, khi tạo cluster | `vks-user-<user ID>-k8s-<cluster ID>-<chuỗi ngẫu nhiên>` | 1 SG cho mỗi cluster |
| SG của load balancer | GreenNode LoadBalancer Controller, khi tạo Service `LoadBalancer` hoặc Ingress | `vks-<cluster ID rút gọn>-<namespace>-<tên Service/Ingress>-<hash>` | 1 SG cho mỗi Service `LoadBalancer` / Ingress |
| SG do bạn tự gắn | Bạn | Theo tên bạn đặt | Tuỳ bạn |

{% hint style="info" %}
**Lưu ý:**

* Traffic được cho phép nếu **bất kỳ** SG nào gắn trên VM cho phép.
* SG hoạt động theo cơ chế stateful: return traffic của một connection đã được cho phép sẽ tự động được cho phép, không cần rule chiều ngược lại.
* Mỗi SG khi tạo mới đều có sẵn 2 rule outbound allow-all: `any → 0.0.0.0/0` (IPv4) và `any → ::/0` (IPv6).
* Mỗi VM chỉ gắn được một số lượng SG giới hạn theo quota của project. Mỗi Service `LoadBalancer` / Ingress gắn thêm 1 SG lên node; nếu chạm quota, controller không gắn được SG mới. Dùng chung SG qua annotation `vks.vngcloud.vn/security-groups` để tránh vượt quota (xem bên dưới).
{% endhint %}

## Node SG của cluster

Mỗi cluster có một node SG, được tạo cùng cluster và gắn lên tất cả worker node của mọi node group, kể cả node tạo sau này. Mô tả của SG: `Default worker security group for VKS cluster <tên cluster>. Please DO NOT DELETE it.`

Trong các bảng dưới, **`<Subnet CIDR>`** là CIDR của subnet mà node group sử dụng. Nếu các node group dùng nhiều subnet khác nhau, mỗi rule được tạo lặp lại cho từng subnet CIDR.

### Inbound — áp dụng cho mọi CNI

| Protocol | Ether type | Port range | Source | Ý nghĩa |
|---|---|---|---|---|
| TCP | IPv4 | 30000-32767 | `<Subnet CIDR>` | NodePort Service (TCP) |
| UDP | IPv4 | 30000-32767 | `<Subnet CIDR>` | NodePort Service (UDP) |
| TCP | IPv4 | 10250 | `<Subnet CIDR>` | Kubelet API |
| TCP | IPv4 | 10250 | `<IP endpoint control plane>/32` | Kubelet API từ control plane. Chỉ có khi endpoint control plane của cluster là địa chỉ IP |

### Inbound — bổ sung theo CNI

**Calico Overlay**

| Protocol | Ether type | Port range | Source | Ý nghĩa |
|---|---|---|---|---|
| TCP | IPv4 | 179 | `<Subnet CIDR>` | Calico BGP |
| 4 (IP-in-IP) | IPv4 | 1-65535 | `<Subnet CIDR>` | Calico IP-in-IP |
| TCP | IPv4 | 5473 | `<Subnet CIDR>` | Calico Typha |

**Cilium Overlay**

| Protocol | Ether type | Port range | Source | Ý nghĩa |
|---|---|---|---|---|
| UDP | IPv4 | 8472 | `<Subnet CIDR>` | Cilium VXLAN overlay |
| TCP | IPv4 | 4240 | `<Subnet CIDR>` | Cilium health check (TCP) |
| ICMP | IPv4 | 1-255 | `<Subnet CIDR>` | Cilium health check (ICMP) |

**Cilium VPC Native Routing**

| Protocol | Ether type | Port range | Source | Ý nghĩa |
|---|---|---|---|---|
| UDP | IPv4 | 8472 | `<Subnet CIDR>` | Cilium VXLAN |
| TCP | IPv4 | 4240 | `<Subnet CIDR>` | Cilium health check (TCP) |
| ICMP | IPv4 | 1-255 | `<Subnet CIDR>` | Cilium health check (ICMP) |
| TCP | IPv4 | 53 | `<Subnet CIDR>` | DNS (TCP) |
| UDP | IPv4 | 53 | `<Subnet CIDR>` | DNS (UDP) |

### Outbound

| Protocol | Ether type | Port range | Destination | Ý nghĩa |
|---|---|---|---|---|
| ANY | IPv4 | 0-65535 | 0.0.0.0/0 | Rule mặc định của mọi SG |
| ANY | IPv6 | 0-65535 | ::/0 | Rule mặc định của mọi SG |

### VKS tự động khôi phục những gì

VKS kiểm tra node SG định kỳ:

* **Inbound rule ở các bảng trên bị xoá hoặc sửa:** VKS tạo lại rule còn thiếu.
* **Rule bạn tự thêm** (inbound hoặc outbound): VKS giữ nguyên, không xoá.
* **Outbound rule mặc định:** VKS không quản lý. Nếu bạn xoá, VKS không tạo lại. Xem [Giới hạn outbound cho worker node](security-group/gioi-han-outbound-cho-worker-node.md) trước khi xoá.
* **Cả node SG bị xoá:** VKS tạo một node SG mới (kèm 2 outbound rule allow-all mặc định) và gắn lên các node. Mọi rule bạn tự thêm vào SG cũ, kể cả bộ outbound rule đã giới hạn, sẽ mất và cần cấu hình lại trên SG mới.

{% hint style="warning" %}
**Không xoá node SG của cluster.** Node SG được xoá cùng cluster. Xoá thủ công khiến cluster mất kết nối giữa các node cho tới khi VKS tạo SG mới, và cấu hình riêng của bạn trên SG cũ bị mất.
{% endhint %}

## SG của load balancer

Khi bạn tạo Service `type: LoadBalancer` (Network Load Balancer) hoặc Ingress (Application Load Balancer), GreenNode LoadBalancer Controller tạo một SG riêng cho Service/Ingress đó, với mô tả `Automatically created using VNGCLOUD LoadBalancer Controller`. SG được gắn lên tất cả worker node (hoặc chỉ các node khớp annotation `vks.vngcloud.vn/target-node-labels`), kể cả node tạo sau này.

Trong các bảng dưới, **`<LB Subnet CIDR>`** là CIDR của subnet mà load balancer dùng để kết nối tới node (backend subnet).

### Inbound — Service `LoadBalancer`

| Trường hợp | Protocol | Port | Source | Ý nghĩa |
|---|---|---|---|---|
| Mặc định (target type `instance`) | Theo protocol của port Service (TCP/UDP) | NodePort của từng port | `<LB Subnet CIDR>` | Load balancer truy cập NodePort |
| Target type `ip` | Theo protocol của port Service (TCP/UDP) | `targetPort` của pod | `<LB Subnet CIDR>` | Load balancer truy cập trực tiếp pod |
| Cluster dùng Cilium VPC Native Routing | Theo protocol của port Service (TCP/UDP) | `targetPort` của pod | Subnet CIDR của mọi node trong cluster | Node chuyển tiếp traffic tới pod ở node khác |
| Có annotation `vks.vngcloud.vn/healthcheck-port` | Theo protocol của port Service | Port health check đã khai báo | `<LB Subnet CIDR>` | Health check port tuỳ chỉnh |
| Service có port UDP | ICMP | 1-255 | Cùng source với rule UDP | Health check cho port UDP |

### Inbound — Ingress

Giống Service ở trên, áp dụng cho từng Service backend của Ingress (default backend và mọi path), với protocol luôn là TCP.

### Outbound

| Protocol | Ether type | Port range | Destination | Ý nghĩa |
|---|---|---|---|---|
| ANY | IPv4 | 0-65535 | 0.0.0.0/0 | Outbound mặc định |
| ANY | IPv6 | 0-65535 | ::/0 | Outbound mặc định |

Hai rule outbound này được tắt bằng annotation `vks.vngcloud.vn/enable-default-egress: "false"` trên Service/Ingress (yêu cầu GreenNode LoadBalancer Controller phiên bản `0.5.0` trở lên). Chi tiết tại [Giới hạn outbound cho worker node](security-group/gioi-han-outbound-cho-worker-node.md).

### VKS tự động khôi phục những gì

Controller quản lý **toàn bộ** rule (cả inbound và outbound) của SG này:

* Rule bị sửa hoặc xoá thủ công được khôi phục ở lần đồng bộ định kỳ kế tiếp. Rule bạn tự thêm vào SG này sẽ bị xoá.
* Khi bạn sửa Service/Ingress (port, annotation…), rule được cập nhật theo.
* Khi xoá Service/Ingress, SG được gỡ khỏi các node và bị xoá.

Vì vậy, **không sửa rule trực tiếp trên portal** cho SG này; luôn cấu hình qua annotation.

### Dùng SG của bạn thay cho SG tự động

Thêm annotation `vks.vngcloud.vn/security-groups: "<SG ID 1>,<SG ID 2>"` vào Service/Ingress:

* Controller không tạo SG riêng cho Service/Ingress đó; SG tự động đã có trước đó được gỡ khỏi node và xoá.
* Các SG bạn chỉ định được gắn lên các worker node (kể cả node mới) — **không** gắn lên load balancer.
* Controller **không đụng** tới rule của các SG này: bạn tự thêm rule inbound cho port Service (theo bảng trên) và tự quản lý outbound. Annotation `enable-default-egress` không có tác dụng trong trường hợp này.
* Có thể dùng chung một SG cho nhiều Service/Ingress để giảm số SG gắn trên mỗi node.

{% hint style="info" %}
Annotation `vks.vngcloud.vn/inbound-cidrs` (giới hạn IP client được truy cập load balancer) cấu hình ACL trên listener của load balancer, không thay đổi rule của SG.
{% endhint %}

## Câu hỏi thường gặp

**Tôi muốn chặn outbound của worker node ra internet?**
Xem [Giới hạn outbound cho worker node](security-group/gioi-han-outbound-cho-worker-node.md). Cần xử lý outbound trên **mọi** SG gắn trên node, không chỉ node SG.

**Tôi muốn thêm inbound rule cho ứng dụng (ví dụ mở port cho hệ thống khác trong VPC truy cập node)?**
Thêm rule vào node SG của cluster hoặc vào một SG riêng do bạn tạo và tự gắn lên node. Không thêm vào SG của load balancer vì controller sẽ xoá rule đó.

**Node mới tạo có tự động có đủ SG không?**
Có. Node SG của cluster và SG của load balancer được gắn tự động lên node mới. SG do bạn tự gắn thủ công lên VM **không** tự gắn lên node mới; dùng annotation `vks.vngcloud.vn/security-groups` nếu cần SG của bạn theo node.
