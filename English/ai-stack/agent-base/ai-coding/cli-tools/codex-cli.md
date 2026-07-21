# Use Codex with Minimax via GreenNode MaaS

> Guide to configuring the [OpenAI Codex CLI](https://github.com/openai/codex) to call the Minimax model via GreenNode MaaS — using the Responses API through a custom `maas` provider defined in `codex.toml`.

***

## Prerequisites

* Prepare your API key, Base URL, and model following [Getting Started with AI Coding](../getting-started.md)
* Node.js ≥ 22 installed

> The GLM 5.2 model via Codex uses the **OpenAI standard** — the Base URL includes `/v1`: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1`.

***

## Step 1 — Install Codex CLI

```bash
npm install -g @openai/codex
```

Confirm the install succeeded:

```bash
codex --version
```

***

## Step 2 — Get an API key from AI Platform

1. Log in to the [AI Platform Console](https://aiplatform.console.greennode.ai/)
2. Go to **API Keys** → **Create API Key**
3. Name the key (5–50 characters, lowercase letters + numbers + hyphens)
4. Copy the API key (`vn-...`) you just created

{% hint style="warning" %}
A newly created API key starts in `pending` status. Wait until status = `ACTIVE` before using it.
{% endhint %}

***

## Step 3 — Configure `codex.toml`

Create or edit `~/.codex/config.toml` (system-wide config) or `codex.toml` at your project root (applies to that project only):

```toml
# API key — export before running Codex
# export MAAS_API_KEY="vn-...your-gateway-token..."

model_provider = "maas"
model = "minimax/minimax-m2.5"

# Needed because MAAS doesn't return model metadata — avoids incorrect context truncation
model_context_window = 204800
model_max_output_tokens = 16400

# The MAAS backend is stateless — Codex must resend the full conversation every turn
disable_response_storage = true

[model_providers.maas]
name = "MAAS AI Gateway"

# base_url has NO trailing /responses — Codex appends it automatically (→ .../v1/responses)
base_url = "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1"
env_key = "MAAS_API_KEY"
wire_api = "responses"
request_max_retries = 3
```

**Key field explanations:**

| Field | Purpose |
|---|---|
| `model_provider` | The provider key under `[model_providers.*]` |
| `model` | Model ID sent to MaaS |
| `model_context_window` | Set manually since MaaS doesn't expose model metadata |
| `disable_response_storage` | Required for the stateless backend — resend the full conversation every turn |
| `base_url` | MaaS endpoint with `/v1` — Codex appends `/responses` after it |
| `env_key` | Name of the environment variable holding the API key |
| `wire_api` | Protocol used — `responses` corresponds to the OpenAI Responses API |

***

## Step 4 — Set the API key and run Codex

Export the API key in your shell:

```bash
export MAAS_API_KEY="vn-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

To do this automatically every time you open a terminal, add it to `~/.zshrc` or `~/.bashrc`:

```bash
echo 'export MAAS_API_KEY="vn-xxxx..."' >> ~/.zshrc
source ~/.zshrc
```

Run Codex inside your project directory:

```bash
codex
```

Codex will show the provider and model in use in the session header:

```
model:     minimax/minimax-m2.5   /model to change
directory: ~/your-project
```

<figure><img src="../../../../.gitbook/assets/Agentbase-image/use-codex-with-minimax.png" alt=""><figcaption><p>Codex running with the minimax/minimax-m2.5 model via GreenNode MaaS</p></figcaption></figure>

***

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `401 Unauthorized` | Wrong, missing, or not-yet-ACTIVE API key | Re-export `MAAS_API_KEY`; check the key's status in the AI Platform Console |
| `404` when sending a request | `base_url` wrong or missing `/v1` | Make sure `base_url` ends with `/v1` (no `/responses`) |
| Context truncated incorrectly | Model metadata not declared | Check `model_context_window` and `model_max_output_tokens` in the config |
| Loses context every turn | `disable_response_storage` not set | Add `disable_response_storage = true` to the config |
| Connection timeout | Endpoint unreachable | Check VPN / connection to `*.api.vngcloud.vn` |

***

## Result

Once done, the Codex CLI routes all requests through GreenNode MaaS using the Minimax model. Usage is logged on the [AI Platform Console → Usage](https://aiplatform.console.greennode.ai/).

| I want to next... | Go to |
|---|---|
| Use OpenCode with MaaS | [Use OpenCode with GreenNode MaaS](opencode.md) |
| Connect Claude Code to MaaS | [Connect Claude Code to GreenNode MaaS](claude-code.md) |
| View usage and billing | [AI Platform Console](https://aiplatform.console.greennode.ai/) |

***

## Need help?

If you've followed the steps and it's still not working, feel free to contact GreenNode Customer Support:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Help center: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Thank you for using GreenNode's services.
