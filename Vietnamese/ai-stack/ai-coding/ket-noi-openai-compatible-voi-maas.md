# Kết nối OpenAI-compatible với GreenNode MaaS

> Hướng dẫn cấu hình các tool, SDK và IDE extension dùng OpenAI API format để gọi model qua endpoint GreenNode — dùng API Key **PAYG** hoặc subscription-key của gói **Token Plan**.

***

## Điều kiện cần (Prerequisites)

* Đã có tài khoản [AI Platform](https://aiplatform.console.greennode.ai/)
* Đã có key ở trạng thái **ACTIVE** — API Key (PAYG) hoặc subscription-key (Token Plan)
* Tool/SDK hỗ trợ tuỳ chỉnh base URL (OpenAI SDK, LiteLLM, Cursor, Continue.dev, v.v.)

***

## Chọn cấu hình theo loại dịch vụ

Mọi tool trên trang này dùng **chuẩn OpenAI** → Base URL **có** `/v1` ở cả hai loại dịch vụ. Chỉ khác host và loại key:

| Loại dịch vụ | Base URL | Key | Model |
|---|---|---|---|
| **PAYG** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | API Key từ [trang API Keys](https://aiplatform.console.greennode.ai/keys) | Model ID từ [portal Models](https://aiplatform.console.greennode.ai/models) (ví dụ `openai/gpt-4o`) |
| **Token Plan** | `https://tokenplan.api.greennode.ai/v1` | subscription-key từ Plan Detail → tab **Subscription keys** | Model code ở tab **Models** của gói (ví dụ `glm-5.2`) |

{% hint style="warning" %}
**Key và Base URL phải cùng một loại dịch vụ.** API Key PAYG gửi tới host `tokenplan…` (hoặc ngược lại) trả về `401 Unauthorized` dù key vẫn còn hiệu lực. Không nhận biết loại key bằng mắt được — nhớ theo nơi bạn đã lấy key. Xem [Mục 2 của trang Điều kiện cần](bat-dau.md).
{% endhint %}

Mọi ví dụ bên dưới đều có 2 tab — chọn đúng tab loại dịch vụ của bạn rồi copy nguyên văn, chỉ thay key và model.

***

## Bước 1 — Lấy key

{% tabs %}
{% tab title="PAYG — API Key" %}
1. Đăng nhập [AI Platform Console](https://aiplatform.console.greennode.ai/)
2. Vào **API Keys** → **Create API Key**
3. Đặt tên key (5–50 ký tự, chữ thường + số + gạch ngang)
4. Copy API key vừa tạo

{% hint style="warning" %}
API key mới tạo ở trạng thái `pending`. Đợi đến khi status = `ACTIVE` mới dùng được.
{% endhint %}
{% endtab %}

{% tab title="Token Plan — subscription-key" %}
1. Vào **API Key** → **Token Plan** → **My Token Plans**, mở gói đã mua
2. Tab **Subscription keys** → copy `default-key` hoặc key bạn tự tạo
3. Tab **Models** → copy **Model code** của model muốn dùng

Chưa có gói? Xem [Mua gói Token Plan](../token-plan/mua-goi-token-plan.md).
{% endtab %}
{% endtabs %}

***

## Bước 2 — Xem danh sách model khả dụng

{% tabs %}
{% tab title="PAYG" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/models \
  -H "Authorization: Bearer <API-key-PAYG-của-bạn>"
```

Dùng giá trị `id` trong response để điền vào tham số `model` khi gọi API.
{% endtab %}

{% tab title="Token Plan" %}
Danh sách model của gói xem trực tiếp trên **Plan Detail → tab Models** — cột **Model code** chính là giá trị điền vào tham số `model`.

Gói chỉ gọi được các model có trong tab này; model ngoài gói trả về `403 Forbidden`.
{% endtab %}
{% endtabs %}

***

## Bước 3 — Cấu hình client

### OpenAI Python SDK

{% tabs %}
{% tab title="PAYG" %}
```python
from openai import OpenAI

client = OpenAI(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
    api_key="<API-key-PAYG-của-bạn>",
)

response = client.chat.completions.create(
    model="openai/gpt-4o",
    messages=[{"role": "user", "content": "Hello"}],
)
print(response.choices[0].message.content)
```
{% endtab %}

{% tab title="Token Plan" %}
```python
from openai import OpenAI

client = OpenAI(
    base_url="https://tokenplan.api.greennode.ai/v1",
    api_key="<subscription-key-của-bạn>",
)

response = client.chat.completions.create(
    model="glm-5.2",   # Model code ở tab Models của gói
    messages=[{"role": "user", "content": "Hello"}],
)
print(response.choices[0].message.content)
```
{% endtab %}
{% endtabs %}

### OpenAI Node.js SDK

{% tabs %}
{% tab title="PAYG" %}
```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
  apiKey: "<API-key-PAYG-của-bạn>",
});

const response = await client.chat.completions.create({
  model: "openai/gpt-4o",
  messages: [{ role: "user", content: "Hello" }],
});
console.log(response.choices[0].message.content);
```
{% endtab %}

{% tab title="Token Plan" %}
```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "https://tokenplan.api.greennode.ai/v1",
  apiKey: "<subscription-key-của-bạn>",
});

