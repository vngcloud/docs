---
description: "DeepSeek-V4-Flash is the efficiency-optimized tier of the DeepSeek-V4 family: a 284B-parameter Mixture-of-Experts model with only 13B active parameters per token, sharing the Pro tier's hybrid attention architecture (CSA + HCA)..."
---

# DeepSeek V4 Flash

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `deepseek/deepseek-v4-flash` · Loại: Chat

DeepSeek-V4-Flash is the efficiency-optimized tier of the DeepSeek-V4 family: a 284B-parameter Mixture-of-Experts model with only 13B active parameters per token, sharing the Pro tier's hybrid attention architecture (CSA + HCA)...

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 1M tokens |
| Output tối đa | 384K tokens |
| Đầu vào | text |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Luôn bật
* Các mức `reasoning_effort`: `low`, `medium`, `high`, `xhigh`, `max`
* Mức mặc định: `high`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek/deepseek-v4-flash",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
