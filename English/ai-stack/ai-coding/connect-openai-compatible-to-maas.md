# Connect OpenAI-compatible Tools to GreenNode MaaS

> Guide to configuring tools, SDKs, and IDE extensions that speak the OpenAI API format to call models through a GreenNode endpoint — using either a **PAYG** API Key or a **Token Plan** subscription-key.

***

## Prerequisites

* An [AI Platform](https://aiplatform.console.greennode.ai/) account
* A key in **ACTIVE** status — either an API Key (PAYG) or a subscription-key (Token Plan)
* A tool/SDK that supports a custom base URL (OpenAI SDK, LiteLLM, Cursor, Continue.dev, etc.)

***

## Pick your configuration by service type

Every tool on this page uses the **OpenAI standard** → the Base URL **includes** `/v1` on both service types. Only the host and the key type differ:

| Service type | Base URL | Key | Model |
|---|---|---|---|
| **PAYG** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | API Key from the [API Keys page](https://aiplatform.console.greennode.ai/keys) | Model ID from the [Models portal](https://aiplatform.console.greennode.ai/models) (e.g. `openai/gpt-4o`) |
| **Token Plan** | `https://tokenplan.api.greennode.ai/v1` | subscription-key from Plan Detail → **Subscription keys** tab | Model code on the plan's **Models** tab (e.g. `glm-5.2`) |

{% hint style="warning" %}
**Your key and Base URL must belong to the same service type.** A PAYG API Key sent to the `tokenplan…` host (or the reverse) returns `401 Unauthorized` even while the key is still valid. You can't tell the key types apart by looking at them — go by where you got the key. See [section 2 of the Prerequisites page](getting-started.md).
{% endhint %}

Every example below has 2 tabs — pick the tab for your service type and copy it as-is, replacing only the key and the model.

***

## Step 1 — Get your key

{% tabs %}
{% tab title="PAYG — API Key" %}
1. Log in to the [AI Platform Console](https://aiplatform.console.greennode.ai/)
2. Go to **API Keys** → **Create API Key**
3. Name the key (5–50 characters, lowercase letters + numbers + hyphens)
4. Copy the API key you just created

{% hint style="warning" %}
A newly created API key starts in `pending` status. Wait until status = `ACTIVE` before using it.
{% endhint %}
{% endtab %}

{% tab title="Token Plan — subscription-key" %}
1. Go to **API Key** → **Token Plan** → **My Token Plans** and open the plan you bought
2. **Subscription keys** tab → copy `default-key` or a key you created
3. **Models** tab → copy the **Model code** of the model you want

No plan yet? See [Buy Token Plan](../token-plan/buy-token-plan.md).
{% endtab %}
{% endtabs %}

***

## Step 2 — List the available models

{% tabs %}
{% tab title="PAYG" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/models \
  -H "Authorization: Bearer <your-PAYG-API-key>"
```

Use the `id` value from the response as the `model` parameter when calling the API.
{% endtab %}

{% tab title="Token Plan" %}
Your plan's model list is shown directly on **Plan Detail → Models tab** — the **Model code** column is exactly what goes into the `model` parameter.

A plan can only call the models listed on that tab; anything else returns `403 Forbidden`.
{% endtab %}
{% endtabs %}

***

## Step 3 — Configure your client

### OpenAI Python SDK

{% tabs %}
{% tab title="PAYG" %}
```python
from openai import OpenAI

client = OpenAI(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
    api_key="<your-PAYG-API-key>",
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
    api_key="<your-subscription-key>",
)

response = client.chat.completions.create(
    model="glm-5.2",   # Model code from your plan's Models tab
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
  apiKey: "<your-PAYG-API-key>",
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
  apiKey: "<your-subscription-key>",
});

const response = await client.chat.completions.create({
  model: "glm-5.2",   // Model code from your plan's Models tab
  messages: [{ role: "user", content: "Hello" }],
});
console.log(response.choices[0].message.content);
```
{% endtab %}
{% endtabs %}

### Environment variables (for tools/CLIs that read OpenAI-compatible config)

{% tabs %}
{% tab title="PAYG" %}
```bash
export OPENAI_BASE_URL="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1"
export OPENAI_API_KEY="<your-PAYG-API-key>"
```
{% endtab %}

{% tab title="Token Plan" %}
```bash
export OPENAI_BASE_URL="https://tokenplan.api.greennode.ai/v1"
export OPENAI_API_KEY="<your-subscription-key>"
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
    api_key="<your-PAYG-API-key>",
)
print(response.choices[0].message.content)
```
{% endtab %}

{% tab title="Token Plan" %}
```python
import litellm

response = litellm.completion(
    model="glm-5.2",   # Model code from your plan's Models tab
    messages=[{"role": "user", "content": "Hello"}],
    base_url="https://tokenplan.api.greennode.ai/v1",
    api_key="<your-subscription-key>",
)
print(response.choices[0].message.content)
```
{% endtab %}
{% endtabs %}

### Cursor / Continue.dev

In the tool's settings, fill in the values for your key's service type:

| Field | PAYG | Token Plan |
|---|---|---|
| **Base URL** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | `https://tokenplan.api.greennode.ai/v1` |
| **API Key** | your PAYG API Key | your subscription-key |
| **Model** | `openai/gpt-4o`, `gemini/gemini-2.5-flash`, `qwen/qwen3-27b` (or a model from Step 2) | Model code on the plan's **Models** tab |

***

## Step 4 — Test the connection

Send a test request with curl:

{% tabs %}
{% tab title="PAYG" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer <your-PAYG-API-key>" \
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
  -H "Authorization: Bearer <your-subscription-key>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "<model-code-from-Models-tab>",
    "messages": [{"role": "user", "content": "ping"}]
  }'
```
{% endtab %}
{% endtabs %}

Expected result: a JSON response containing `choices[0].message.content`.

***

## Billing & Usage

| | PAYG | Token Plan |
|---|---|---|
| Pricing model | Pay per token actually used, 1 credit = 1 VND | Fixed prepaid 30-day package, token/request quota per model |
| When it runs out | **Prepaid:** credit is deducted every 5-minute collection cycle — when credit hits zero, the model is auto-disabled. **Postpaid:** usage is billed on account, no quota cap | Once that model's token quota is exhausted, requests stop — wait for the next cycle, buy another plan, or temporarily switch to a PAYG API Key |
| Where to track | [AI Platform Console](https://aiplatform.console.greennode.ai/) → **Usage** and **Cost** tabs | [AI Platform Console](https://aiplatform.console.greennode.ai/) → **Usage** tab only (cost was fixed at purchase) |

***

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `401 Unauthorized` | Wrong or not-yet-ACTIVE key | Re-check the key and its status |
| `401` while the key is still valid | **Key and Base URL belong to different service types** | Re-check the table at the top: a key from the **API Keys** page → the `maas-llm-…` host; a key from the **Subscription keys** tab → the `tokenplan…` host |
| `403 Forbidden` (Token Plan) | Model isn't included in the plan | Only call models listed on the plan's **Models** tab |
| `402 Payment Required` (Token Plan) | Plan expired or was deleted | Buy the plan again or enable **Auto-renew** |
| `404 Not Found` | Missing `/v1` in the URL | OpenAI standard — the base URL must end with `/v1` |
| Model doesn't respond | PAYG out of credit, or Token Plan out of token quota | PAYG: top up credit. Token Plan: wait for the next cycle or buy another plan |
| `OPENAI_BASE_URL` ignored | The tool overrides it with its own config variable | Check that tool's docs for how to set a custom base URL |
| Response parse errors | The tool appends `/v1` to the base URL itself | Try removing `/v1` from the base URL if the tool handles it |

***

## Result

Your tool or SDK now calls models through the GreenNode endpoint for your chosen service type instead of OpenAI directly. Usage is recorded in the AI Platform Console.

| I want to next... | Go to |
|---|---|
| Use Claude Code with MaaS | [Claude Code](cli-tools/claude-code.md) |
| Learn about Token Plan packages | [Token Plan](../token-plan/README.md) |
| Walk Token Plan end-to-end, from purchase to a running tool | [A-Z Guide](../token-plan/a-z-guide.md) |
| View usage and billing | [AI Platform Console](https://aiplatform.console.greennode.ai/) |
