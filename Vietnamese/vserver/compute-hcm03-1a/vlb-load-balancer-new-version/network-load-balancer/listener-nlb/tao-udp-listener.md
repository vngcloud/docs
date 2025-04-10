# Tạo UDP Listener

Sử dụng hướng dẫn này để thêm mới một UDP Listener vào một Network Load Balancer có sẵn.

**Cách thêm mới UDP Listener**

1. **Truy cập vào trang chủ Load Balancer tại đây:** [**https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb**](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb)
2. **Tại trang chủ Load Balancer, click chọn Load Balancer cần thêm mới Listener.**
3. **Tại phần thông tin chi tiết Load Balancer, chọn tab Listener.**
4. **Nhấn chọn nút "Thêm mới Listener", một cửa sổ giao diện hiện lên cho phép bạn cấu hình thông tin Listener**
5. **Tại cửa sổ thêm mới, cấu hình các thông tin như:**
   * **Tên Listener:** Lưu ý rằng tên Listener không thể thay đổi sau khi khởi tạo
   * **Chọn Giao thức UDP và Port** (mặc định hiển thị Port 53 và tăng dần nếu các Port nhỏ hơn đã được sử dụng)
   * **Cấu hình Pool mặc định và hành động:** Trong trường các request đến Load Balancer mà không phù hợp với bất kỳ pool cụ thể nào, NLB sẽ chuyển hướng lưu lượng đó đến pool mặc định.&#x20;
   * **Cấu hình nâng cao:** Tham khảo thêm các hướng dẫn cấu hình nâng cao theo tính năng như bên dưới
     * [Config timeout](../../application-load-balancer/listener/config-timeout.md)
     * [Config IP whitelist to load balancer](../../application-load-balancer/listener/config-ip-whitelist-to-load-balancer.md)

{% hint style="info" %}
**Lưu ý**

Lưu ý rằng bạn chỉ có thể chọn Pool với giao thức UDP để chỉ định làm Pool mặc định cho UDP Listener
{% endhint %}

