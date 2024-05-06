# Whitelist

### **Tổng quan**

Tính năng Whitelist IP trên chế độ Private Node Group của VKS cho phép bạn chỉ cho phép các địa chỉ IP cụ thể kết nối đến Cluster của bạn. Điều này giúp tăng cường bảo mật cho các ứng dụng và dữ liệu nhạy cảm bằng cách hạn chế truy cập từ các nguồn không xác định.

**Lợi ích**

* **Tăng cường bảo mật:** Whitelist IP giúp bảo vệ dữ liệu và ứng dụng của bạn khỏi các mối đe dọa tiềm ẩn trên mạng công cộng, chẳng hạn như tấn công mạng và vi phạm dữ liệu.
* **Giảm thiểu rủi ro:** Bằng cách hạn chế truy cập vào các node nhạy cảm, Whitelist IP giúp giảm thiểu rủi ro lây lan vi phạm dữ liệu sang các phần khác của mạng của bạn.
* **Kiểm soát tốt hơn:** Whitelist IP cho phép bạn kiểm soát chặt chẽ quyền truy cập vào các node của mình, đảm bảo chỉ những người dùng và ứng dụng được ủy quyền mới có thể truy cập.

{% hint style="info" %}
**Chú ý:**&#x20;

* Whitelist IP chỉ hoạt động khi tất cả các Node Group trong một Cluster đều sử dụng chế độ Private Node Group. Lúc này, bạn có thể sử dụng tính năng Chỉnh sửa Whitelist theo hướng dẫn bên dưới.
* Nếu Cluster của bạn có bất kỳ Node Group nào ở chế độ Public Node Group, việc thiết lập Whitelist IP sẽ không khả thi.
{% endhint %}

***

### Chỉnh sửa Whitelist

Để sử dụng tính năng Whitelist IP trên chế độ Private Node Group, bạn cần thực hiện các bước sau:

**Bước 1:** Truy cập vào [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Bước 2:** Tại màn hình **Overview**, chọn menu **Kubernetes Cluster.**

**Bước 3:** Chọn biểu tượng <img src="https://docs-admin.vngcloud.vn/download/thumbnails/73762015/image2024-4-16_15-51-55.png?version=1&#x26;modificationDate=1713262579000&#x26;api=v2" alt="" data-size="line">và chọn **Edit Whitelist** hoặc chọn biểu tượng **Edit** khi xem chi tiết một Cluster để thực hiện thêm Whitelist cho Cluster của bạn.

**Bước 4:** Lúc này, màn hình **Edit Whitelist** hiển thị, bạn có thể nhập địa chỉ IP mà bạn muốn cho phép truy cập vào Cluster sau đó chọn **Add**.&#x20;

**Bước 5:** Lặp lại bước 4 nếu bạn muốn thêm nhiều **Whitelist IP** cho Cluster của bạn.

**Bước 6:** Chọn **Save** để lưu thông tin hoặc **Cancel** để hủy bỏ việc lưu các thông số này.
