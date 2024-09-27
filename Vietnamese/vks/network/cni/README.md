# CNI

## **Tổng quan**

**CNI (Container Network Interface)** là một bộ công cụ tiêu chuẩn cung cấp khả năng kết nối mạng cho các container trong một cụm Kubernetes. Nói một cách đơn giản, CNI là một lớp trừu tượng, giúp Kubernetes quản lý và cấu hình mạng cho các pod (một tập hợp các container chia sẻ cùng một mạng) một cách linh hoạt và hiệu quả.

### CNI hoạt động như thế nào?

Khi bạn tạo một pod mới, Kubernetes sẽ gọi đến CNI để tạo một mạng interface cho pod đó. Plugin CNI sẽ thực hiện các tác vụ sau:

* **Cấp phát địa chỉ IP:** Gán một địa chỉ IP duy nhất cho pod.
* **Cấu hình routing:** Thiết lập các quy tắc routing cho phép giao tiếp giữa các pod,...

***

## So sánh giữa các plugin CNI

Hiện tại, VKS đang cung cấp 3 plugin CNI phổ biến là Calico Overlay, Cilium Overlay, Cilium VPC Native Routing. Trong đó:

* **Calico Overlay:** Phù hợp cho các môi trường cần **hiệu suất cao** và khả năng tương thích với nhiều hạ tầng.
* **Cilium Overlay**: Tối ưu cho các ứng dụng cần **bảo mật mạnh mẽ,** giúp cải thiện hiệu suất, bảo mật, và khả năng mở rộng.
* **Cilium VPC Native Routing:** Lý tưởng cho các môi trường sử dụng **VPC**, tối ưu hóa hiệu suất và quản lý IP trực tiếp từ VPC.

Dưới đây là bảng so sánh chi tiết ba plugin CNI phổ biến được cung cấp trên VKS: **Calico Overlay**, **Cilium Overlay**, và **Cilium VPC Native Routing**.

<table><thead><tr><th width="175">Tiêu chí</th><th>Calico Overlay</th><th>Cilium Overlay</th><th>Cilium VPC Native Routing</th></tr></thead><tbody><tr><td><strong>Mô hình mạng</strong></td><td>Overlay (VXLAN/Ipip tunneling)</td><td>Overlay (VXLAN tunneling)</td><td>Native routing trực tiếp trên VPC (no overlay)</td></tr><tr><td><strong>Công nghệ nền tảng</strong></td><td>Sử dụng IP-in-IP hoặc VXLAN để tạo mạng overlay</td><td>Sử dụng eBPF để tạo mạng overlay</td><td>Sử dụng eBPF và sử dụng routing native của VPC</td></tr><tr><td><strong>Hiệu năng</strong></td><td>Tốt, phù hợp với nhiều workload</td><td>Rất tốt, tối ưu cho workloads yêu cầu hiệu năng cao</td><td>Tốt nhất, tận dụng tối đa hạ tầng VPC</td></tr><tr><td><strong>Bảo mật</strong></td><td>Mạnh mẽ, hỗ trợ policy-based networking chi tiết. </td><td>Tốt, tích hợp sâu với kernel, hỗ trợ eBPF</td><td>Tương đối tốt, dựa trên cấu hình VPC</td></tr><tr><td><strong>Tích hợp với Kubernetes NetworkPolicy</strong></td><td>Có </td><td>Có </td><td>Có</td></tr><tr><td><strong>Quản lý IP</strong></td><td>Quản lý IP động, cấp phát IP từ dải địa chỉ của Calico CIDR</td><td>Quản lý IP động, cấp phát IP từ dải địa chỉ của Cilium CIDR</td><td>Quản lý IP trực tiếp từ dải địa chỉ của VPC</td></tr><tr><td><strong>Khả năng mở rộng</strong></td><td>Hỗ trợ mở rộng tốt, phù hợp với các cụm lớn</td><td>Hỗ trợ mở rộng tốt, nhưng bị giới hạn bởi eBPF map size</td><td>Hỗ trợ mở rộng tốt, tối ưu hóa cho mạng VPC</td></tr></tbody></table>
