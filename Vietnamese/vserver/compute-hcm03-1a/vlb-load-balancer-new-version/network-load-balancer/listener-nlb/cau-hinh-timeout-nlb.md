# Config Idle Timeout

Tổng quan

NLB chỉ nhìn thấy địa chỉ IP nguồn/đích, cổng và protoocol. Nó khôngrequest  hiểu nội dung HTTP/HTTPS nên không xử lý header `Connection: keep-alive`. Do đó, khái niệm "HTTP/ HTTPS Keep-Alive" không được NLB xử lý như ALB. Tuy nhiên, nó vẫn chuyển tiếp các gói TCP/UDP, vì vậy kết nối TCP cơ bản _giữa client và NLB_ và _giữa NLB và backend_ vẫn có thể tồn tại lâu dài nếu cả hai phía duy trì.&#x20;

Các kết nối idle chiếm dụng tài nguyên trên Load Balancer và các máy chủ backend. Do đó, **Idle Timeout** là tính năng giúp giải phóng tài nguyên bằng cách tự động đóng các kết nối TCP đã không có bất kỳ hoạt động nào (gửi/nhận dữ liệu) trong một khoảng thời gian xác định trước.

### **Cơ chế hoạt động**

1. Load Balancer (NLB) thiết lập một bộ đếm thời gian cho mỗi kết nối.
2. Mỗi khi có dữ liệu được truyền qua kết nối, bộ đếm được **thiết lập lại** về 0.
3. Nếu bộ đếm đạt đến giá trị `idle timeout` (ví dụ: 50 giây) mà không có hoạt động nào, NLB sẽ chủ động đóng kết nối đó.

### **Hướng Dẫn Cấu Hình Idle Timeout**

Các bước thực hiện:

**Bước 1:** Truy cập vào trang chủ Load Balancer tại đây: [https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb)

**Bước 2:** Tại trang chủ **Load Balancer**, click chọn **Load Balancer** cần cấu hình.

**Bước 3:** Tại phần thông tin chi tiết **Load Balancer**, chọn tab **Listener**.

**Bước 4:** Nhấn biểu tượng **Edit** tại **Listener** cần cấu hình **Timeout**.

<figure><img src="../../../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

**Bước 5:** Một cửa sổ giao diện sẽ hiện ra, tìm đến phần **Advanced Configuration** ở phía dưới cùng của cửa sổ. Tại phần **Idle Timeout,** người dùng có thể cấu hình timeout cho 3 loại sau:

<table><thead><tr><th width="123.51171875">Loại Timeout</th><th>Ý Nghĩa</th><th>Mặc định</th></tr></thead><tbody><tr><td><strong>Client</strong></td><td>Thời gian chờ kết nối từ <strong>client → Load Balancer</strong> không hoạt động.</td><td><ul><li>Mặc định: 50 giây.</li></ul><ul><li>Giá trị tối thiểu: 1 giây.</li></ul><ul><li>Giá trị tối đa: 3600 giây.</li></ul><p>(Thông thường bạn nên thiết lập ở 30-180 giây)</p></td></tr><tr><td><strong>Member</strong></td><td>Thời gian chờ kết nối từ <strong>Load Balancer → Backend Server</strong> không hoạt động.</td><td><ul><li>Mặc định: 50 giây.</li></ul><ul><li>Giá trị tối thiểu: 1 giây.</li></ul><ul><li>Giá trị tối đa: 3600 giây.</li></ul><p>(Nên thiết lập >= giá trị client timeout do nếu member timeout &#x3C; client timeourt thì backend có thể đóng kết nối trước và lúc đó client sẽ bị lỗi)</p></td></tr><tr><td><strong>Connection</strong></td><td>Thời gian chờ thiết lập <strong>kết nối TCP</strong> với backend (không phải idle).</td><td><ul><li>Mặc định: 5 giây.</li></ul><ul><li>Giá trị tối thiểu: 1 giây.</li></ul><ul><li>Giá trị tối đa: 3600 giây.</li></ul><p>(Bạn không đổi trừ backend của bạn quá chậm)</p></td></tr></tbody></table>

**Bước 6:** Nhấn nút **Save** tại góc dưới bên phải của cửa sổ để hoàn tất việc cập nhật.

<figure><img src="../../../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
