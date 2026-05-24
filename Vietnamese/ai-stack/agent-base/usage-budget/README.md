# Usage & Budget

**Usage & Budget** giúp bạn theo dõi mức tiêu thụ tài nguyên và kiểm soát ngân sách hàng tháng — tất cả trong một nhóm menu duy nhất trên AgentBase.

---

## Tổng quan

**Usage & Budget** gồm hai trang chính:

| Trang | Mô tả | Quyền truy cập |
|---|---|---|
| **Usage & Cost** | Dashboard xem usage (requests, tokens, active agents) và cost theo agent, provider, model — kèm bộ lọc linh hoạt và dự báo chi phí cuối tháng | Root, Admin, Viewer (full org data); Member (data agent của mình) |
| **Budget & Alerts** | Đặt hạn mức ngân sách tháng (VND) và cấu hình cảnh báo tự động khi chi phí tiếp cận giới hạn | Chỉ Root |

---

## Tính năng chính

### Usage & Cost Dashboard

Dashboard tổng hợp usage và cost toàn org với bộ lọc đa chiều:

- **Global filters:** Agent (bao gồm **Others** — MaaS gọi trực tiếp không qua agent), Provider, Model, API Key, Time Range
- **Tab Usage:** Requests, Tokens, Active Agents; biểu đồ Requests over time; Token Breakdown; bảng **Top Expensive Agent** (top 10 agent tốn chi phí nhất, aggregate per agent)
- **Tab Cost:** Total Cost, Budget Used %, Monthly Projection; Cost by Agent, by Provider, by Model; Monthly Cost Trend

### Budget & Alerts

Root đặt hạn mức ngân sách tháng bằng **VND** (cố định, không có tùy chọn currency khác). Khi chi phí đạt ngưỡng:

- **80%:** Gửi email cảnh báo đến Root + hiển thị banner vàng cố định trên **Tab Usage**
- **100%:** Gửi email cảnh báo + banner đỏ cố định trên **Tab Usage**

Budget tự động áp dụng lại cho tháng tiếp theo (always recurring) — không cần cấu hình lại mỗi tháng.

---

## Bắt đầu

| Tôi muốn... | Đi đến |
|---|---|
| Xem usage, cost và dự báo chi phí cuối tháng | [Xem Usage & Cost](xem-usage-cost) |
| Đặt hạn mức ngân sách và cấu hình cảnh báo | [Cấu hình Budget & Alerts](budget-alert) |
