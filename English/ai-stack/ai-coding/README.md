# AI Coding

AI Coding lets you connect popular AI coding tools — Claude Code, OpenAI SDK, IDE extensions — directly to models operated by GreenNode, using cloud models without managing API keys from external providers.

***

## Architecture

Requests from your tool are redirected to a GreenNode endpoint. The endpoint exposes two protocols in parallel to support all existing clients:

<figure><img src="../../.gitbook/assets/ai_coding_flow (1).png" alt=""><figcaption><p>Both API protocols connect to a single endpoint sharing the same Model Pool</p></figcaption></figure>

A single key works for both protocols — but the **key must match the host of the service type that issued it**.

***

## Two service types — settle this before configuring anything

| Service type | Pricing model | Key used to call | Base URL host |
|---|---|---|---|
| **PAYG** | Pay per token actually used | API Key from **API Keys** | `maas-llm-aiplatform-hcm.api.vngcloud.vn` |
| **Token Plan** | Prepaid 30-day package with a fixed token quota | subscription-key from Plan Detail → **Subscription keys** tab | `tokenplan.api.greennode.ai` |

***

## Base URL by service type and client standard

| Service type | **Anthropic**-standard clients<br>(Claude Code, Anthropic SDK) | **OpenAI**-standard clients<br>(OpenAI SDK, LiteLLM, Cursor, Continue.dev, Codex, OpenCode) |
|---|---|---|
| **PAYG** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| **Token Plan** | `https://tokenplan.api.greennode.ai` | `https://tokenplan.api.greennode.ai/v1` |

{% hint style="warning" %}
Picking the wrong cell in this table is the most common failure: the wrong **`/v1` suffix** gives `404 Not Found`; the wrong **host for your key type** gives `401 Unauthorized` even while the key is still valid. Every tool guide has separate tabs per service type — pick your tab and copy it as-is.
{% endhint %}

***

## Supported Tools

### Claude Code

Claude Code CLI supports overriding `ANTHROPIC_BASE_URL` — pointing to a GreenNode endpoint instead of Anthropic directly. All sessions, tool calls, and sub-agents route through the GreenNode endpoint, with usage visible in AI Platform Console.

### OpenAI-compatible clients

Any tool that allows setting a custom `base_url` in OpenAI SDK format works out of the box — OpenAI Python/Node.js SDK, LiteLLM, Cursor, Continue.dev, and other IDE extensions. Change the base URL and key; no logic changes needed.

***

## Billing

| | PAYG | Token Plan |
|---|---|---|
| Pricing | Credit-token, 1 credit = 1 VND | Fixed prepaid 30-day package |
| Quota | **Prepaid:** credits deducted every 5-minute collection cycle; model auto-disabled when credits run out. **Postpaid:** usage recorded as debt with no quota limit | Fixed token/request quota per model, shared across all subscription-keys in the plan |
| Where to track | [AI Platform Console](https://aiplatform.console.greennode.ai/) → **Usage** and **Cost** | [AI Platform Console](https://aiplatform.console.greennode.ai/) → **Usage** only |

***

## Getting Started

| I want to... | Go to |
|---|---|
| Prepare a key and Base URL, and choose a model | [Getting Started with AI Coding](getting-started.md) |
| Use a GUI tool | [GUI Tools group](gui-tools/README.md) |
| Use a CLI tool | [CLI Tools group](cli-tools/README.md) |
| Configure an SDK / IDE extension on the OpenAI standard | [Connect OpenAI-compatible Tools to GreenNode MaaS](connect-openai-compatible-to-maas.md) |
| Attach an MCP server to an agent | [Using MCP Servers with AI Coding](mcp-servers.md) |
| Buy and use a Token Plan package | [Token Plan](../token-plan/README.md) |
| Get a PAYG API key | [AI Platform Console](https://aiplatform.console.greennode.ai/) |
