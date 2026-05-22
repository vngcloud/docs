# Phân quyền theo role

> Bảng permission matrix read-only — giúp Root và Admin hiểu rõ quyền của từng role trước khi gán cho thành viên.

---

## Mở tab Roles & Permissions

Vào [Team & Permissions](https://aiplatform.console.vngcloud.vn/team-permissions) → tab **Roles & Permissions**

![Roles & Permissions](../../../.gitbook/assets/Agentbase-image/Role-permission-tab.png)

---

## Mô tả các Role

| Role | Capabilities chính |
|---|---|
| **Root** | Billing & Quota management · Model Access configuration · Toàn quyền member & agents |
| **Admin** | Invite/Remove thành viên · CRUD tất cả agents · Quản lý API Keys & SA · Xem Usage dashboard |
| **Member** | Tạo agent mới · Sửa agent của mình · Chạy bất kỳ agent · Xem logs & traces |
| **Viewer** | Xem danh sách agents · Xem logs & traces · Xem conversation history · Xem danh sách tools |

---

## Permission Matrix

> ✅ Toàn quyền &nbsp;·&nbsp; 🔸 Chỉ own (tài nguyên của mình) &nbsp;·&nbsp; ✕ Không có quyền

| Nhóm quyền | Permission | Root | Admin | Member | Viewer |
|---|---|:---:|:---:|:---:|:---:|
| **Member / SA Management** | Xem | ✅ | ✅ | ✅ | ✅ |
| | Quản lý (invite, remove, edit) | ✅ | ✅ | 🔸 | 🔸 |
| **Container Registry** | Xem | ✅ | ✅ | ✅ | ✅ |
| | Xóa image, artifact & reset credentials | ✅ | ✅ | ✕ | ✕ |
| **Agent — CRUD** | Xem | ✅ | ✅ | ✅ | ✅ |
| | Tạo & sửa agent, memory, access control | ✅ | ✅ | ✅ | ✕ |
| | Xóa agent, memory, access control | ✅ | ✅ | ✕ | ✕ |
| **Tools & Integrations** | Xem | ✅ | ✅ | ✅ | ✅ |
| | Tạo, sửa, xóa | ✅ | ✅ | ✕ | ✕ |
| **API Keys** | Tạo API key | ✅ | ✅ | ✅ | ✕ |
| | Xem & xóa API key | ✅ | ✅ | ✕ | ✕ |
| **Usage & Budget** | Xem usage & cost | ✅ | ✅ | ✅ | ✅ |
| | Xem & chỉnh sửa budget | ✅ | ✕ | ✕ | ✕ |
| **Rate Limit & Model** | Xem | ✅ | ✅ | ✅ | ✅ |
| | Tạo & chỉnh sửa | ✅ | ✅ | ✕ | ✕ |

**Giải thích 🔸 Chỉ own:**
- **Member / SA Management — Quản lý**: Member và Viewer chỉ có thể đổi password của chính mình

*Admin chỉ có thể gán role trong phạm vi Workspace scope.*

---

## Kết quả

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Gán hoặc đổi role thành viên | [Quản lý thành viên](quan-ly-thanh-vien.md) |
| Xem Service Accounts của agent | [Quản lý Service Accounts](quan-ly-service-accounts.md) |