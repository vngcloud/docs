# OpenCode

> Guide to configuring [OpenCode](https://opencode.ai) — a TUI coding assistant — to call a model via GreenNode MaaS through the `@ai-sdk/openai-compatible` provider.

***

## Prerequisites

* Prepare your key, Base URL, and model following [Getting Started with AI Coding](../getting-started.md)
* Node.js installed

***

## Pick your configuration by service type

OpenCode uses the **OpenAI standard** → `baseURL` **includes** `/v1` on both service types. Only the host and the key type differ:

| Service type | `baseURL` | Key | Model |
|---|---|---|---|
| **PAYG** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | API Key from the [API Keys page](https://aiplatform.console.greennode.ai/keys) | `openai/gpt-oss-120b` |
| **Token Plan** | `https://tokenplan.api.greennode.ai/v1` | subscription-key from Plan Detail → **Subscription keys** tab | Model code on the plan's **Models** tab |

{% hint style="warning" %}
**Your key and `baseURL` must belong to the same service type.** A PAYG API Key sent to the `tokenplan…` host (or the reverse) returns `401 Unauthorized` even while the key is still valid. Go by where you got the key — see [section 2 of the Prerequisites page](../getting-started.md).
{% endhint %}

***

## Step 1 — Install OpenCode

```bash
npm install -g opencode-ai
```

Or via Homebrew (macOS):

```bash
brew install opencode
```

***

## Step 2 — Get your key

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

No plan yet? See [Buy Token Plan](../../token-plan/buy-token-plan.md).
{% endtab %}
{% endtabs %}

***

## Step 3 — Create the `opencode.json` config file

Create `opencode.json` in your project root. Copy the tab matching your service type:

{% tabs %}
{% tab title="PAYG" %}
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
{% endtab %}

{% tab title="Token Plan" %}
```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "MAAS-chat/glm-5.2",
  "provider": {
    "MAAS-chat": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "MAAS chat",
      "options": {
        "baseURL": "https://tokenplan.api.greennode.ai/v1",
        "apiKey": "{env:MAAS_API_KEY}"
      },
      "models": {
        "glm-5.2": {
          "name": "glm-5.2"
        }
      }
    }
  }
}
```

{% hint style="info" %}
Replace `glm-5.2` (in both `model` and `models`) with the exact **Model code** from your plan's **Models** tab. Calling a model outside the plan returns `403 Forbidden`.
{% endhint %}
{% endtab %}
{% endtabs %}

**Field reference:**

| Field | Purpose |
|---|---|
| `$schema` | Enables autocomplete/validation in your editor |
| `model` | Default model — format `<provider-key>/<model-id>` |
| `provider.MAAS-chat` | Provider key — the part before `/` in `model` must match exactly |
| `npm` | Adapter package — `@ai-sdk/openai-compatible` works with any OpenAI-style endpoint |
| `options.baseURL` | The endpoint for your service type, ending in `/v1` |
| `options.apiKey` | Your MaaS key — use `{env:MAAS_API_KEY}` instead of hardcoding |
| `models` | The models exposed from this provider |

{% hint style="warning" %}
Common mistake: setting `"model"` to a name that doesn't match the registered provider key. OpenCode splits on the first `/` to find the provider — if it doesn't match, the model won't load. The `model` value must always start with `MAAS-chat/`.
{% endhint %}

***

## Step 4 — Provide the key

Because the config uses `{env:MAAS_API_KEY}`, the key isn't stored in the file — it's read from the environment at runtime. Use the key belonging to the same service type as the `baseURL` you set in Step 3.

**Option A — Export an environment variable (recommended)**

{% tabs %}
{% tab title="PAYG" %}
```bash
export MAAS_API_KEY="<your-PAYG-API-key>"
opencode
```
{% endtab %}

{% tab title="Token Plan" %}
```bash
export MAAS_API_KEY="<your-subscription-key>"
opencode
```
{% endtab %}
{% endtabs %}

To set it automatically every time you open a terminal, add it to `~/.zshrc` or `~/.bashrc`:

```bash
echo 'export MAAS_API_KEY="<your-key>"' >> ~/.zshrc
source ~/.zshrc
```

Or set it inline for a single run:

```bash
MAAS_API_KEY="<your-key>" opencode
```

**Option B — Use a gitignored `.env` file in the project**

Create a `.env` file (add it to `.gitignore`):

```bash
export MAAS_API_KEY="<your-key>"
```

Run OpenCode after loading `.env`:

```bash
source .env && opencode
```

{% hint style="warning" %}
Don't hardcode the key into `opencode.json` if that file gets committed. If a key has already been committed, rotate it right away — rotate a PAYG API Key on the [API Keys page](https://aiplatform.console.greennode.ai/keys); revoke and recreate a subscription-key on the plan's **Subscription keys** tab.
{% endhint %}

***

## Step 5 — Run OpenCode and pick a model

1. Change into your project directory and run:

   ```bash
   opencode
   ```

   OpenCode starts with the default model declared in `model` in Step 3.

2. Switch models during a session with `/models`, then choose **MAAS chat →** your model from the list.

<figure><img src="../../../.gitbook/assets/using-opencode-with-maas (1).png" alt=""><figcaption><p>OpenCode running with the openai/gpt-oss-120b model via GreenNode MaaS</p></figcaption></figure>

***

## Add more models

To expose more models from the same endpoint, add entries to `models`:

{% tabs %}
{% tab title="PAYG" %}
```json
"models": {
  "openai/gpt-oss-120b": { "name": "openai/gpt-oss-120b" },
  "openai/gpt-oss-20b":  { "name": "openai/gpt-oss-20b" }
}
```
{% endtab %}

{% tab title="Token Plan" %}
```json
"models": {
  "glm-5.2":       { "name": "glm-5.2" },
  "minimax-m2.5":  { "name": "minimax-m2.5" }
}
```

You can only add models **included in the plan** — check the plan's **Models** tab.
{% endtab %}
{% endtabs %}

Then pick one via `/models`, or change the top-level `model` to the new `MAAS-chat/<model-id>`.

***

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `provider not found` / model won't load | `model` value doesn't match the provider key | The `model` value must start with `MAAS-chat/` |
| `401 Unauthorized` | Key wrong, expired, or not yet ACTIVE | Re-export `MAAS_API_KEY`; check the key status |
| `401` while the key is still valid | **Key and `baseURL` belong to different service types** | Re-check the table at the top: a key from the **API Keys** page → the `maas-llm-…` host; a key from the **Subscription keys** tab → the `tokenplan…` host |
| `403 Forbidden` (Token Plan) | Model isn't included in the plan | Only declare models listed on the plan's **Models** tab |
| `402 Payment Required` (Token Plan) | Plan expired or was deleted | Buy the plan again or enable **Auto-renew** |
| `404` on request | Base URL wrong or missing `/v1` | OpenCode is OpenAI-standard — `baseURL` must end with `/v1` |
| Connection timeout | Endpoint unreachable from your network | Check VPN / connectivity to `*.api.vngcloud.vn` (PAYG) or `tokenplan.api.greennode.ai` (Token Plan) |
| Model errors while auth is fine | Wrong model ID | PAYG: use the ID the portal publishes. Token Plan: use the **Model code** from the **Models** tab |

***

## Result

OpenCode now routes every request through the GreenNode endpoint for your chosen service type. Usage is recorded in the [AI Platform Console → Usage](https://aiplatform.console.greennode.ai/).

| I want to next... | Go to |
|---|---|
| Use Codex with Minimax via MaaS | [Codex CLI](codex-cli.md) |
| Connect Claude Code to MaaS | [Claude Code](claude-code.md) |
| Learn about Token Plan packages | [Token Plan](../../token-plan/README.md) |
| View usage and billing | [AI Platform Console](https://aiplatform.console.greennode.ai/) |

***

## Need help?

If you've followed the steps and it's still not working, feel free to contact GreenNode Customer Support:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Help center: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Thank you for using GreenNode's services.
