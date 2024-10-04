# CNI

## **Tổng quan**

**CNI (Container Network Interface)** là một bộ công cụ tiêu chuẩn cung cấp khả năng kết nối mạng cho các container trong một cụm Kubernetes. Nói một cách đơn giản, CNI là một lớp trừu tượng, giúp Kubernetes quản lý và cấu hình mạng cho các pod (một tập hợp các container chia sẻ cùng một mạng) một cách linh hoạt và hiệu quả.

### CNI hoạt động như thế nào?

Khi bạn tạo một pod mới, Kubernetes sẽ gọi đến CNI để tạo một mạng interface cho pod đó. Plugin CNI sẽ thực hiện các tác vụ sau:

* **Cấp phát địa chỉ IP:** Gán một địa chỉ IP duy nhất cho pod.
* **Cấu hình routing:** Thiết lập các quy tắc routing cho phép giao tiếp giữa các pod,...

Bên cạnh đó, các kết nối hoạt động như sau:

* **Kết nối trong cùng một VPC**: Các node trong cùng một VPC sẽ kết nối trực tiếp với nhau.
* **Kết nối giữa các VPC khác nhau**: Sử dụng VPC Peering để kết nối các node giữa các VPC khác nhau.
* **Kết nối tới hạ tầng bên ngoài:** Sử dụng các giải pháp kết nối mạng như VPN site-to-site hoặc Direct Connect để kết nối từ các node trong VPC tới các hạ tầng bên ngoài (On Cloud, On-premise).

Điều này giúp duy trì một hạ tầng mạng liên tục, linh hoạt và bảo mật trong môi trường multi-cloud hoặc hybrid-cloud.

***

## So sánh giữa các plugin CNI

Hiện tại, VKS đang cung cấp 3 plugin CNI phổ biến là Calico Overlay, Cilium Overlay, Cilium VPC Native Routing. Trong đó:

* **Calico Overlay:** Phù hợp cho các môi trường cần **hiệu suất cao** và khả năng tương thích với nhiều hạ tầng.
* **Cilium Overlay**: Tối ưu cho các ứng dụng cần **bảo mật mạnh mẽ,** giúp cải thiện hiệu suất, bảo mật, và khả năng mở rộng.
* **Cilium VPC Native Routing:** Lý tưởng cho các môi trường sử dụng **VPC**, tối ưu hóa hiệu suất và quản lý IP trực tiếp từ VPC.
