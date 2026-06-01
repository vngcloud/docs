# Connect OpenAI-compatible Clients to GreenNode MaaS

> Configure tools, SDKs, and IDE extensions that use the OpenAI API format to call models through GreenNode MaaS, billed via internal credit-tokens.

---

## Prerequisites

- An active [AI Platform](https://aiplatform.console.vngcloud.vn/) account
- An API key with status **ACTIVE**
- A tool or SDK that supports a custom base URL (OpenAI SDK, LiteLLM, Cursor, Continue.dev, etc.)

{% hint style="info" %}
The LLM URL for OpenAI-compatible clients is `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` (with `/v1`). This differs from Claude Code, which uses the Anthropic protocol (no `/v1`).
{% endhint %}

---

## Step 1 — Get an API key from AI Platform

1. Log in to [AI Platform Console](https://aiplatform.console.vngcloud.vn/)
2. Go to **API Keys** → **Create API Key**
3. Name the key (5–50 chars, lowercase letters, numbers, and hyphens)
4. Copy the API key — it is shown only once

{% hint style="warning" %}
A newly created API key has status `pending`. Wait until the status is `ACTIVE` before using it.
{% endhint %}

---

## Step 2 — List available models

Fetch available models via the OpenAI-compatible endpoint:

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/models \
  -H "Authorization: Bearer <your-api-key>"
```

Use the `id` value from the response as the `model` parameter in your API calls.

---

## Step 3 — Configure the client

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

**Environment variables (for OpenAI-compatible tools and CLIs)**

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

In the tool's settings, fill in:

| Field | Value |
|---|---|
| **Base URL** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| **API Key** | `<your-api-key>` |
| **Model** | `openai/gpt-4o`, `gemini/gemini-2.5-flash`, `qwen/qwen3-27b` (or the model ID from Step 2) |

---

## Step 4 — Verify the connection

Send a test request with curl:

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "openai/gpt-4o",
    "messages": [{"role": "user", "content": "ping"}]
  }'
```

Expected result: a JSON response containing `choices[0].message.content`.

---

## Billing & Usage

- Requests through GreenNode MaaS are billed in credit-tokens (1 credit = 1 VND)
- View real-time usage on [AI Platform Console → Usage](https://aiplatform.console.vngcloud.vn/)
- **Prepaid:** credits are deducted every 5-minute collection cycle — when credits run out, the model is automatically disabled
- **Postpaid:** usage is recorded as a debt with no quota limit

---

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `401 Unauthorized` | Wrong or inactive API key | Verify the key |
| `404 Not Found` | Missing `/v1` in the URL | Ensure the base URL ends with `/v1` |
| Model not responding | Credits exhausted, model disabled | Add credits in AI Platform Console |
| `OPENAI_BASE_URL` not recognized | Tool uses its own config variable | Check the tool's docs for setting a custom base URL |
| Response parse error | Tool auto-appends `/v1` to base URL | Try removing `/v1` from the base URL if the tool handles it |

---

## Result

After configuration, the tool or SDK calls models through GreenNode MaaS instead of OpenAI directly. Usage is recorded in AI Platform Console and billed via internal credit-tokens.

| I want to... | Go to |
|---|---|
| Use Claude Code with MaaS | [Connect Claude Code to GreenNode MaaS](connect-claude-code-to-maas.md) |
| View usage and billing | [AI Platform Console](https://aiplatform.console.vngcloud.vn/) |
