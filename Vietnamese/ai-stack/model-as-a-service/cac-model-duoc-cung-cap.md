# Các Model được cung cấp

MaaS API cung cấp quyền truy cập với độ chính xác đầy đủ vào các họ mô hình Anthropic, OpenAI, Qwen... được liệt kê bên dưới.

{% hint style="info" %}
Danh mục model bên dưới đã được cập nhật theo lộ trình chuyển đổi bắt đầu **03/08/2026**, gồm model do GreenNode self-host và model third-party đã ký hợp đồng chính thức. Xem chi tiết mốc thời gian tại [Release Notes](../release-notes.md) và nguyên tắc tính phí tại [Cách tính phí](cach-tinh-phi.md).
{% endhint %}

### Rate limit

Mặc định áp dụng cho **mọi tài khoản** dùng MaaS API:

| Giới hạn | Giá trị |
| --- | --- |
| Theo phút | **10 RPM** — 10 request/phút |
| Theo ngày | **14.400 request/ngày** |

Giới hạn được tính trên **tài khoản** và dùng chung cho mọi model — không phải hạn mức riêng của từng model. Trong các bảng bên dưới, cột **Rate Limit** hiển thị `–` nghĩa là model đó không có giới hạn riêng và áp dụng mức mặc định này.

{% hint style="info" %}
Cần mức cao hơn 10 RPM? Hãy [liên hệ GreenNode](https://helpdesk.greennode.ai/portal/vi/newticket) để được xem xét đưa vào **whitelist**. Whitelist được xét theo từng trường hợp cụ thể.
{% endhint %}

***

### Danh sách mô hình

Cột **Loại Provider** cho biết request của bạn được xử lý ở đâu:

* **GreenNode self-host** — model chạy trên hạ tầng của GreenNode.
* **Third-party** — request được chuyển tiếp đến nhà cung cấp model (Anthropic, OpenAI, Moonshot AI, Qwen, MiniMax, Cohere...) theo hợp đồng chính thức.

MaaS hỗ trợ nhiều loại mô hình khác nhau:

#### _Chat_

| Model Name     | Loại Provider       | Modalities (Input → Output)   | Rate Limit | Sẵn có từ    |
| --------------- | ------------------- | ---------------------------------- | ---------- | ------------ |
| Kimi K2.7 Code | Third-party         | Text + Image → Text               | –          | 03/08/2026   |
| Kimi 2.6       | Third-party         | Text + Image → Text               | –          | 03/08/2026   |
| GLM-5.2        | GreenNode self-host | Text → Text                        | –          | 03/08/2026   |
| Gemma 4 31B-IT | Third-party         | Text + Image → Text               | –          | 03/08/2026   |
| Qwen 3.7 Plus  | Third-party         | Text + Image + Video → Text       | –          | 03/08/2026   |
| Qwen 3.6 Plus  | Third-party         | Text + Image + Video → Text       | –          | 03/08/2026   |
| Qwen 3.6 Flash | Third-party         | Text + Image + Video → Text       | –          | 03/08/2026   |
| MiniMax M3     | Third-party         | Text + Image + Video → Text       | –          | 03/08/2026   |
| MiniMax M2.5   | Third-party         | Text → Text                        | –          | 03/08/2026   |
| Opus 4.8       | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| Sonnet 4.6     | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| Haiku 4.5      | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| GPT-5.4        | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| GPT-5.4 Mini   | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| GPT-5.4 Nano   | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| GPT-5          | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| GPT-5 Mini     | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| GPT-5 Nano     | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| GPT-4o         | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| GPT-4o Mini    | Third-party         | Text + Image + File → Text        | –          | 20/08/2026   |
| GPT-OSS 20B    | Third-party         | Text → Text                        | –          | 20/08/2026   |
| GPT-OSS 120B   | Third-party         | Text → Text                        | –          | 20/08/2026   |

{% hint style="info" %}
Modalities mô tả khả năng chung của model theo tài liệu của nhà cung cấp — khả năng thực tế có thể phụ thuộc vào endpoint API cụ thể được gọi qua MaaS. Model có mốc **03/08/2026** đã sẵn sàng sử dụng; model có mốc **20/08/2026** đang được triển khai dần và chưa khả dụng.
{% endhint %}

#### _Image Generation_

| Model Name    | Loại Provider | Modalities (Input → Output) | Rate Limit | Sẵn có từ  |
| -------------- | ------------- | ------------------------------- | ---------- | ---------- |
| gpt-image-2    | Third-party   | Text + Image → Image           | –          | 20/08/2026 |

#### _Embedding_

| Model Name          | Loại Provider       | Modalities (Input → Output) | Rate Limit | Sẵn có từ  |
| -------------------- | ------------------- | ------------------------------- | ---------- | ---------- |
| Cohere Embed v4     | Third-party         | Text + Image → Vector          | –          | 20/08/2026 |
| Qwen3 Embedding 8B  | Third-party         | Text → Vector                   | –          | 20/08/2026 |

#### _Rerank_

| Model Name              | Loại Provider | Modalities (Input → Output) | Rate Limit | Sẵn có từ  |
| ------------------------ | ------------- | ------------------------------- | ---------- | ---------- |
| Cohere Rerank v4.0 pro  | Third-party   | Text → Ranked List             | –          | 20/08/2026 |

