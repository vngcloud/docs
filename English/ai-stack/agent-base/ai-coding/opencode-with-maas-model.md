# Use OpenCode with GreenNode MaaS

> Configure [OpenCode](https://opencode.ai) — a TUI coding assistant — to call models through GreenNode MaaS via the `@ai-sdk/openai-compatible` provider, billed via internal credit-tokens.

---

## Prerequisites

- An active [AI Platform](https://aiplatform.console.vngcloud.vn/) account
- API key (`vn-...` token) with status **ACTIVE**
- Node.js installed

---

## Step 1 — Install OpenCode

```bash
npm install -g opencode-ai
```

Or via Homebrew (macOS):

```bash
brew install opencode
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

## Step 3 — Create the `opencode.json` config file

Create `opencode.json` at the project root:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "MAAS-chat/openai/gpt-oss-120b",
  "provider": {
    "MAAS-chat": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "MAAS chat",
      "options": {
        "baseURL": "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
        "apiKey": "{env:MAAS_API_KEY}"
      },
      "models": {
        "openai/gpt-oss-120b": {
          "name": "openai/gpt-oss-120b"
        }
      }
    }
  }
}
```

**Field reference:**

| Field | Purpose |
|---|---|
| `$schema` | Enables editor autocomplete and validation |
| `model` | Default model — format is `<provider-key>/<model-id>` |
| `provider.MAAS-chat` | Provider key — the part before `/` in `model` must match exactly |
| `npm` | Adapter package — `@ai-sdk/openai-compatible` works for any OpenAI-style endpoint |
| `options.baseURL` | MaaS endpoint, including the `/v1` suffix |
| `options.apiKey` | MaaS token — use `{env:MAAS_API_KEY}` instead of a hardcoded value |
| `models` | Models to expose from this provider |

{% hint style="warning" %}
Common mistake: setting `"model"` to a value that does not match a registered provider key. OpenCode resolves `model` by splitting on the first `/` and looking up the provider. If it doesn't match a `provider.*` entry, the model fails to load. Always use `MAAS-chat/openai/gpt-oss-120b`.
{% endhint %}

---

## Step 4 — Provide the API key

Because the config uses `{env:MAAS_API_KEY}`, the key is never stored in the file — OpenCode reads it from the environment variable at runtime. Two options:

**Option A — Export the environment variable (recommended)**

Export the key in your shell, then launch OpenCode in the same session:

```bash
export MAAS_API_KEY="vn-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
opencode
```

To set it automatically on every terminal open, add it to `~/.zshrc` or `~/.bashrc`:

```bash
echo 'export MAAS_API_KEY="vn-xxxx..."' >> ~/.zshrc
source ~/.zshrc
```

Or set it inline for a single run:

```bash
MAAS_API_KEY="vn-xxxx..." opencode
```

**Option B — Use a gitignored `.env` file in the project**

Create a `.env` file (add to `.gitignore`):

```bash
export MAAS_API_KEY="vn-xxxx..."
```

Source it before launching OpenCode:

```bash
source .env && opencode
```

{% hint style="warning" %}
Do not hardcode the API key directly in `opencode.json` if the file is committed to git. If a key has already been committed, rotate it immediately in the MAAS Console — once pushed, it must be treated as compromised.
{% endhint %}

---

## Step 5 — Run OpenCode and select the model

1. Navigate to the project directory and run:

   ```bash
   opencode
   ```

   OpenCode starts with `MAAS-chat/openai/gpt-oss-120b` as the active model.

2. Switch models at runtime with the `/models` command, then pick **MAAS chat → openai/gpt-oss-120b** from the list.

<figure><img src="../../../.gitbook/assets/Agentbase-image/using-opencode-with-maas.png" alt=""><figcaption><p>OpenCode running with openai/gpt-oss-120b via GreenNode MaaS</p></figcaption></figure>

---

## Adding more MaaS models

To expose additional models from the same MaaS endpoint, add entries under `models`:

```json
"models": {
  "openai/gpt-oss-120b": { "name": "openai/gpt-oss-120b" },
  "openai/gpt-oss-20b":  { "name": "openai/gpt-oss-20b" }
}
```

Then select them via `/models`, or update the top-level `model` field to `MAAS-chat/<model-id>`.

---

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `provider not found` / model won't load | `model` value doesn't match a provider key | Use `MAAS-chat/openai/gpt-oss-120b` |
| `401 Unauthorized` | Missing, expired, or inactive API key | Re-export `MAAS_API_KEY`; rotate the token in MAAS Console |
| `404` on requests | Wrong base URL or missing `/v1` | Confirm `baseURL` ends with `/v1` |
| Connection timeout | Endpoint unreachable from your network | Check VPN / connectivity to `*.api.vngcloud.vn` |
| Model returns errors but auth is fine | Incorrect model ID | Use the exact ID MaaS publishes (`openai/gpt-oss-120b`) |

---

## Result

After completing setup, OpenCode routes all requests through GreenNode MaaS. Usage is recorded on [AI Platform Console → Usage](https://aiplatform.console.vngcloud.vn/).

| I want to... | Go to |
|---|---|
| Use Codex with Minimax via MaaS | [Use Codex with Minimax via GreenNode MaaS](use-codex-with-minimax.md) |
| Connect Claude Code to MaaS | [Connect Claude Code to GreenNode MaaS](connect-claude-code-to-maas.md) |
| View usage and billing | [AI Platform Console](https://aiplatform.console.vngcloud.vn/) |
