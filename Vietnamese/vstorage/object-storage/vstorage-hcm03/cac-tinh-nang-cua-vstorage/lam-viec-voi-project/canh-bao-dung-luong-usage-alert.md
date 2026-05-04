# Cảnh báo dung lượng (Usage alert)

### Tổng Quan

Tính năng Cảnh báo dung lượng lưu trữ (Usage alert) trên vStorage cho phép bạn thiết lập cảnh báo qua email khi dung lượng lưu trữ đạt đến ngưỡng. Mặc định, project khi được tạo đã được thiết lập ngưỡng cảnh báo ở mức 90% quota. Hướng dẫn này sẽ cung cấp chi tiết cách thức cấu hình và quản lý tính năng này thông qua vStorage Portal.

***

### Các bước thực hiện

**Bước 1:** Đăng nhập vào vStorage Portal tại [đây](https://vstorage.console.vngcloud.vn/overview).

**Bước 2**: Tại project cần thiết lập Cảnh báo dung lượng, chọn biểu tượng <img src="../../../../../.gitbook/assets/image (398).png" alt="" data-size="line"> sau đó chọn mục **Cảnh báo dung lượng** và tiếp tục chọn **Cấu hình** **Cảnh báo dung lượng**.

**Bước 3**: Tại màn hình cấu hình **Cảnh báo dung lượng**, thực hiện thiết lập các thông số cần thiết. Cụ thể:

* Thiết lập **Đơn vị quota:** bạn có thể chọn 1 trong hai loại đơn vị bao gồm **GB** hoặc **Phần trăm**.
* Thiết lập **Ngưỡng quota** hoặc **Hạn mức còn lại:** Nếu bạn chọn **Đơn vị quota** là **Phần trăm**, tại đây bạn sẽ nhập phần trăm ngưỡng sử dụng mà khi đạt tới thì hệ thống sẽ kích hoạt cảnh báo. Nếu bạn chọn **Đơn vị quota** là **GB**, tại đây bạn sẽ nhập lượng quota còn lại mà khi đạt tới hệ thống cũng sẽ kích hoạt cảnh báo.

**Bước 4:** Bật tính năng **Cảnh báo dung lượng** tại biểu tượng <img src="../../../../../.gitbook/assets/image (402).png" alt="" data-size="line">. Khi biểu tượng này trở thành <img src="../../../../../.gitbook/assets/image (403).png" alt="" data-size="line">tức là bạn đã bật **Cảnh báo dung lượng** thành công.

**Bước 5**: Ngoài ra, bạn có thể nhấn vào mục **Quản lý người nhận thông báo** để thiết lập thêm danh sách người cùng nhận email cảnh báo.

{% hint style="info" %}
**Chú ý:**

* **Hệ thống vStorage** sẽ thực hiện kiểm tra project có/ không đủ điều kiện được cảnh báo dung lượng theo chu kỳ mỗi **2 lần/ngày** để tự động tăng dung lượng dựa trên ngưỡng đã thiết lập. Email cảnh báo sẽ được gởi tối đa 3 lần liên tiếp.
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/Screenshot from 2026-05-04 15-22-14.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/Screenshot from 2026-05-04 15-22-25.png" alt=""><figcaption></figcaption></figure>
