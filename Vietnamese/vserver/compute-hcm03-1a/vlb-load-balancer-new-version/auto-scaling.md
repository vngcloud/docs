# Auto Scaling

Tính năng Auto Scaling cho phép vLB tự động điều chỉnh số lượng Slave dựa trên lưu lượng truy cập, giúp tối ưu hóa hiệu suất và chi phí.

**Bật Auto Scaling**

* Auto Scaling chỉ có thể được bật khi khởi tạo vLB và không thể tắt sau đó.
* Trong quá trình tạo vLB, chọn tùy chọn "Bật auto scaling" (Enable auto scaling).

**Chính sách Auto Scaling**

* Chính sách dựa trên tỷ lệ phần trăm kết nối đang hoạt động (active connection) so với giới hạn kết nối tối đa (max connection).
* **Scaling out (Mở rộng):**
  * Khi đạt ngưỡng 80% active connection/max connection trong 3 phút liên tục, hệ thống sẽ tự động thêm 1 LB role Slave.
* **Scaling in (Thu hẹp):**
  * Khi ngưỡng giảm xuống dưới 20% active connection/max connection trong 3 phút liên tục, hệ thống sẽ tự động xóa 1 LB role Slave.

**Lưu ý quan trọng**

* **Tính năng Resize bị vô hiệu hóa:** Đối với các vLB đã bật Auto Scaling, bạn không thể thay đổi gói dịch vụ (resize) thủ công.
* **Trạng thái Scaling:** Trong quá trình mở rộng hoặc thu hẹp quy mô LB, trạng thái của LB sẽ chuyển từ "Active" sang "Scaling in/Scaling out". Sau khi hoàn tất, trạng thái sẽ trở lại "Active".
* **Thời gian Scaling:** Thời gian để scale lên hoặc xuống 1 LB role Slave là khoảng 2-8 phút, tùy thuộc vào số lượng listener của LB đó.

**Xem lịch sử Scaling**

* Truy cập trang chi tiết của LB .
* Chọn tab "Scale History" để xem lịch sử các lần mở rộng/thu hẹp quy mô và số lượng LB Slave hiện tại. Giải thích ý nghĩa các trường thông tin như sau
  * Event type: Hành động Scale in hoặc Scale out
  * Adjustment number: Số lượng LB trước khi scale
  * Total number: Số lượng LB sau khi scale
  * Scale at: Thời gian hoàn tất quá trình scale.

**Tóm tắt**

Auto Scaling giúp bạn:

* **Tối ưu hóa hiệu suất:** Đảm bảo vLB luôn có đủ tài nguyên để xử lý lưu lượng truy cập, tránh tình trạng quá tải.
* **Tiết kiệm chi phí:** Tự động giảm số lượng Slave khi lưu lượng thấp, giúp bạn tiết kiệm chi phí.
* **Đơn giản hóa quản lý:** Không cần phải theo dõi và điều chỉnh quy mô vLB thủ công.
