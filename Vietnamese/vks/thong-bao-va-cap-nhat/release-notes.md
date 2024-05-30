# Release notes

## May 30, 2024 <a href="#april_19_2024" id="april_19_2024"></a>

Chúng tôi vô cùng trân trọng thông báo, bản release chính thức (**General Availability**) của dịch vụ VNGCloud Kubernetes Service đã có sẵn. Với bản release chính thức này, ngoài các tính năng mà chúng tôi đã cung cấp trên các bản release trước đó, phiên bản này sẽ mang đến nhiều tính năng và cải tiến mới cho người dùng. Dưới đây là chi tiết về bản cập nhật:

**Tính năng mới:**

* **Re-activate :** VKS cho phép bạn thực hiện yêu cầu hệ thống tự động khởi tạo lại Service Account mặc định khi bạn xóa nhầm hoặc thay đổi thông tin Service Account mặc định đã khởi tạo trước đó. Service Account mặc định là Service Account được hệ thống VKS tự động khởi tạo khi bạn bắt đầu làm việc với VKS, chúng tôi sẽ sử dụng Service Account này để khởi tạo các resource cho Cluster của bạn.
* **Event History**: VKS sẽ thực hiện hiển thị lịch sử các sự kiện xảy ra khi người dùng làm việc với Cluster hoặc từng Node Group. Đây sẽ là một cách giúp bạn có thể giám sát các hoạt động xảy ra với Cluster của bạn, từ đó hạn chế các hoạt động bất thường xảy ra.
* **Volume**: VKS đã tích hợp hiển thị danh sách Volume tại Resource Tab, giúp bạn dễ dàng quản lý các Volume đang được attach vào Cluster của bạn.
* **Load Balancer**: VKS đã tích hợp hiển thị danh sách Load Balancer tại Resource Tab, giúp bạn dễ dàng quản lý các Load Balancer đang được sử dụng cho Cluster của bạn.

**Cải tiến:**

* **Hiệu năng**: VKS đã thực hiện tối ưu hiệu năng khi khởi tạo Cluster. Cụ thể, tại bản Alpha, thời gian từ khi bắt đầu khởi tạo Cluster (với Default Node Group) tới khi Cluster chuyển trạng thái **ACTIVE** vào khoảng 04:00s tới 04:30s. Hiện tại thời gian này đã được chúng tôi tối ưu về <mark style="color:red;">**02:30s tới 03:00s**</mark> tùy thuộc vào từng Cluster và từng thời điểm mà bạn khởi tạo.
* **Manage Image**: VKS sẽ tự động xóa các image không được sử dụng khi disk chạm mức giới hạn sử dụng (tỷ lệ usage/ quota >= 85%).
* **Ngoài ra**, bản GA này được chúng tôi cải thiến một vài vấn đề khác như:&#x20;
  * Thay đổi cách đặt tên **Node Name** giúp bạn dễ dàng sử dụng và quản lý Cluster của bạn. Cụ thể, tên Node Name sẽ có thêm thông tin **Cluster Name**, **Node Group Name**.
  * Xóa **User Builder** trên User's Worker Node.
  * Thay đổi cơ chế **SSH** từ Port 22 qua Port 234.

Nếu bạn gặp bất kỳ vấn đề với bản phát hành chính thức này, vui lòng liên hệ với bộ phận hỗ trợ của VKS để được trợ giúp.

***

## May 03, 2024 <a href="#april_19_2024" id="april_19_2024"></a>

Bản cập nhật mới nhất cho VKS đã có sẵn, mang đến nhiều tính năng và cải tiến mới cho người dùng. Dưới đây là chi tiết về bản cập nhật:

**Tính năng mới:**

* **Hỗ trợ tính năng Whitelist:** VKS cho phép tạo Private Node Group với chỉ Private IP đồng thời cho phép IP nào kết nối tới Cluster thông qua tính năng Whitelist IP. Chi tiết tham khảo thêm tại [Whitelist](../clusters/whitelist.md).

**Cải tiến:**

* **Tối ưu hóa hệ thống:** Giúp hệ thống hoạt động trơn tru và hiệu quả hơn.
* **Sửa lỗi:** Khắc phục một số lỗi nhỏ để mang đến trải nghiệm người dùng tốt hơn.

Nếu bạn gặp bất kỳ vấn đề nào sau khi cập nhật, vui lòng liên hệ với bộ phận hỗ trợ của VKS để được trợ giúp.

***

## April 17, 2024 <a href="#april_19_2024" id="april_19_2024"></a>

**Chúng tôi vô cùng hân hạnh giới thiệu bản cập nhật mới cho dịch vụ VKS, mang đến cho bạn trải nghiệm quản lý Kubernetes mạnh mẽ và hiệu quả hơn bao giờ hết!**

**Điểm nổi bật:**

* **Quản lý Control Plane hoàn toàn tự động (Fully Managed control plane):** VKS sẽ giải phóng bạn khỏi gánh nặng quản lý Control Plane của Kubernetes, giúp bạn tập trung vào việc phát triển ứng dụng.
* **Hỗ trợ các phiên bản Kubernetes mới nhất:** VKS luôn cập nhật những phiên bản Kubernetes mới nhất (minor version từ 1.27, 1.28, 1.29) để đảm bảo bạn luôn tận dụng được những tính năng tiên tiến nhất.
* **Kubernetes Networking:** VKS tích hợp Calico CNI, mang lại tính hiệu quả và bảo mật cao.
* **Upgrade seamlessly:** VKS hỗ trợ nâng cấp giữa các phiên bản Kubernetes một cách dễ dàng và nhanh chóng, giúp bạn luôn cập nhật những cải tiến mới nhất.
* **Scaling & Healing Automatically:** VKS tự động mở rộng Node group khi cần thiết và tự động sửa lỗi khi node gặp vấn đề, giúp bạn tiết kiệm thời gian và công sức quản lý.
* **Giảm chi phí và nâng cao độ tin cậy:** VKS triển khai Control Plane của Kubernetes ở chế độ sẵn sàng cao và hoàn toàn miễn phí, giúp bạn tiết kiệm chi phí và nâng cao độ tin cậy cho hệ thống.
* **Tích hợp Blockstore Native (Container Storage Interface - CSI):** VKS cho phép bạn quản lý Blockstore thông qua YAML của Kubernetes, cung cấp lưu trữ bền vững cho container và hỗ trợ các tính năng quan trọng như thay đổi kích thước, thay đổi IOPS và snapshot volume.
* **Tích hợp Load Balancer (Network Load Balancer, Application Load Balancer) thông qua các driver được tích hợp sẵn như VNGCloud Controller Mananger, VNGCloud Ingress Controller:** VKS cung cấp khả năng quản lý NLB/ALB thông qua YAML của Kubernetes, giúp bạn dễ dàng expose Service trong Kubernetes ra bên ngoài.
* **Nâng cao bảo mật:** VKS cho phép bạn tạo Private Node Group với chỉ Private IP và kiểm soát quyền truy cập vào cluster thông qua tính năng Whitelist IP, đảm bảo an toàn cho hệ thống của bạn.

**Với những tính năng đột phá này, VKS hứa hẹn sẽ mang đến cho bạn trải nghiệm quản lý Kubernetes hoàn toàn mới, giúp bạn tối ưu hóa hiệu quả và tiết kiệm chi phí!**

**Hãy liên hệ với chúng tôi để được tư vấn và hỗ trợ thêm!**
