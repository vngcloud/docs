# Token Plan

**Token Plan** giúp bạn khoá trước ngân sách AI hàng tháng bằng một gói **prepaid 30 ngày** với hạn mức token/request cố định theo từng model — thay vì trả tiền theo từng token dùng thực tế như PAYG.

---

## Kiến trúc

Token Plan là một gói subscription tách biệt hoàn toàn với API Key PAYG hiện có, truy cập qua **subscription-key** và một endpoint riêng.

```
Portal (Packages / My Token Plans)
   → Billing API (mua, gia hạn)
   → Subscription Service (tạo/quản lý subscription-key, hạn mức gói)
   → MaaS Gateway (áp rate limit + kiểm soát model theo gói)
   → Model Providers
```

- **Portal:** Token Plan nằm trong nhóm **API Key**, cùng cấp với **API Keys**, trên **AI Platform**.
- **Subscription Endpoint:** dùng chung một host `tokenplan.api.greennode.ai`, tách biệt với GreenNode MaaS Endpoint dùng cho API Key PAYG. Có thêm hậu tố `/v1` hay không là tuỳ chuẩn của tool:
  - Tool chuẩn **OpenAI** (Cursor, OpenCode, Codex…): `https://tokenplan.api.greennode.ai/v1`
  - Tool chuẩn **Anthropic** (Claude Code, Claude Desktop): `https://tokenplan.api.greennode.ai` — **không** có `/v1`

---

## Thành phần chính

### Packages
Catalog các gói do Admin/Pricing cấu hình sẵn — mỗi gói gồm tên, các model đi kèm, hạn mức token/request theo từng model, giá, và số subscription-key tối đa. Bạn browse, xem chi tiết, và mua trực tiếp.

### My Token Plans
Danh sách các gói đã mua. Mỗi gói là **1 plan instance độc lập** — mua nhiều gói song song không gộp quota, kể cả khi trùng Plan Type hoặc model. Mỗi gói có trang Plan Detail riêng gồm 2 tab: **Models** (thông tin gọi API — endpoint, model code) và **Subscription keys** (danh sách key trong gói).

### Subscription Key
Key riêng để gọi model trong hạn mức gói, tách biệt hoàn toàn khỏi API Key PAYG — không xuất hiện chung dropdown chọn key ở bất kỳ đâu trong AgentBase. Khi mua gói, hệ thống tự tạo 1 key mặc định (`default-key`); bạn có thể tạo thêm key trong giới hạn số key tối đa của gói — mọi key trong cùng 1 gói **dùng chung** hạn mức token/request của gói, không có quota riêng theo từng key. Subscription-key tự động xuất hiện trên trang [Access Control](../agent-base/access-control/README.md) với nhãn Key Type = `Plan: {tên gói}`, và bị loại khỏi trang [Rate Limit](../agent-base/protect-govern/rate-limit.md).

---

## So sánh PAYG và Token Plan

| Tiêu chí | PAYG | Token Plan |
|---|---|---|
| Cách tính phí | Trả theo token thực dùng | Prepaid cố định 30 ngày |
| Hạn mức | Không giới hạn — trả theo mức dùng | Hạn mức token/request cố định theo từng model, tính riêng cho mỗi model, dùng chung giữa các subscription-key trong gói |
| Key sử dụng | API Key (PAYG) | Subscription-key |
| Endpoint | GreenNode MaaS Endpoint | Subscription Endpoint |
| Dự đoán chi phí | Khó, biến động theo usage | Dễ — biết trước chi phí/tháng |
| Phù hợp với | Usage biến động, thử nghiệm | Usage ổn định hàng ngày (ví dụ: coding assistant) |

---

## Bắt đầu với Token Plan

| Tôi muốn... | Đi đến |
|---|---|
| **Mới hoàn toàn — đi hết một vòng từ mua gói đến chạy được trên tool** | [Hướng dẫn A-Z](huong-dan-a-z.md) |
| Browse & mua gói Token Plan | [Mua gói Token Plan](mua-goi-token-plan.md) |
| Quản lý gói đã mua & subscription-key | [Quản lý Token Plan](quan-ly-token-plan.md) |
| Dùng subscription-key với AI coding tool (Claude Code, Cursor,...) | [Kết nối OpenAI-compatible với GreenNode MaaS](../ai-coding/ket-noi-openai-compatible-voi-maas.md) |
| Xem usage & chi phí tổng | [Usage & Budget](../usage-budget/README.md) |
| Kiểm soát Rate Limit | [Rate Limit](../agent-base/protect-govern/rate-limit.md) |
