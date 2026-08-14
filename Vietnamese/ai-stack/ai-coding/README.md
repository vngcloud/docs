# AI Coding

AI Coding cho phép kết nối các AI coding tool phổ biến — Claude Code, OpenAI SDK, IDE extension — trực tiếp với model do GreenNode vận hành, dùng model cloud mà không cần tự quản lý key từ các provider ngoài.

---

## Kiến trúc

Request từ tool của bạn được redirect sang endpoint GreenNode. Endpoint expose hai protocol song song để tương thích với mọi client hiện có:

<figure><img src="../../.gitbook/assets/Agentbase-image/ai_coding_flow.png" alt=""><figcaption><p>Hai chuẩn API cùng kết nối tới một endpoint, dùng chung Model Pool</p></figcaption></figure>

Một key dùng được cho cả hai protocol — nhưng **key phải khớp host của loại dịch vụ đã phát hành key đó**.

---

## Hai loại dịch vụ — chọn đúng trước khi cấu hình

| Loại dịch vụ | Cách tính phí | Key dùng để gọi | Host của Base URL |
|---|---|---|---|
| **PAYG** | Trả theo token thực dùng | API Key từ **API Keys** | `maas-llm-aiplatform-hcm.api.vngcloud.vn` |
| **Token Plan** | Gói prepaid 30 ngày, hạn mức token cố định | subscription-key từ Plan Detail → tab **Subscription keys** | `tokenplan.api.greennode.ai` |

---

## Base URL theo loại dịch vụ và chuẩn của client

| Loại dịch vụ | Client chuẩn **Anthropic**<br>(Claude Code, Anthropic SDK) | Client chuẩn **OpenAI**<br>(OpenAI SDK, LiteLLM, Cursor, Continue.dev, Codex, OpenCode) |
|---|---|---|
| **PAYG** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| **Token Plan** | `https://tokenplan.api.greennode.ai` | `https://tokenplan.api.greennode.ai/v1` |

{% hint style="warning" %}
Sai ô trong bảng này là nguyên nhân lỗi phổ biến nhất: sai **hậu tố `/v1`** → `404 Not Found`; sai **host so với loại key** → `401 Unauthorized` dù key vẫn còn hiệu lực. Mọi trang hướng dẫn công cụ đều có tab riêng cho từng loại dịch vụ — chọn đúng tab rồi copy nguyên văn.
{% endhint %}

---

## Công cụ được hỗ trợ

### Claude Code

Claude Code CLI hỗ trợ override `ANTHROPIC_BASE_URL` — trỏ về endpoint GreenNode thay vì Anthropic trực tiếp. Toàn bộ session, tool call và subagent đều đi qua endpoint GreenNode, usage hiển thị trên AI Platform Console.

### OpenAI-compatible client

Bất kỳ tool nào cho phép set custom `base_url` theo OpenAI SDK format đều hoạt động — OpenAI Python/Node.js SDK, LiteLLM, Cursor, Continue.dev, và các IDE extension khác. Chỉ cần đổi base URL và key, không cần thay đổi code logic.

---

## Billing

| | PAYG | Token Plan |
|---|---|---|
| Cách tính | Credit-token, 1 credit = 1 VND | Prepaid trọn gói 30 ngày |
| Hạn mức | **Prepaid:** credit bị trừ mỗi chu kỳ collect 5 phút, hết credit → model bị tắt tự động. **Postpaid:** usage được ghi nợ, không giới hạn quota | Hạn mức token/request cố định theo từng model, dùng chung giữa các subscription-key trong gói |
| Theo dõi | [AI Platform Console](https://aiplatform.console.greennode.ai/) → **Usage** và **Cost** | [AI Platform Console](https://aiplatform.console.greennode.ai/) → chỉ **Usage** |

---

## Bắt đầu

| Tôi muốn... | Đi đến |
|---|---|
| Chuẩn bị key, Base URL, chọn model | [Bắt đầu với AI Coding](bat-dau.md) |
| Dùng công cụ có giao diện (GUI) | [Nhóm Có giao diện](co-giao-dien/README.md) |
| Dùng công cụ dòng lệnh (CLI) | [Nhóm Dòng lệnh](dong-lenh/README.md) |
| Cấu hình SDK / IDE extension theo chuẩn OpenAI | [Kết nối OpenAI-compatible với GreenNode MaaS](ket-noi-openai-compatible-voi-maas.md) |
| Gắn MCP server cho agent | [Dùng MCP Server với AI Coding](mcp-openrouter.md) |
| Mua và dùng gói Token Plan | [Token Plan](../token-plan/README.md) |
| Lấy API key PAYG | [AI Platform Console](https://aiplatform.console.greennode.ai/) |
