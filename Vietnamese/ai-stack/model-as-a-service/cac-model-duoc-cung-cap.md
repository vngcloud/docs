# Các Model được cung cấp

MaaS API cung cấp quyền truy cập với độ chính xác đầy đủ vào các họ mô hình Gemini, Anthropic, OpenAI... được liệt kê bên dưới.

{% hint style="info" %}
Danh mục model bên dưới đã được cập nhật theo lộ trình chuyển đổi bắt đầu **03/08/2026**, gồm model do GreenNode self-host và model third-party đã ký hợp đồng chính thức. Xem chi tiết mốc thời gian tại [Release Notes](../release-notes.md) và bảng giá đầy đủ tại [Bảng giá Model](bang-gia-model.md).
{% endhint %}

### Danh sách mô hình

MaaS hỗ trợ nhiều loại mô hình khác nhau:

#### _Chat_

| Model Name     | Provider    | Modalities (Input → Output)   | Rate Limit | Sẵn có từ    |
| --------------- | ----------- | ---------------------------------- | ---------- | ------------ |
| Kimi K2.7 Code | Moonshot AI | Text + Image → Text               | –          | 03/08/2026   |
| Kimi 2.6       | Moonshot AI | Text + Image + Video → Text       | –          | 03/08/2026   |
| GLM-5.2        | Zhipu AI    | Text → Text                        | –          | 03/08/2026   |
| Gemma 4 31B-IT | Google      | Text + Image → Text               | –          | 03/08/2026   |
| Qwen 3.7 Plus  | Qwen        | Text + Image + Video → Text       | –          | 03/08/2026   |
| Qwen 3.6 Plus  | Qwen        | Text + Image + Video → Text       | –          | 03/08/2026   |
| Qwen 3.6 Flash | Qwen        | Text + Image → Text               | –          | 03/08/2026   |
| MiniMax M3     | MiniMax     | Text + Image + Video → Text       | –          | 03/08/2026   |
| MiniMax M2.5   | MiniMax     | Text → Text                        | –          | 03/08/2026   |
| Opus 4.8       | Anthropic   | Text + Image → Text               | –          | 20/08/2026   |
| Sonnet 4.6     | Anthropic   | Text + Image → Text               | –          | 20/08/2026   |
| Haiku 4.5      | Anthropic   | Text + Image → Text               | –          | 20/08/2026   |
| GPT-5.4        | OpenAI      | Text + Image → Text               | –          | 20/08/2026   |
| GPT-5.4 Mini   | OpenAI      | Text + Image → Text               | –          | 20/08/2026   |
| GPT-5.4 Nano   | OpenAI      | Text + Image → Text               | –          | 20/08/2026   |
| GPT-5          | OpenAI      | Text + Image → Text               | –          | 20/08/2026   |
| GPT-5 Mini     | OpenAI      | Text + Image → Text               | –          | 20/08/2026   |
| GPT-5 Nano     | OpenAI      | Text + Image → Text               | –          | 20/08/2026   |
| GPT-4o         | OpenAI      | Text + Image → Text               | –          | 20/08/2026   |
| GPT-4o Mini    | OpenAI      | Text + Image → Text               | –          | 20/08/2026   |
| GPT-OSS 20B    | OpenAI      | Text → Text                        | –          | 20/08/2026   |
| GPT-OSS 120B   | OpenAI      | Text → Text                        | –          | 20/08/2026   |

{% hint style="info" %}
Modalities mô tả khả năng chung của model theo tài liệu của nhà cung cấp — khả năng thực tế có thể phụ thuộc vào endpoint API cụ thể được gọi qua MaaS. Model có mốc **03/08/2026** đã sẵn sàng sử dụng; model có mốc **20/08/2026** đang được triển khai dần và chưa khả dụng.
{% endhint %}

#### _Image Generation_

| Model Name    | Provider | Modalities (Input → Output) | Rate Limit | Sẵn có từ  |
| -------------- | -------- | ------------------------------- | ---------- | ---------- |
| gpt-image-2    | OpenAI   | Text + Image → Image           | –          | 20/08/2026 |

#### _Embedding_

| Model Name          | Provider | Modalities (Input → Output) | Rate Limit | Sẵn có từ  |
| -------------------- | -------- | ------------------------------- | ---------- | ---------- |
| Cohere Embed v4     | Cohere   | Text + Image → Vector          | –          | 20/08/2026 |
| Qwen3 Embedding 8B  | Qwen     | Text → Vector                   | –          | 20/08/2026 |

#### _Rerank_

| Model Name              | Provider | Modalities (Input → Output) | Rate Limit | Sẵn có từ  |
| ------------------------ | -------- | ------------------------------- | ---------- | ---------- |
| Cohere Rerank v4.0 pro  | Cohere   | Text → Ranked List             | –          | 20/08/2026 |

Lưu ý:

* Bạn có thể tạo [ticket](https://helpdesk.greennode.ai/portal/vi/newticket) để yêu cầu model mong muốn

