# Kết nối OpenAI-compatible với GreenNode MaaS

> Hướng dẫn cấu hình các tool, SDK và IDE extension dùng OpenAI API format để gọi model qua GreenNode MaaS endpoint, thanh toán bằng credit-token nội bộ.

***

## Điều kiện cần (Prerequisites)

* Đã có tài khoản [AI Platform](https://aiplatform.console.vngcloud.vn/)
* Đã tạo API key với status **ACTIVE**
* Tool/SDK hỗ trợ tuỳ chỉnh base URL (OpenAI SDK, LiteLLM, Cursor, Continue.dev, v.v.)

{% hint style="info" %}
LLM URL cho OpenAI-compatible client: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` (có `/v1`). Khác với Claude Code dùng Anthropic protocol (không có `/v1`).
{% endhint %}

***

## Bước 1 — Lấy API key từ AI Platform

1. Đăng nhập [AI Platform Console](https://aiplatform.console.vngcloud.vn/)
2. Vào **API Keys** → **Create API Key**
3. Đặt tên key (5–50 ký tự, chữ thường + số + gạch ngang)
4. Copy API key vừa tạo

{% hint style="warning" %}
API key mới tạo ở trạng thái `pending`. Đợi đến khi status = `ACTIVE` mới dùng được.
{% endhint %}

***

## Bước 2 — Xem danh sách model

Lấy danh sách model khả dụng qua OpenAI-compatible endpoint:

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/models \
  -H "Authorization: Bearer <your-api-key>"
```

Dùng giá trị `id` trong response để điền vào tham số `model` khi gọi API.

***

## Bước 3 — Cấu hình client

**OpenAI Python SDK**

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
    api_key="<your-api-key>",
)

response = client.chat.completions.create(
    model="openai/gpt-4o",
    messages=[{"role": "user", "content": "Hello"}],
)
print(response.choices[0].message.content)
```

**OpenAI Node.js SDK**

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
  apiKey: "<your-api-key>",
});

const response = await client.chat.completions.create({
  model: "openai/gpt-4o",
  messages: [{ role: "user", content: "Hello" }],
});
console.log(response.choices[0].message.content);
```

**Biến môi trường (cho tool/CLI nhận OpenAI-compatible config)**

```bash
export OPENAI_BASE_URL="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1"
export OPENAI_API_KEY="<your-api-key>"
```

**LiteLLM**

```python
import litellm

response = litellm.completion(
    model="openai/gpt-4o",
    messages=[{"role": "user", "content": "Hello"}],
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
    api_key="<your-api-key>",
)
print(response.choices[0].message.content)
```

**Cursor / Continue.dev**

Trong phần cài đặt của tool, điền:

| Trường       | Giá trị                                              |
| ------------ | ---------------------------------------------------- |
| **Base URL** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| **API Key**  | `<your-api-key>`                                     |
| **Model**    | `openai/gpt-4o`, `gemini/gemini-2.5-flash`, `qwen/qwen3-27b` (hoặc model từ bước 2) |

***

## Bước 4 — Kiểm tra kết nối

Gửi request thử bằng curl:

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "openai/gpt-4o",
    "messages": [{"role": "user", "content": "ping"}]
  }'
```

Kết quả mong đợi: response JSON có trường `choices[0].message.content`.

***

## Billing & Usage

* Request đi qua GreenNode MaaS được tính phí bằng credit-token (1 credit = 1 VND)
* Xem usage real-time trên [AI Platform Console → Usage](https://aiplatform.console.vngcloud.vn/)
* **Prepaid:** credit bị trừ mỗi chu kỳ collect 5 phút — khi hết credit, model bị tắt tự động
* **Postpaid:** usage được ghi nợ, không giới hạn quota

***

## Troubleshooting

| Triệu chứng                  | Nguyên nhân                        | Cách xử lý                                      |
| ---------------------------- | ---------------------------------- | ----------------------------------------------- |
| `401 Unauthorized`           | API key sai hoặc chưa ACTIVE       | Kiểm tra lại key                                |
| `404 Not Found`              | Thiếu `/v1` trong URL              | Đảm bảo base URL kết thúc bằng `/v1`            |
| Model không phản hồi         | Credit hết, model bị tắt           | Nạp thêm credit tại AI Platform Console         |
| `OPENAI_BASE_URL` không nhận | Tool ghi đè bằng biến config riêng | Xem tài liệu của tool đó để set custom base URL |
| Response lỗi parse           | Tool tự append `/v1` vào base URL  | Thử bỏ `/v1` khỏi base URL nếu tool tự xử lý    |

***

## Kết quả

Sau khi cấu hình, tool hoặc SDK sẽ gọi model qua GreenNode MaaS thay vì OpenAI trực tiếp. Usage được ghi nhận trên AI Platform Console và tính phí theo credit-token nội bộ.

| Tôi muốn tiếp theo...     | Đi đến                                                                    |
| ------------------------- | ------------------------------------------------------------------------- |
| Dùng Claude Code với MaaS | [Kết nối Claude Code với GreenNode MaaS](ket-noi-claude-code-voi-maas.md) |
| Xem usage và billing      | [AI Platform Console](https://aiplatform.console.vngcloud.vn/)            |
