# What is VKS?

VKS (VNGCloud Kubernetes Service) là một dịch vụ được quản lý trên VNGCloud giúp bạn đơn giản hóa quá trình triển khai và quản lý các ứng dụng dựa trên container. Kubernetes là một nền tảng mã nguồn mở được phát triển bởi Google, được sử dụng rộng rãi để quản lý và triển khai các ứng dụng container trên môi trường phân tán.

<figure><img src="https://media.licdn.com/dms/image/D4E12AQE2lTRiOJ1m4w/article-inline_image-shrink_1500_2232/0/1657985109690?e=1718841600&#x26;v=beta&#x26;t=Wq4ePWjKyKwxhqRuURZsxeKbtm1CtuLKOJSxLSxhhO0" alt=""><figcaption></figcaption></figure>

### Các thành phần chính:  <a href="#whatisvks-cacthanhphanchinh" id="whatisvks-cacthanhphanchinh"></a>

1. **Control Plane:** chịu trách nhiệm quản lý trạng thái tổng thể của cluster và đưa ra các quyết định về cách triển khai và quản lý các ứng dụng. Control Plane gồm các thành phần sau:
   * **kube-api-server:** Tiếp nhận các yêu cầu API từ người dùng và các thành phần khác trong cụm, xử lý các yêu cầu đó và trả về kết quả.
   * **kube-controller-manager:** Chạy một số bộ điều khiển chịu trách nhiệm thực hiện các tác vụ quản lý cụm, chẳng hạn như đảm bảo rằng số lượng pod mong muốn cho mỗi triển khai đang được duy trì, cân bằng tải lưu lượng truy cập giữa các pod và quản lý các dịch vụ cụm.
   * **kube-scheduler:** Chọn nút phù hợp để chạy các pod mới.
   * **etcd:** Lưu trữ dữ liệu cấu hình cho cụm, bao gồm thông tin về các pod, dịch vụ, nút và các đối tượng Kubernetes khác.
2. **Worker Node:** chạy các pod, là các đơn vị cơ bản của triển khai Kubernetes. Worker node gồm các thành phần sau:
   * **Kubelet:** Giao tiếp với máy chủ điều khiển, quản lý các pod trên nút và thực hiện các lệnh từ máy chủ điều khiển.
   * **Kube-proxy:** Quản lý mạng cho các pod trên nút và đảm bảo rằng chúng có thể giao tiếp với nhau và với thế giới bên ngoài.

***

### Những điểm nổi bật của VKS: <a href="#whatisvks-nhungdiemnoibatcuavks" id="whatisvks-nhungdiemnoibatcuavks"></a>

* **Fully Manage Control:**
  * VKS tự động hóa các tác vụ quản lý Kubernetes phức tạp, cho phép bạn tập trung vào việc phát triển ứng dụng.
  * VKS hỗ trợ 24/7 từ đội ngũ chuyên gia của VNG Cloud.
* **Scalability (Khả năng mở rộng):**
  * VKS tự động mở rộng cụm Kubernetes bằng cách tăng giảm số lượng nodes trong cụm của bạn dựa trên nhu cầu thực tế sử dụng.
* **Security (Bảo mật):**
  * VKS tuân thủ các tiêu chuẩn bảo mật quốc tế.
  * VKS cung cấp các tính năng bảo mật nâng cao để bảo vệ các ứng dụng của bạn.
* **Focus on applications (Tập trung vào ứng dụng):**
  * VKS giúp bạn tăng tốc độ phát triển và triển khai ứng dụng thông qua việc bạn chỉ cần tập trung vào việc phát triển ứng dụng, không phải quản lý cơ sở hạ tầng.

**Ngoài ra, VKS còn có các ưu điểm sau:**

* Dễ sử dụng: VKS cung cấp giao diện đơn giản và dễ sử dụng.
* Chi phí hợp lý: VKS cung cấp mức giá cạnh tranh cho các dịch vụ của mình.
