---
description: "GLM-5.3-Flash is the first natively multimodal model in Z.ai's GLM-5 series, released August 26, 2026 under the MIT license. Built on a 320B-parameter Mixture-of-Experts architecture with ~18B active parameters per..."
---

# GLM-5.3 Flash

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `z-ai/glm-5.3-flash-thirdparty` · Type: Chat

GLM-5.3-Flash is the first natively multimodal model in Z.ai's GLM-5 series, released August 26, 2026 under the MIT license. Built on a 320B-parameter Mixture-of-Experts architecture with ~18B active parameters per...

## Specs

| Spec | Value |
| --- | --- |
| Context length | 1M tokens |
| Max output | 128K tokens |
| Input | text, image, video |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: Always on
* `reasoning_effort` levels: `low`, `high`, `xhigh`, `max`
* Default effort: `max`

## Supported parameters

`frequency_penalty`, `include_reasoning`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.3-flash-thirdparty",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
