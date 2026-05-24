# Quản lý Policy Group

> Hướng dẫn này giúp bạn tạo Policy Group, thêm policies định nghĩa quyền truy cập tool, gắn group vào MCP Gateway và xóa group khi không còn cần thiết.

---

## Điều kiện cần

- Có tài khoản GreenNode với role **Root** hoặc **Admin** (Member và Viewer chỉ có quyền xem)
- Đã tạo ít nhất 1 MCP Gateway để gắn Policy Group vào

---

## Tạo Policy Group

**Bước 1: Mở trang Policy Groups**

1. Đăng nhập vào [AI Platform Console](https://aiplatform.console.vngcloud.vn)
2. Chọn **AgentBase** trong menu trái
3. Chọn **MCP Governance** → **Policy Groups**

![Danh sách Policy Groups](../../../../.gitbook/assets/Agentbase-image/Policy-group-list.png)

4. Nhấn **Create Policy Group**

**Bước 2: Điền thông tin cơ bản (Step 1)**

1. Điền **Name** theo quy tắc:
   - Bắt đầu bằng chữ cái (a–z, A–Z)
   - Hợp lệ: chữ cái, số, dấu gạch dưới `_`
   - Tối thiểu 5, tối đa 50 ký tự
   - Duy nhất trong organization

   | Ví dụ name | Hợp lệ? |
   |---|---|
   | `PolicyGroup_Prod01` | ✅ |
   | `sales_agent_policy` | ✅ |
   | `myPolicy` | ✅ |
   | `123invalid` | ❌ — bắt đầu bằng số |
   | `name with space` | ❌ — chứa khoảng trắng |
   | `ab` | ❌ — dưới 5 ký tự |

2. Điền **Description** (tuỳ chọn) — tối đa 4096 ký tự
3. Nhấn **Create Policy Group** → chuyển sang Policy Builder

---

## Thêm Policies (Policy Builder)

Sau khi tạo group, trang Policy Builder mở ra (Step 2). Bạn có thể thêm tối đa **20 policies** mỗi group.

**Bước 3: Thêm một policy mới**

1. Nhấn **+ Add Policy**
2. Điền **Policy name** — tối đa 64 ký tự, duy nhất trong group (ví dụ: `allow-sales-call-tool`)
3. Điền **Policy description** (tuỳ chọn)

**Bước 4: Chọn Effect**

| Lựa chọn | Ý nghĩa |
|---|---|
| **ALLOW** | Cho phép agent thực thi action khi policy match |
| **DENY** | Chặn agent thực thi action khi policy match |

**Bước 5: Chọn Principal**

- **All principals (everyone)** — áp dụng cho mọi agent gọi qua gateway
- **Specific principal** — chỉ áp dụng cho một user/service cụ thể

  Khi chọn **Specific**:

  | Trường | Giá trị | Ghi chú |
  |---|---|---|
  | Type | `iam` hoặc `jwt` | `iam` = IAM identity; `jwt` = JWT token |
  | Identifier | tuỳ chọn | Để trống → match mọi user thuộc type; điền ID → match đúng 1 user |

  Ví dụ:
  - Type `jwt`, identifier `sales-agent-001` → serialize thành `"jwt:sales-agent-001"`
  - Type `iam`, không điền identifier → serialize thành `"iam"` (match tất cả IAM users)
  - Type `jwt`, identifier `*` → `"jwt:*"` (wildcard hợp lệ — match tất cả JWT users)

**Bước 6: Chọn Gateway Scope**

- **All gateways (*)** — policy enforce trên mọi gateway đã gắn group
- **Specific gateway(s)** — chọn subset từ dropdown (chỉ gateways đã attach group)

**Bước 7: Chọn Action**

- **All actions (*)** — áp dụng cho mọi `tools/call`
- **Specific actions** — nhập chính xác theo format `targetName__toolName`

  Ví dụ action patterns hợp lệ:
  ```
  weatherTarget__getForecast
  paymentTarget__chargeCard
  refundTarget__getAmount
  ```

{% hint style="warning" %}
Chỉ hỗ trợ `*` (tất cả) hoặc exact `targetName__toolName`. Các partial wildcard như `paymentTarget__*` hay `*__chargeCard` đều không hợp lệ.
{% endhint %}

**Bước 8: Thêm Conditions (tuỳ chọn)**

1. Bật toggle **Add conditions**
2. Nhấn **+ Add Condition**
3. Chọn **Operator**, nhập **Key** và **Value**
4. Lặp lại để thêm nhiều conditions — tất cả phải đúng (**AND logic**)

---

## Ví dụ Policy thực tế

### Ví dụ 1 — ALLOW tất cả agents gọi mọi tool

```
Policy name:  allow-all
Effect:       ALLOW
Principal:    All principals (everyone)
Gateway:      All gateways (*)
Action:       All actions (*)
Conditions:   (không có)
```

Dùng làm baseline "permit all", kết hợp với DENY policies có điều kiện cụ thể hơn.

---

### Ví dụ 2 — ALLOW chỉ sales agent gọi payment tools

```
Policy name:  allow-sales-payment
Effect:       ALLOW
Principal:    Specific — type: jwt, identifier: sales-agent-service
Gateway:      All gateways (*)
Action:       Specific — paymentTarget__chargeCard, paymentTarget__getBalance
Conditions:   equals · principal.role · sales
```

Serialized principal: `"jwt:sales-agent-service"`

Chỉ agent `sales-agent-service` với role `sales` mới được gọi `chargeCard` và `getBalance`.

---

### Ví dụ 3 — DENY mọi request ngoài giờ hành chính

```
Policy name:  deny-outside-business-hours
Effect:       DENY
Principal:    All principals (everyone)
Gateway:      All gateways (*)
Action:       All actions (*)
Conditions:   lessThan · request.timestamp.hour · 8
```

Kết hợp thêm condition thứ 2 để block cả sau 17 giờ:

```
              greaterThan · request.timestamp.hour · 17
```

Vì multiple conditions kết hợp AND, cần tách thành 2 policies riêng: một policy DENY trước 8h, một policy DENY sau 17h.

---

### Ví dụ 4 — DENY agents từ IP ngoài mạng nội bộ

```
Policy name:  deny-external-ip
Effect:       DENY
Principal:    All principals (everyone)
Gateway:      All gateways (*)
Action:       All actions (*)
Conditions:   notEquals · request.client_ip matches 10.0.0.0/8
```

Hoặc dùng `ipInRange` để allow internal và DENY everything else:

```
Policy name:  allow-internal-only
Effect:       ALLOW
Principal:    All principals (everyone)
Gateway:      All gateways (*)
Action:       All actions (*)
Conditions:   ipInRange · request.client_ip · 10.0.0.0/8
```

---

**Bước 9: Lưu**

Nhấn **Save Changes** → group chuyển sang trạng thái **Active** và mở trang Policy Group Detail.

![Policy Group Detail](../../../../.gitbook/assets/Agentbase-image/policy-group-detail.png)

![Chi tiết Policy trong Group](../../../../.gitbook/assets/Agentbase-image/policy-in-policygroup-detail.png)

---

## Gắn Policy Group vào Gateway

Có 3 cách gắn group vào gateway:

**Cách 1 — Từ Policy Group Detail**

1. Mở Policy Group Detail (nhấn tên group từ danh sách)
2. Chọn tab **Associated Gateways**
3. Nhấn **Associate Gateway**
4. Chọn gateway từ dropdown
5. Nhấn **Confirm**

**Cách 2 — Từ danh sách Policy Groups**

1. Tick checkbox trên row của group
2. Nhấn **Associate Gateway** (nút outline xanh trên toolbar)
3. Chọn gateway và nhấn **Confirm**

**Cách 3 — Từ MCP Gateway Detail**

Xem hướng dẫn tại [Quản lý MCP Gateway](../mcp-gateway/quan-ly-mcp-gateway.md).

{% hint style="warning" %}
Mỗi MCP Gateway chỉ được gắn **một Policy Group** tại một thời điểm. Nếu gateway đã có group cũ, gắn group mới sẽ **thay thế hoàn toàn** group cũ — policies của group cũ ngừng hiệu lực ngay lập tức.
{% endhint %}

---

## Gỡ Gateway khỏi Policy Group

1. Mở Policy Group Detail → tab **Associated Gateways**
2. Tìm gateway cần gỡ → nhấn **Detach**
3. Xác nhận trong dialog

Sau khi detach, gateway không còn policy control — mọi `tools/call` qua gateway sẽ bị từ chối cho đến khi gắn Policy Group mới.

---

## Xóa Policy Group

{% hint style="warning" %}
Xóa Policy Group là **không thể hoàn tác**. Nếu group đang gắn gateway, xóa sẽ tự động gỡ tất cả gắn — gateway mất policy control ngay lập tức.
{% endhint %}

1. Vào trang **Policy Groups**
2. Tick checkbox trên row của group cần xóa
3. Nhấn **Delete** (nút đỏ) → đọc cảnh báo và xác nhận

---

## Kết quả

Sau khi hoàn thành, Policy Group ở trạng thái **Active** và đã gắn vào gateway. Mọi `tools/call` qua gateway sẽ được evaluate theo thứ tự policies từ trên xuống — first-match wins, DENY by default nếu không có rule nào match.

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Hiểu evaluation flow hoạt động chi tiết | [Policy Groups — Tổng quan](README.md) |
| Cấu hình MCP Gateway | [Quản lý MCP Gateway](../mcp-gateway/quan-ly-mcp-gateway.md) |
