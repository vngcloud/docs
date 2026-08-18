# Available Models

The MaaS API provides full-accuracy access to model families such as Anthropic, OpenAI, Qwen, and others listed below.

{% hint style="info" %}
The model catalog below has been updated under the transition starting **August 3, 2026**, covering models self-hosted by GreenNode and third-party models under official contracts. See the timeline details in [Release Notes](../release-notes.md) and the billing rules in [Pricing](pricing.md).
{% endhint %}

### Model list

The **Provider Type** column tells you where your request is processed:

* **GreenNode self-host** — the model runs on GreenNode infrastructure.
* **Third-party** — the request is forwarded to the model vendor (Anthropic, OpenAI, Moonshot AI, Qwen, MiniMax, Cohere, etc.) under an official contract.

MaaS supports several model types:

#### _Chat_

| Model Name     | Provider Type       | Modalities (Input → Output)      | Rate Limit | Available From    |
| --------------- | ------------------- | ----------------------------------- | ---------- | ------------------ |
| Kimi K2.7 Code | Third-party         | Text + Image → Text               | –          | August 3, 2026     |
| Kimi 2.6       | Third-party         | Text + Image → Text               | –          | August 3, 2026     |
| GLM-5.2        | GreenNode self-host | Text → Text                        | –          | August 3, 2026     |
| Gemma 4 31B-IT | Third-party         | Text + Image → Text               | –          | August 3, 2026     |
| Qwen 3.7 Plus  | Third-party         | Text + Image + Video → Text       | –          | August 3, 2026     |
| Qwen 3.6 Plus  | Third-party         | Text + Image + Video → Text       | –          | August 3, 2026     |
| Qwen 3.6 Flash | Third-party         | Text + Image + Video → Text       | –          | August 3, 2026     |
| MiniMax M3     | Third-party         | Text + Image + Video → Text       | –          | August 3, 2026     |
| MiniMax M2.5   | Third-party         | Text → Text                        | –          | August 3, 2026     |
| Opus 4.8       | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| Sonnet 4.6     | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| Haiku 4.5      | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5.4        | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5.4 Mini   | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5.4 Nano   | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5          | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5 Mini     | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-5 Nano     | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-4o         | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-4o Mini    | Third-party         | Text + Image + File → Text        | –          | August 20, 2026    |
| GPT-OSS 20B    | Third-party         | Text → Text                        | –          | August 20, 2026    |
| GPT-OSS 120B   | Third-party         | Text → Text                        | –          | August 20, 2026    |

{% hint style="info" %}
Modalities describe the model's general capability per its provider's documentation — actual support may depend on the specific API endpoint used via MaaS. Models listed as **August 3, 2026** are live now; models listed as **August 20, 2026** are rolling out progressively and are not yet available.
{% endhint %}

#### _Image Generation_

| Model Name    | Provider Type | Modalities (Input → Output) | Rate Limit | Available From |
| -------------- | ------------- | ------------------------------- | ---------- | --------------- |
| gpt-image-2    | Third-party   | Text + Image → Image           | –          | August 20, 2026 |

#### _Embedding_

| Model Name          | Provider Type       | Modalities (Input → Output) | Rate Limit | Available From |
| -------------------- | ------------------- | ------------------------------- | ---------- | --------------- |
| Cohere Embed v4     | Third-party         | Text + Image → Vector          | –          | August 20, 2026 |
| Qwen3 Embedding 8B  | Third-party         | Text → Vector                   | –          | August 20, 2026 |

#### _Rerank_

| Model Name              | Provider Type | Modalities (Input → Output) | Rate Limit | Available From |
| ------------------------ | ------------- | ------------------------------- | ---------- | --------------- |
| Cohere Rerank v4.0 pro  | Third-party   | Text → Ranked List             | –          | August 20, 2026 |

Note:

* You can create [ticket](https://helpdesk.greennode.ai/portal/vi/newticket) for request new model
