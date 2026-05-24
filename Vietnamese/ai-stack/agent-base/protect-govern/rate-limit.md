# Rate Limit

> Giới hạn số Request và Token theo chu kỳ thời gian, giúp bảo vệ hệ thống khỏi quá tải và kiểm soát chi phí.

---

## Tổng quan

Rate Limit cho phép bạn đặt ngưỡng tối đa theo hai chiều:

| Chiều giới hạn | Mô tả |
|---|---|
| **Requests** | Số lần gọi API tối đa trong một chu kỳ |
| **Tokens** | Tổng số token (input + output) tối đa trong một chu kỳ |

Mỗi Rate Limit được áp dụng độc lập cho **từng API Key** và **từng Model** được chỉ định:

- Nếu gắn Rate Limit với API Key `key-01` → `key-01` bị giới hạn 50 req/ngày (tính tổng qua tất cả Model)
- Nếu gắn Rate Limit với Model `gpt-5` → `gpt-5` bị giới hạn 50 req/ngày (tính tổng qua tất cả API Key)
- Hai giới hạn trên hoạt động song song, không phụ thuộc vào nhau

{% hint style="info" %}
Tính năng giới hạn "API Key X chỉ được dùng Model Y" sẽ ra mắt trong thời gian tới.
{% endhint %}

---

## Điều kiện cần

- Tài khoản GreenNode với vai trò Root hoặc Admin
- Ít nhất một API Key đã tạo (xem [Access Control](../access-control/README.md))
- Ít nhất một Model đã bật trong [GreenNode MaaS](https://maas.console.vngcloud.vn)

---

## Xem danh sách Rate Limit

Mở [Protect & Govern → Rate Limit](https://aiplatform.console.vngcloud.vn/protect-govern/rate-limit).

![Danh sách Rate Limit](../../../.gitbook/assets/Agentbase-image/rate-limit-list.png)

Mỗi Rate Limit hiển thị:

| Cột | Mô tả |
|---|---|
| **Name** | Tên Rate Limit |
| **Status** | Trạng thái (`ACTIVE`) |
| **Rate limit** | Ngưỡng req/ngày và token/ngày |
| **Associated models** | Các Model được áp dụng giới hạn |
| **Associated API Keys** | Các API Key được áp dụng giới hạn |
| **Action** | Menu ⋮ để chỉnh sửa hoặc xóa |

---

## Tạo Rate Limit

**Bước 1:** Nhấn **Create a rate limit**.

**Bước 2:** Điền thông tin trong popup:

![Tạo Rate Limit](../../../.gitbook/assets/Agentbase-image/Create-rate-limit.png)

| Trường | Giá trị ví dụ | Ghi chú |
|---|---|---|
| **Rate limit name** | `rate-limit-01` | Chữ thường a-z, 0-9, dấu `-`; 5–100 ký tự |
| **Limit by** | Requests và/hoặc Tokens | Chọn một hoặc cả hai |
| **Request limit** | `50` Requests / 1 Day | Áp dụng riêng cho từng API Key và từng Model |
| **Token limit** | `1000000` Tokens / 1 Day | Áp dụng riêng cho từng API Key và từng Model |
| **API Keys** | `mee-agent` | Các API Key sẽ bị giới hạn bởi Rate Limit này |
| **Models** | `ChatGPT 4o, gpt-5` | Các Model sẽ bị giới hạn bởi Rate Limit này |

{% hint style="info" %}
Khi bật cả **Requests** và **Tokens**, hệ thống từ chối request khi **một trong hai** ngưỡng bị vượt — tùy theo điều kiện nào xảy ra trước.
{% endhint %}

**Bước 3:** Nhấn **Create**.

Rate Limit xuất hiện trong danh sách với trạng thái **ACTIVE**.

---

## Chỉnh sửa Rate Limit

1. Trong danh sách, tìm Rate Limit cần chỉnh sửa → nhấn icon **⋮** ở cột Action
2. Chọn **Edit configuration**
3. Cập nhật các trường cần thay đổi (ngưỡng, chu kỳ, API Key, Model) → nhấn **Save**

Thay đổi có hiệu lực ngay lập tức cho chu kỳ hiện tại.

---

## Xóa Rate Limit

1. Trong danh sách, tìm Rate Limit cần xóa → nhấn icon **⋮** ở cột Action
2. Chọn **Delete** → xác nhận

{% hint style="warning" %}
Xóa Rate Limit sẽ gỡ bỏ giới hạn ngay lập tức. Các API Key và Model liên kết sẽ không còn bị kiểm tra ngưỡng.
{% endhint %}

---

## Kết quả

Sau khi tạo, mọi request từ API Key hoặc Model được chỉ định đều bị kiểm tra ngưỡng theo chu kỳ. Khi vượt ngưỡng, request nhận mã lỗi `429 Too Many Requests`.

| Tôi muốn tiếp theo... | Đến |
|---|---|
| Xem chi phí và lượng dùng | [Usage & Budget](../usage-budget/) |
| Quản lý API Key | [Access Control](../access-control/README.md) |