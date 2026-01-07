# Quản lý nhóm IP

### Tổng quan

Chức năng **IP Groups** cho phép quản trị viên gom nhiều địa chỉ IP hoặc dải CIDR thành các nhóm có thể tái sử dụng.

Các nhóm IP giúp đơn giản hóa việc quản lý bảo mật bằng cách dùng chung một tập IP cho nhiều tính năng WAF khác nhau.

Hiện tại, IP Groups được áp dụng trong:

* **Allow & Deny Rules**
* **Cấu hình Anti-Bot**

Cách tiếp cận này giúp đảm bảo áp dụng chính sách nhất quán và dễ dàng cập nhật nguồn IP tin cậy hoặc IP bị chặn.

***

### Tổng quan danh sách IP Groups

Danh sách IP Groups hiển thị toàn bộ các nhóm IP đã tạo, bao gồm:

* **Name** – Tên nhóm IP
* **Content** – Danh sách IP hoặc dải CIDR
* **Updated at** – Thời điểm cập nhật gần nhất
* **Action** – Các thao tác như Edit hoặc Delete

IP Groups đóng vai trò trung tâm trong việc quản lý IP trên toàn bộ hệ thống WAF.

***

### Các trường hợp sử dụng IP Groups

IP Groups đặc biệt hữu ích trong các trường hợp:

* Chặn các địa chỉ IP hoặc dải IP độc hại đã biết
* Allowlist các mạng tin cậy hoặc hệ thống nội bộ
* Gom nhóm IP đáng ngờ để tinh chỉnh Anti-Bot
* Duy trì tập IP nhất quán cho nhiều rule bảo mật khác nhau

Mọi thay đổi trong IP Group sẽ **tự động áp dụng** cho tất cả các rule đang sử dụng nhóm đó.

***

### Thêm IP Group

Chọn **Add IP Group** để mở hộp thoại cấu hình và tạo nhóm IP mới.

***

### Cấu hình IP Group

#### Name (bắt buộc)

Nhập tên mô tả cho nhóm IP.

Ví dụ:

* `Blocked group`
* `Trusted networks`
* `Suspicious scanners`

***

#### Reference (tùy chọn)

Một URL tham chiếu đến nguồn bên ngoài chứa danh sách IP.

Nếu được cung cấp, hệ thống sẽ lưu URL này làm thông tin tham chiếu cho nhóm IP.

> Lưu ý: Trường này **không tự động cập nhật nội dung IP** và không kèm ví dụ.

***

#### Content

Nhập danh sách địa chỉ IP hoặc dải CIDR, **mỗi dòng một giá trị**.

Định dạng hỗ trợ:

```
192.168.1.10
68.22.141.0/24
103.245.252.19
```

Lưu ý:

* Mỗi IP hoặc CIDR phải nằm trên một dòng riêng
* Hỗ trợ cả IP đơn lẻ và CIDR

***

### Các thao tác khả dụng

#### Edit

Chỉnh sửa tên nhóm, link tham chiếu hoặc nội dung IP/CIDR.

Thay đổi có hiệu lực ngay lập tức và áp dụng cho tất cả rule đang sử dụng nhóm IP.

***

#### Delete

Xóa vĩnh viễn nhóm IP.

Sau khi xóa, cần rà soát lại các rule đang tham chiếu nhóm này để tránh ảnh hưởng đến chính sách truy cập.
