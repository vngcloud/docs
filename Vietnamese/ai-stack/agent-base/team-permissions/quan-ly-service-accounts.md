# Quản lý Service Accounts

> Service Accounts (SA) được tự động tạo khi deploy agent — tab này giúp Root và Admin xem danh sách SA đang hoạt động và chuyển sang IAM để quản lý credentials.

---

## Điều kiện cần

- Đã đăng nhập với role **Root** hoặc **Admin**

---

## Mở tab Service Accounts

Vào [Team & Permissions](https://aiplatform.console.vngcloud.vn/team-permissions) → tab **Service Accounts**

Danh sách hiển thị:

| Cột | Mô tả |
|---|---|
| **SA Name** | Tên SA theo convention `auto-sa-{agent-slug}` |
| **Client ID** | Prefix 8 ký tự + `***` (masked) |
| **Type** | "Auto-generated" — SA chỉ do hệ thống tạo khi deploy agent |
| **Associated Agent** | Tên agent liên kết; hiển thị "—" nếu agent đã bị xóa |
| **Created By** | Thành viên đã deploy agent |
| **Created Date** | Ngày tạo |
| **Status** | Active / Revoked |

---

## Xem và quản lý credentials trong IAM

Nhấp vào bất kỳ SA nào trong danh sách → hệ thống chuyển bạn sang **IAM** để xem Client Secret, revoke credentials và thực hiện các thao tác quản lý đầy đủ.

{% hint style="warning" %}
Client Secret chỉ hiển thị một lần duy nhất ngay sau khi agent được deploy. Sau đó, chỉ Root mới có thể xem lại thông qua IAM — mỗi lần xem được ghi vào Audit Log.
{% endhint %}

---

## SA Orphaned — agent đã bị xóa

Khi agent liên kết bị xóa, SA tương ứng hiển thị badge **Orphaned** trong cột **Associated Agent**. Nên chuyển sang IAM để revoke SA này nhằm tránh credentials không kiểm soát tồn tại trong hệ thống.

---

## Kết quả

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Quản lý thành viên và gán role | [Quản lý thành viên](quan-ly-thanh-vien.md) |
| Xem quyền của từng role | [Phân quyền theo role](phan-quyen-theo-role.md) |