# Team & Permissions

**Team & Permissions** giúp Root và Admin kiểm soát ai được truy cập AgentBase và với quyền gì — thông qua hệ thống role được AgentBase wrap sẵn, dễ gán mà không cần cấu hình IAM policy thủ công.

Truy cập tại: [https://aiplatform.console.vngcloud.vn/team-permissions](https://aiplatform.console.vngcloud.vn/team-permissions)

![Team & Permissions — danh sách thành viên](../../../.gitbook/assets/Agentbase-image/Members-list.png)

---

## Tổng quan

**Team & Permissions** gồm ba tab:

| Tab | Mô tả |
|---|---|
| **Members** | Xem danh sách thành viên trong org; mời thành viên mới bằng cách copy Login URL IDP; gán/đổi role qua icon ⋮ |
| **Roles & Permissions** | Bảng permission matrix read-only — hiểu quyền của từng role trước khi assign |
| **Service Accounts** | Xem SA được tự động tạo khi deploy agent; nhấp vào SA để chuyển sang IAM quản lý credentials |

---

## Roles trong AgentBase

AgentBase wrap sẵn 4 role từ IAM — bạn chỉ cần chọn role phù hợp, không cần cấu hình policy thủ công:

| Role | Mô tả |
|---|---|
| **Root** | Chủ sở hữu org — toàn quyền, bao gồm billing và SA secrets. Mỗi org chỉ có 1 Root. |
| **Admin** | Quản trị viên do Root bổ nhiệm — quản lý members, agents, cấu hình org. Không có quyền billing, quota và model config. |
| **Member** | Thành viên hoạt động — tạo và chạy agent của mình; xem SA của agent do mình tạo |
| **Viewer** | Chỉ đọc — xem agent config, logs và conversation history. Không thực hiện được các thao tác có side-effect. |

---

## Mời thành viên

Thành viên mới đăng nhập vào AgentBase thông qua **Identity Provider (IDP)** đã cấu hình trong IAM — không cần tạo tài khoản riêng. Để mời:

1. Vào tab **Members** → nhấp **Invite Member**
2. Copy **Login URL** của IDP phù hợp
3. Gửi URL đó cho thành viên — họ truy cập link, xác thực qua IDP và tự động được thêm vào org

Sau khi thành viên đăng nhập lần đầu, Root gán role phù hợp qua icon ⋮ trên row của thành viên.

---

## Bắt đầu

| Tôi muốn... | Đi đến |
|---|---|
| Xem, mời, xóa thành viên và gán role | [Quản lý thành viên](quan-ly-thanh-vien.md) |
| Hiểu quyền của từng role | [Phân quyền theo role](phan-quyen-theo-role.md) |
| Xem Service Accounts của agents | [Quản lý Service Accounts](quan-ly-service-accounts.md) |