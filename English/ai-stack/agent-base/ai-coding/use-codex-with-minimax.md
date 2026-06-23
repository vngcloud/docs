# Use Codex with Minimax via GreenNode MaaS

> Configure [OpenAI Codex CLI](https://github.com/openai/codex) to call Minimax models through GreenNode MaaS — using the Responses API via a custom `maas` provider defined in `codex.toml`.

---

## Prerequisites

- An active [AI Platform](https://aiplatform.console.vngcloud.vn/) account
- API key (`vn-...` token) with status **ACTIVE**
- Node.js ≥ 22 installed

---

## Step 1 — Install Codex CLI

```bash
npm install -g @openai/codex
```

Verify the installation:

```bash
codex --version
```

---

## Step 2 — Get an API key from AI Platform

1. Log in to [AI Platform Console](https://aiplatform.console.vngcloud.vn/)
2. Go to **API Keys** → **Create API Key**
3. Name the key (5–50 chars, lowercase letters, numbers, and hyphens)
4. Copy the API key (`vn-...`)

{% hint style="warning" %}
A newly created API key has status `pending`. Wait until the status is `ACTIVE` before using it.
{% endhint %}

---

## Step 3 — Configure `codex.toml`

Create or edit `~/.codex/config.toml` (system-wide) or `codex.toml` at the project root (project-scoped):

```toml
# API key — export before running Codex
# export MAAS_API_KEY="vn-...your-gateway-token..."

model_provider = "maas"
model = "minimax/minimax-m2.5"

# Required because MAAS does not expose model metadata — prevents incorrect context truncation
model_context_window = 204800
model_max_output_tokens = 16400

# MAAS backend is stateless — Codex must resend the full conversation every turn
disable_response_storage = true

[model_providers.maas]
name = "MAAS AI Gateway"

# base_url WITHOUT trailing /responses — Codex appends it (→ .../v1/responses)
base_url = "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1"
env_key = "MAAS_API_KEY"
wire_api = "responses"
request_max_retries = 3
```

**Field reference:**

| Field | Purpose |
|---|---|
| `model_provider` | Key of the provider defined in `[model_providers.*]` |
| `model` | Model ID sent to MaaS |
| `model_context_window` | Declared manually because MaaS does not expose model metadata |
| `disable_response_storage` | Required for stateless backends — resends full conversation each turn |
| `base_url` | MaaS endpoint with `/v1` — Codex appends `/responses` automatically |
| `env_key` | Name of the environment variable holding the API key |
| `wire_api` | Protocol used — `responses` maps to the OpenAI Responses API |

---

## Step 4 — Set the API key and run Codex

Export the API key in your shell:

```bash
export MAAS_API_KEY="vn-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

To set it automatically on every terminal open, add it to `~/.zshrc` or `~/.bashrc`:

```bash
echo 'export MAAS_API_KEY="vn-xxxx..."' >> ~/.zshrc
source ~/.zshrc
```

Navigate to the project directory and run Codex:

```bash
codex
```

Codex displays the active provider and model in the session header:

```
model:     minimax/minimax-m2.5   /model to change
directory: ~/your-project
```

<figure><img src="../../../.gitbook/assets/Agentbase-image/use-codex-with-minimax.png" alt=""><figcaption><p>Codex running with minimax/minimax-m2.5 via GreenNode MaaS</p></figcaption></figure>

---

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `401 Unauthorized` | Wrong, missing, or inactive API key | Re-export `MAAS_API_KEY`; check key status in AI Platform Console |
| `404` on requests | Wrong `base_url` or missing `/v1` | Ensure `base_url` ends with `/v1` (no `/responses`) |
| Context truncated incorrectly | Model metadata not declared | Verify `model_context_window` and `model_max_output_tokens` in config |
| Previous context lost each turn | `disable_response_storage` not set | Add `disable_response_storage = true` to config |
| Connection timeout | Endpoint unreachable | Check VPN / connectivity to `*.api.vngcloud.vn` |

---

## Result

After completing setup, Codex CLI routes all requests through GreenNode MaaS using the Minimax model. Usage is recorded on [AI Platform Console → Usage](https://aiplatform.console.vngcloud.vn/).

| I want to... | Go to |
|---|---|
| Use OpenCode with MaaS | [Use OpenCode with GreenNode MaaS](opencode-with-maas-model.md) |
| Connect Claude Code to MaaS | [Connect Claude Code to GreenNode MaaS](connect-claude-code-to-maas.md) |
| View usage and billing | [AI Platform Console](https://aiplatform.console.vngcloud.vn/) |
