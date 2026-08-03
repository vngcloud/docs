# Available Models

The MaaS API provides full-accuracy access to model families such as Gemini, Anthropic, OpenAI, and others listed below.

{% hint style="info" %}
The model catalog below has been updated under the transition starting **August 3, 2026**, covering models self-hosted by GreenNode and third-party models under official contracts. See the timeline details in [Release Notes](../release-notes.md) and the full price list in [Model Pricing List](model-pricing-list.md).
{% endhint %}

### Danh sách mô hình

MaaS hỗ trợ nhiều loại mô hình khác nhau:

#### _**Chat**_

| Model Name     | Provider    | Modalities (Input → Output)      | Rate Limit | Available From    |
| --------------- | ----------- | ----------------------------------- | ---------- | ------------------ |
| Kimi K2.7 Code | Moonshot AI | Text + Image → Text               | –          | August 3, 2026     |
| Kimi 2.6       | Moonshot AI | Text + Image → Text               | –          | August 3, 2026     |
| GLM-5.2        | Zhipu AI    | Text → Text                        | –          | August 3, 2026     |
| Gemma 4 31B-IT | Google      | Text + Image → Text               | –          | August 3, 2026     |
| Qwen 3.7 Plus  | Qwen        | Text + Image + Video → Text       | –          | August 3, 2026     |
| Qwen 3.6 Plus  | Qwen        | Text + Image + Video → Text       | –          | August 3, 2026     |
| Qwen 3.6 Flash | Qwen        | Text + Image + Video → Text       | –          | August 3, 2026     |
| MiniMax M3     | MiniMax     | Text + Image + Video → Text       | –          | August 3, 2026     |
| MiniMax M2.5   | MiniMax     | Text → Text                        | –          | August 3, 2026     |
| Opus 4.8       | Anthropic   | Text + Image + File → Text        | –          | August 20, 2026    |
| Sonnet 4.6     | Anthropic   | Text + Image + File → Text        | –          | August 20, 2026    |
| Haiku 4.5      | Anthropic   | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5.4        | OpenAI      | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5.4 Mini   | OpenAI      | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5.4 Nano   | OpenAI      | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5          | OpenAI      | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5 Mini     | OpenAI      | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5 Nano     | OpenAI      | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-4o         | OpenAI      | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-4o Mini    | OpenAI      | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-OSS 20B    | OpenAI      | Text → Text                        | –          | August 20, 2026    |
| GPT-OSS 120B   | OpenAI      | Text → Text                        | –          | August 20, 2026    |

{% hint style="info" %}
Modalities describe the model's general capability per its provider's documentation — actual support may depend on the specific API endpoint used via MaaS. Models listed as **August 3, 2026** are live now; models listed as **August 20, 2026** are rolling out progressively and are not yet available.
{% endhint %}

#### _Image Generation_

| Model Name    | Provider | Modalities (Input → Output) | Rate Limit | Available From |
| -------------- | -------- | ------------------------------- | ---------- | --------------- |
| gpt-image-2    | OpenAI   | Text + Image → Image           | –          | August 20, 2026 |

#### _Embedding_

| Model Name          | Provider | Modalities (Input → Output) | Rate Limit | Available From |
| -------------------- | -------- | ------------------------------- | ---------- | --------------- |
| Cohere Embed v4     | Cohere   | Text + Image → Vector          | –          | August 20, 2026 |
| Qwen3 Embedding 8B  | Qwen     | Text → Vector                   | –          | August 20, 2026 |

#### _Rerank_

| Model Name              | Provider | Modalities (Input → Output) | Rate Limit | Available From |
| ------------------------ | -------- | ------------------------------- | ---------- | --------------- |
| Cohere Rerank v4.0 pro  | Cohere   | Text → Ranked List             | –          | August 20, 2026 |

Note:

* You can create [ticket](https://helpdesk.greennode.ai/portal/vi/newticket) for request new model
