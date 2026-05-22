# Cấu hình Budget & Alerts

> Hướng dẫn Root đặt hạn mức ngân sách tháng (VND), theo dõi chi phí đã dùng và cấu hình cảnh báo tự động khi chi phí tiếp cận giới hạn.

---

## Điều kiện cần

- Đã đăng nhập với role **Root** (Budget & Alerts chỉ dành cho Root; Admin và Member không có quyền truy cập)

---

## Bật Budget Limit lần đầu

**Bước 1: Mở Budget & Alerts**

1. Vào **AgentBase** → sidebar → **Usage & Budget** → **Budget & Alerts**

![Budget & Alerts](../../../.gitbook/assets/Agentbase-image/Budget-Alerts.png)

**Bước 2: Nhập hạn mức và lưu**

1. Nhập giá trị vào trường **Monthly Limit**:

| Trường | Ví dụ | Ghi chú |
|---|---|---|
| **Monthly Limit** | `100,000,000` | Nhập số VND |

> Đơn vị cố định là **VND** — không có tùy chọn currency khác.
> Toggle **Enable Budget Unlimited**: khi bật ON, hệ thống bỏ giới hạn và cho phép chi tiêu không giới hạn. Mặc định để OFF để giữ nguyên hạn mức.

2. Nhấn biểu tượng xác nhận (✓) bên cạnh ô nhập để lưu

**Bước 3: Xác nhận đã set**

Sau khi lưu thành công, trang hiển thị:

- **Monthly Limit**: Số VND đã đặt (kèm biểu tượng chỉnh sửa)
- **Used This Month**: Chi phí tháng hiện tại (VND)
- **Budget Usage** section: Thanh progress bar + phần trăm đã dùng + số VND còn lại
- **Budget Alerts** section: 2 toggle cảnh báo được kích hoạt (đều ON mặc định)

---

## Xem trạng thái Budget

Khi budget đã được set, phần **Budget Usage** hiển thị:

| Thành phần | Mô tả |
|---|---|
| **Progress bar** | Thanh liền màu thay đổi theo % tổng: xanh lá (0–69%) / vàng (70–79%) / cam (80–99%) / đỏ (100%+) |
| **Label "X.XM / XXXM"** | Used / Limit hiển thị góc phải section title |
| **Legend MaaS** | MaaS — Model API calls · X,XXX,XXX VND · X% |
| **Legend Runtime** | Runtime — Agent compute · X,XXX,XXX VND · X% |
| **Monthly Projection** | Ước tính chi phí cuối tháng (hiển thị sau khi đã qua ≥ 3 ngày trong tháng) |

---

## Cấu hình Alert Thresholds

**Budget Alerts** section hiển thị hai ngưỡng cố định — cả hai đều ON mặc định khi budget được set:

| Ngưỡng | Hành động khi đạt |
|---|---|
| **Email alert at 80% usage** | Gửi email thông báo đến địa chỉ nhận được cấu hình — Primary root contact will be notified. |
| **Email alert at 100% usage** | Gửi email đến địa chỉ nhận — Agents vẫn tiếp tục chạy, cần xử lý ngay lập tức. |

- **Alert recipient**: Nhập địa chỉ email nhận cảnh báo (có thể chỉnh sửa)
- Mỗi ngưỡng chỉ gửi email **1 lần/tháng** — không spam khi cron chạy lại
- Nhấn **Save Changes** sau khi điều chỉnh toggle hoặc thay đổi địa chỉ nhận

{% hint style="warning" %}
Budget Alert chỉ **cảnh báo** — không tự động dừng agent hay block request khi vượt ngưỡng. Nếu muốn giảm chi phí ngay lập tức, cần thủ công stop Runtime.
{% endhint %}

---

## Chỉnh sửa Budget Limit giữa tháng

1. Nhấn icon ✏️ trên KPI card **MONTHLY LIMIT**
2. Nhập giá trị mới → nhấn **Save**

**Trường hợp tăng limit:**
- `used%` được tính lại ngay theo limit mới
- Tất cả alert flags reset — ngưỡng 80% và 100% tính theo limit mới

**Trường hợp giảm limit xuống dưới chi phí đã dùng:**

{% hint style="warning" %}
Nếu limit mới thấp hơn chi phí đã dùng trong tháng, hệ thống hiển thị dialog cảnh báo:
> "Limit mới thấp hơn chi phí đã dùng (X VND). Org sẽ ngay lập tức ở trạng thái vượt budget. Bạn có chắc?"

Nhấn **Confirm** để lưu — hệ thống gửi email alert 100% ngay lập tức (không chờ cron), progress bar chuyển đỏ.
{% endhint %}

---

## Bỏ giới hạn Budget

1. Bật toggle **Enable Budget Unlimited**
2. Xác nhận dialog: "Bật Budget Unlimited — chi phí sẽ không có giới hạn tháng. Tiếp tục?"
3. Nhấn **Confirm**

Sau khi bật:
- Hạn mức Monthly Limit bị vô hiệu hóa
- Budget Alerts section chuyển sang disabled (greyed-out)
- Banner cảnh báo trên Tab Usage của Usage & Cost tự ẩn

---

## Budget reset đầu tháng mới

Vào 00:00 ngày 1 mỗi tháng, hệ thống tự động:
- Reset **Used this month** về 0
- Áp dụng cùng budget limit cho tháng mới (always recurring)
- Reset alert flags (80% và 100% có thể trigger lại trong tháng mới)

---

## Kết quả

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Xem chi tiết chi phí theo agent/provider/model | [Xem Usage & Cost](xem-usage-cost.md) |
| Tổng quan Usage & Budget | [Usage & Budget](README.md) |
