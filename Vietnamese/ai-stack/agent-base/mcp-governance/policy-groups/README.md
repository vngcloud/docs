# Policy Groups

Policy Groups giúp bạn kiểm soát chính xác agent nào được gọi tool nào qua MCP Gateway — không cần sửa code agent, áp dụng ngay khi gắn vào Gateway.

---

## Kiến trúc

Mỗi Policy Group là một tập hợp **Policy rules** được đánh giá theo thứ tự từ trên xuống khi một agent gửi `tools/call` qua MCP Gateway. Rule đầu tiên khớp sẽ quyết định kết quả (ALLOW hoặc DENY). Nếu không có rule nào khớp, hệ thống mặc định **từ chối (DENY by default)**.

![Policy Group — Evaluation Flow](../../../../.gitbook/assets/Agentbase-image/policy_group_flow.png)

---

## Thành phần chính

### Policy Group Status

Policy Group chỉ có một trạng thái: **Active** — group tồn tại và sẵn sàng được gắn vào Gateway.

Mỗi **Policy** (rule) bên trong group có trạng thái riêng:

| Trạng thái Policy | Ý nghĩa |
|---|---|
| **Active** | Policy được đánh giá khi có `tools/call` qua gateway |
| **Inactive** | Policy bị tạm vô hiệu hóa, bỏ qua trong quá trình đánh giá |

### Policy Rule

Mỗi Policy trong group gồm 5 thành phần:

| Thành phần | Mô tả |
|---|---|
| **Effect** | `ALLOW` — cho phép agent thực thi. `DENY` — chặn agent. |
| **Principal** | Đối tượng bị áp dụng — `All` (mọi agent) hoặc một user/service account cụ thể. |
| **Gateway Scope** | Policy enforce trên tất cả gateway hay chỉ một subset gateway đã gắn group. |
| **Action Pattern** | Tool call nào bị evaluate — `*` (all) hoặc exact format `targetName__toolName`. |
| **Conditions** | Điều kiện bổ sung theo context: `[Operator] [Key] [Value]`, kết hợp AND. |

---

## Action Patterns

Action pattern xác định tool call nào được áp dụng rule. Format bắt buộc: `targetName__toolName` (hai dấu gạch dưới).

| Pattern | Hợp lệ? | Ý nghĩa |
|---|---|---|
| `*` | ✅ | Tất cả tool calls |
| `weatherTarget__getForecast` | ✅ | Chỉ tool `getForecast` trên target `weatherTarget` |
| `paymentTarget__chargeCard` | ✅ | Chỉ tool `chargeCard` trên target `paymentTarget` |
| `refundTarget__getAmount` | ✅ | Chỉ tool `getAmount` trên target `refundTarget` |
| `*__chargeCard` | ❌ | Partial wildcard — không hợp lệ |
| `paymentTarget__*` | ❌ | Partial wildcard — không hợp lệ |
| `pay*__chargeCard` | ❌ | Partial wildcard — không hợp lệ |

{% hint style="warning" %}
Partial wildcard **không được hỗ trợ**. Chỉ chấp nhận `*` (tất cả actions) hoặc exact `targetName__toolName`.
{% endhint %}

---

## Principal và Wildcard Rules

Khi chọn **Specific principal**, bạn chỉ định `principalType` (`iam` hoặc `jwt`) và tùy chọn `principalIdentifier`:

| Cấu hình | Serialize | Ý nghĩa |
|---|---|---|
| Type `iam`, không có identifier | `"iam"` | Match mọi IAM identity |
| Type `iam`, identifier `user-abc123` | `"iam:user-abc123"` | Match đúng 1 IAM user |
| Type `jwt`, không có identifier | `"jwt"` | Match mọi JWT user |
| Type `jwt`, identifier `user-abc123` | `"jwt:user-abc123"` | Match đúng 1 JWT user |
| Type `jwt`, identifier `*` | `"jwt:*"` | ✅ Wildcard hợp lệ — match tất cả JWT users |
| Type `jwt`, identifier `abc*` | `"jwt:abc*"` | ⚠️ LITERAL — chỉ match user có ID chính xác là `"abc*"` |

{% hint style="warning" %}
`jwt:abc*` **không phải prefix match**. Đây là literal identifier — chỉ match user có ID chính xác là `"abc*"`. Dùng `jwt:*` nếu muốn match tất cả JWT users.
{% endhint %}

---

## Conditions

Conditions cho phép bạn giới hạn policy theo thông tin từ request context (email, role, IP, thời gian...). Mỗi condition có cấu trúc **Operator · Key · Value**. Nhiều conditions kết hợp bằng **AND** — tất cả phải đúng thì policy mới match.

**Ví dụ conditions:**

| Operator | Key | Value | Ý nghĩa |
|---|---|---|---|
| `equals` | `principal.role` | `Admin` | Chỉ apply khi principal có role Admin |
| `greaterThan` | `request.timestamp.hour` | `9` | Chỉ apply sau 9 giờ sáng |
| `lessThan` | `request.timestamp.hour` | `17` | Chỉ apply trước 17 giờ |
| `ipInRange` | `request.client_ip` | `10.0.0.0/8` | Chỉ apply từ dải IP nội bộ |
| `contains` | `principal.email` | `@vng.com.vn` | Chỉ apply cho email VNG |
| `in` | `principal.role` | `Admin,Editor` | Chỉ apply khi role là Admin hoặc Editor |

**Operators hỗ trợ:**

| Nhóm | Operators |
|---|---|
| Equality | `equals`, `notEquals` |
| Comparison | `lessThan`, `lessThanOrEqual`, `greaterThan`, `greaterThanOrEqual` |
| String/Pattern | `like`, `contains`, `containsAll`, `containsAny`, `startsWith`, `endsWith` |
| Membership | `in`, `has`, `hasTag`, `is`, `memberOf` |
| Network/IP | `ipInRange`, `isIpv4`, `isIpv6`, `isLoopback`, `isMulticast` |

---

## Quan hệ Gateway và Policy Group

Một Policy Group có thể gắn vào **nhiều Gateway**, nhưng mỗi Gateway chỉ được gắn với **một Policy Group** tại một thời điểm.

```
Policy Group A  ──►  MCP Gateway 1
                ──►  MCP Gateway 2
                ──►  MCP Gateway 3

Policy Group B  ──►  MCP Gateway 4
```

---

## Bắt đầu với Policy Groups

| Tôi muốn... | Đi đến |
|---|---|
| Tạo Policy Group và thêm policies | [Quản lý Policy Group](quan-ly-policy-group.md) |
| Hiểu MCP Gateway hoạt động như thế nào | [MCP Gateway](../mcp-gateway/README.md) |
| Cấu hình MCP Governance tổng quan | [MCP Governance](../README.md) |