const response = await client.chat.completions.create({
  model: "glm-5.2",   // Model code ở tab Models của gói
  messages: [{ role: "user", content: "Hello" }],
});
console.log(response.choices[0].message.content);
```
{% endtab %}
{% endtabs %}

### Biến môi trường (cho tool/CLI nhận OpenAI-compatible config)

{% tabs %}
{% tab title="PAYG" %}
```bash
export OPENAI_BASE_URL="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1"
export OPENAI_API_KEY="<API-key-PAYG-của-bạn>"
```
{% endtab %}

{% tab title="Token Plan" %}
```bash
export OPENAI_BASE_URL="https://tokenplan.api.greennode.ai/v1"
export OPENAI_API_KEY="<subscription-key-của-bạn>"
```
{% endtab %}
{% endtabs %}

### LiteLLM

{% tabs %}
{% tab title="PAYG" %}
```python
import litellm

response = litellm.completion(
    model="openai/gpt-4o",
    messages=[{"role": "user", "content": "Hello"}],
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
    api_key="<API-key-PAYG-của-bạn>",
)
print(response.choices[0].message.content)
```
{% endtab %}

{% tab title="Token Plan" %}
```python
import litellm

response = litellm.completion(
    model="glm-5.2",   # Model code ở tab Models của gói
    messages=[{"role": "user", "content": "Hello"}],
    base_url="https://tokenplan.api.greennode.ai/v1",
    api_key="<subscription-key-của-bạn>",
)
print(response.choices[0].message.content)
```
{% endtab %}
{% endtabs %}

### Cursor / Continue.dev

Trong phần cài đặt của tool, điền theo đúng loại dịch vụ của key:

| Trường | PAYG | Token Plan |
|---|---|---|
| **Base URL** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | `https://tokenplan.api.greennode.ai/v1` |
| **API Key** | API Key PAYG của bạn | subscription-key của bạn |
| **Model** | `openai/gpt-4o`, `gemini/gemini-2.5-flash`, `qwen/qwen3-27b` (hoặc model từ Bước 2) | Model code ở tab **Models** của gói |

***

## Bước 4 — Kiểm tra kết nối

Gửi request thử bằng curl:

{% tabs %}
{% tab title="PAYG" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer <API-key-PAYG-của-bạn>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "openai/gpt-4o",
    "messages": [{"role": "user", "content": "ping"}]
  }'
```
{% endtab %}

{% tab title="Token Plan" %}
```bash
curl https://tokenplan.api.greennode.ai/v1/chat/completions \
  -H "Authorization: Bearer <subscription-key-của-bạn>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "<model-code-từ-tab-Models>",
    "messages": [{"role": "user", "content": "ping"}]
  }'
```
{% endtab %}
{% endtabs %}

Kết quả mong đợi: response JSON có trường `choices[0].message.content`.

***

## Billing & Usage

| | PAYG | Token Plan |
|---|---|---|
| Cách tính phí | Trả theo token thực dùng, 1 credit = 1 VND | Prepaid cố định 30 ngày, hạn mức token/request theo từng model |
| Khi cạn | **Prepaid:** credit bị trừ mỗi chu kỳ collect 5 phút — hết credit thì model bị tắt tự động. **Postpaid:** usage được ghi nợ, không giới hạn quota | Hết hạn mức token của model đó thì request dừng — đợi chu kỳ mới, mua thêm gói, hoặc tạm chuyển sang API Key PAYG |
| Theo dõi | [AI Platform Console](https://aiplatform.console.greennode.ai/) → tab **Usage** và **Cost** | [AI Platform Console](https://aiplatform.console.greennode.ai/) → chỉ tab **Usage** (chi phí đã cố định lúc mua gói) |

***

## Troubleshooting

| Triệu chứng | Nguyên nhân | Cách xử lý |
|---|---|---|
| `401 Unauthorized` | Key sai hoặc chưa ACTIVE | Kiểm tra lại key và status của key |
| `401` dù key còn hiệu lực | **Key và Base URL lệch loại dịch vụ** | Đối chiếu bảng đầu trang: key ở trang **API Keys** → host `maas-llm-…`; key ở tab **Subscription keys** → host `tokenplan…` |
| `403 Forbidden` (Token Plan) | Model không nằm trong gói | Chỉ gọi model có trong tab **Models** của gói |
| `402 Payment Required` (Token Plan) | Gói hết hạn hoặc bị xoá | Mua lại gói hoặc bật **Auto-renew** |
| `404 Not Found` | Thiếu `/v1` trong URL | Chuẩn OpenAI — base URL phải kết thúc bằng `/v1` |
| Model không phản hồi | PAYG hết credit, hoặc Token Plan hết hạn mức token | PAYG: nạp thêm credit. Token Plan: đợi chu kỳ mới hoặc mua thêm gói |
| `OPENAI_BASE_URL` không nhận | Tool ghi đè bằng biến config riêng | Xem tài liệu của tool đó để set custom base URL |
| Response lỗi parse | Tool tự append `/v1` vào base URL | Thử bỏ `/v1` khỏi base URL nếu tool tự xử lý |

***

## Kết quả

Sau khi cấu hình, tool hoặc SDK sẽ gọi model qua endpoint GreenNode của loại dịch vụ bạn chọn thay vì OpenAI trực tiếp. Usage được ghi nhận trên AI Platform Console.

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Dùng Claude Code với MaaS | [Kết nối Claude Code với GreenNode MaaS](dong-lenh/claude-code.md) |
| Tìm hiểu gói Token Plan | [Token Plan](../token-plan/README.md) |
| Đi hết một vòng Token Plan từ mua gói đến chạy tool | [Hướng dẫn A-Z](../token-plan/huong-dan-a-z.md) |
| Xem usage và billing | [AI Platform Console](https://aiplatform.console.greennode.ai/) |
