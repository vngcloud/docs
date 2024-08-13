# Recovery Point Retention

Trong quá trình sử dụng dịch vụ Disaster Recovery (DR), việc quản lý các Recovery Point (điểm khôi phục) là một yếu tố quan trọng để đảm bảo khả năng phục hồi dữ liệu hiệu quả đồng thời tối ưu hóa chi phí lưu trữ. VNG Cloud Disaster Recovery Center (DRC) cung cấp các tùy chọn linh hoạt để bạn quản lý Retention Recovery Point, giúp bạn cân bằng giữa nhu cầu bảo vệ dữ liệu và ngân sách của mình.

Dưới đây là mô tả chi tiết về các chính sách Retention Recovery Point của DRC, giúp bạn hiểu rõ hơn về cách thức hoạt động và cách lựa chọn phù hợp với nhu cầu của mình.

**Mô tả Retention Recovery Point của DRC**

DRC cung cấp ba loại chính sách Retention Recovery Point: Daily, Weekly và giới hạn tổng số Point được phép lưu trữ.

## Daily

* **Thời gian thực hiện:** 00h00m mỗi ngày (đảm bảo chạy sau job tạo point)
* **Quy tắc lưu trữ:**
  * Khi tạo một Point Daily mới, toàn bộ recovery point & snapshot tương ứng với point đó của ngày hôm trước sẽ được giữ lại.
  * Từ ngày hôm kia trở về trước, chỉ giữ lại các point & snapshot có đánh dấu "contain Daily" (thường là point lúc 0h00m của ngày đó).
* **Ví dụ:** Vào lúc 0h00m ngày 20:
  * Toàn bộ point của ngày 19 sẽ được giữ lại.
  * Từ ngày 18 trở về trước, các point và snapshot sẽ bị xóa, chỉ giữ lại point có đánh dấu "contain Daily" (là point lúc 0h00m ngày 18).

## Weekly

* **Thời gian thực hiện:** 00h00m mỗi ngày Chủ Nhật hàng tuần.
* **Quy tắc lưu trữ:**
  * Khi tạo đến Point Weekly thứ \[n], các point Daily của tuần thứ \[n - 2] sẽ bị xóa, chỉ giữ lại point Weekly thứ \[n - 2] đó.

**Ví dụ:**

* Khi tạo đến point Weekly thứ 3, các point Daily của tuần thứ 1 sẽ bị xóa, chỉ giữ lại point được đánh dấu là "Weekly".

## Total Point

* **Quy tắc lưu trữ:**
  * Hệ thống chỉ cho phép lưu tối đa 63 point.
  * Khi tạo đến point thứ 64, point cũ nhất (xa nhất về thời gian) sẽ bị xóa.

**Tóm tắt:**

* **Daily:** Giữ lại toàn bộ point của ngày hôm trước và các point "contain Daily" của các ngày trước đó.
* **Weekly:** Giữ lại các point "Weekly" và xóa các point "Daily" của tuần cũ hơn 2 tuần.
* **Total Point:** Giới hạn số lượng point tối đa là 63, xóa point cũ nhất khi vượt quá giới hạn.

**Lưu ý:**

* Các quy tắc lưu trữ này giúp tối ưu hóa việc sử dụng không gian lưu trữ đồng thời đảm bảo khả năng phục hồi dữ liệu trong các khoảng thời gian khác nhau.
* Bạn có thể điều chỉnh các tham số (như **Interval Time**) để phù hợp với nhu cầu và chính sách lưu trữ của mình.
