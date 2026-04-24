# Auto Scaling

Tính năng **Auto Scaling** cho phép Load Balancer tự động điều chỉnh số lượng instance dựa trên lưu lượng truy cập thực tế, giúp tối ưu hóa hiệu suất và chi phí vận hành.

* **Tối ưu hóa hiệu suất:** Đảm bảo Load Balancer luôn có đủ tài nguyên để xử lý lưu lượng, tránh tình trạng quá tải.
* **Tiết kiệm chi phí:** Tự động tăng/giảm số lượng instance theo nhu cầu thực tế, tránh lãng phí tài nguyên khi lưu lượng thấp.
* **Đơn giản hóa quản lý:** Không cần theo dõi và điều chỉnh quy mô thủ công.

**Bật Auto Scaling**

* Auto Scaling chỉ có thể được bật khi khởi tạo Load Balancer và **không thể tắt** sau đó.
* Trong quá trình tạo Load Balancer, chọn tùy chọn **"Enable auto scaling"**.
* Sau khi bật, tính năng **Resize** sẽ bị vô hiệu hóa – bạn không thể thay đổi gói dịch vụ thủ công đối với các Load Balancer đã bật Auto Scaling.

**Chính sách Auto Scaling**

Chính sách dựa trên tỷ lệ kết nối đang hoạt động (active connection) so với giới hạn kết nối tối đa (max connection):

* **Scale out (Mở rộng):** Khi tỷ lệ active connection/max connection đạt **80%** trong 3 phút liên tục, hệ thống tự động thêm 1 instance.
* **Scale in (Thu hẹp):** Khi tỷ lệ giảm xuống dưới **20%** trong 3 phút liên tục, hệ thống tự động xóa 1 instance.
* **Thời gian thực hiện:** Mỗi lần scale mất khoảng 5–10 phút kể từ thời điểm connection vượt ngưỡng, tùy thuộc vào số lượng Listener của Load Balancer.
* **Trạng thái trong quá trình scaling:** Load Balancer chuyển từ trạng thái `Active` sang `Scaling in` hoặc `Scaling out`, và trở lại `Active` sau khi hoàn tất.

**Phân giải CNAME**

Khi bật Auto Scaling, hệ thống tự động tạo tên miền cho cụm Load Balancer theo template:

```
lb_name-{userid}.{region}.vlb.vngcloud.vn
```

Người dùng cần chủ động cập nhật bản ghi CNAME để trỏ tên miền riêng đến tên miền này. Khi số lượng instance thay đổi do scale up/down, hệ thống sẽ tự động cập nhật bản ghi DNS tương ứng.

**Cấu hình Auto Scaling**

1. **Truy cập vào trang chủ Load Balancer tại đây:** [**https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb**](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb)
2. **Tại trang chủ Load Balancer, click chọn Load Balancer cần cấu hình.**
3. **Tại phần thông tin chi tiết Load Balancer, nhấn nút Configure AutoScale.**
4. **Một cửa sổ giao diện sẽ hiện ra với các trường cấu hình sau:**
   * **Min size:** Số lượng instance tối thiểu cho phép. (Min: 1, Max: 15)
   * **Max size:** Số lượng instance tối đa cho phép. (Min: 1, Max: 15)
   * **Availability zones:**&#x20;
     * Chọn các availability zone và subnet tương ứng cho từng zone. Ví dụ: chọn **HCM-1A** với subnet `10.30.0.0/24`.&#x20;
     * Chỉ có thể chọn các subnet chung VPC với Subnet đã chọn ban đầu.&#x20;
     * Khi chọn thêm AZ, bạn cần điều chỉnh Min Size theo phù hợp. VD: 2 AZ thì MinSize=2, 3 AZ thì MinSize=3.
5. **Nhấn nút "Save" tại góc dưới bên phải của cửa sổ để hoàn tất việc cập nhật.**

**Xem lịch sử Scaling**

1. **Truy cập trang chi tiết của Load Balancer.**
2. **Chọn tab "Scale History"** để xem lịch sử các lần scale và số lượng instance hiện tại.
   * **Event type:** Loại hành động – Scale in hoặc Scale out.
   * **Adjustment number:** Số lượng instance thay đổi trong lần scale đó. Ví dụ: Adjustment number là `1` với Event type là `Scale out` nghĩa là hệ thống đã thêm 1 instance vào cụm.
   * **Total number:** Tổng số instance sau khi scale.
   * **Scale at:** Thời điểm hoàn tất quá trình scale.
