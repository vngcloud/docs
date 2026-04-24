# ACL (Access Control List)

Tính năng **cấu hình ACL (Access Control List)** cho Load Balancer là một phần quan trọng của bảo mật mạng, cho phép bạn kiểm soát chính xác những địa chỉ IP nào được phép hoặc bị chặn truy cập vào hệ thống. Khác với tính năng IP Whitelist trước đây chỉ hỗ trợ danh sách cho phép, ACL cung cấp cả **danh sách chặn (Dropped CIDRs)**, **danh sách cho phép (Allowed CIDRs)** và **hành động mặc định (Default Action)**.

**Cách hoạt động**

* ACL kiểm tra các request theo thứ tự từ trên xuống dưới. Rule đầu tiên khớp sẽ được áp dụng và quá trình kiểm tra dừng lại ngay.
* Nếu địa chỉ IP nguồn nằm trong **Dropped CIDRs**, request bị từ chối ngay lập tức – không kiểm tra thêm bất kỳ rule nào.
* Nếu địa chỉ IP nguồn nằm trong **Allowed CIDRs** (và không bị chặn trước đó), request được chấp nhận và chuyển tiếp đến máy chủ backend.
* Nếu địa chỉ IP nguồn không khớp với bất kỳ rule nào, hệ thống sẽ áp dụng **Default Action** đã được cấu hình.

**Tại sao cần cấu hình ACL cho Load Balancer**

* **Bảo Mật Tăng Cao**: Tính năng này tăng cường bảo mật bằng cách kiểm soát chặt chẽ quyền truy cập từ các địa chỉ IP nguồn không xác định.
* **Phòng Chống Tấn Công**: ACL giúp ngăn chặn các tấn công từ các địa chỉ IP đáng ngờ hoặc không mong muốn thông qua Dropped CIDRs.
* **Quản Lý Quyền Truy Cập Linh Hoạt**: ACL cho phép bạn kết hợp danh sách chặn, danh sách cho phép và hành động mặc định để xây dựng chính sách truy cập phù hợp với từng môi trường.

**Cấu trúc ACL trong hệ thống**

* **Dropped CIDRs (Danh sách chặn)**: Các CIDR trong danh sách này sẽ bị từ chối ngay lập tức với ưu tiên cao nhất. Ví dụ: `192.168.1.100/32, 10.0.0.0/8`.
* **Allowed CIDRs (Danh sách cho phép)**: Chỉ các CIDR trong danh sách này mới được phép truy cập, với điều kiện chúng không bị chặn bởi Dropped CIDRs trước đó. Ví dụ: `203.0.113.0/24, 172.16.1.10/32`.
* **Default Action (Hành động mặc định)**: Áp dụng khi request không khớp với bất kỳ rule nào trong cả hai danh sách trên. Có hai lựa chọn:
  * **Accept if not specified** – Cho phép truy cập (phù hợp với hệ thống công khai).
  * **Drop if not specified** – Từ chối truy cập (khuyến nghị cho môi trường bảo mật cao).

**Hướng dẫn cấu hình**

1. **Truy cập vào trang chủ Load Balancer tại đây:** [**https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb**](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb)
2. **Tại trang chủ Load Balancer, click chọn Load Balancer cần cấu hình.**
3. **Tại phần thông tin chi tiết Load Balancer, chọn tab Listener.**
4. **Nhấn biểu tượng Edit tại Listener cần cấu hình.**
5. **Một cửa sổ giao diện sẽ hiện ra, tìm đến phần Cấu hình nâng cao ở phía dưới cùng của cửa sổ.**
6. **Tại phần Dropped CIDRs, người dùng có thể cấu hình dải IP cần chặn.**
   * Ví dụ: nhập `192.168.1.100/32, 10.0.0.0/8` để chặn các IP thuộc hai dải này.
7. **Tại phần Allowed CIDRs, người dùng có thể cấu hình dải IP được phép truy cập.**
   * Ví dụ: nhập `203.0.113.0/24, 172.16.1.10/32` để chỉ cho phép các IP thuộc hai dải này.
8. **Tại phần Default Action, chọn hành động áp dụng cho các IP không khớp với bất kỳ rule nào.**
   * Chọn **Accept if not specified** nếu muốn cho phép mặc định.
   * Chọn **Drop if not specified** nếu muốn từ chối mặc định (khuyến nghị).
9. **Nhấn nút "Lưu" tại góc dưới bên phải của cửa sổ để hoàn tất việc cập nhật.**
