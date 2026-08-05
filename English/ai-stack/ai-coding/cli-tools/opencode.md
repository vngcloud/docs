# OpenCode

> Guide to configuring [OpenCode](https://opencode.ai) — a TUI coding assistant — to call a model via GreenNode MaaS through the `@ai-sdk/openai-compatible` provider, billed via internal credit-tokens.

***

## Prerequisites

* Prepare your API key, Base URL, and model following [Getting Started with AI Coding](../getting-started.md)
* Node.js installed

> The GLM 5.2 model via OpenCode uses the **OpenAI standard** — the Base URL includes `/v1`: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1`.

{% hint style="info" %}
**Using a Token Plan (subscription package) key instead of a pay-as-you-go API key?** Use `https://tokenplan.api.greennode.ai/v1` as the Base URL instead. See [Token Plan](../../token-plan/README.md) for details.
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

## Step 2 — Get an API key from AI Platform

1. Log in to the [AI Platform Console](https://aiplatform.console.greennode.ai/)
2. Go to **API Keys** → **Create API Key**
3. Name the key (5–50 characters, lowercase letters + numbers + hyphens)
4. Copy the API key (`vn-...`) you just created

{% hint style="warning" %}
A newly created API key starts in `pending` status. Wait until status = `ACTIVE` before using it.
{% endhint %}

***

## Step 3 — Create the `opencode.json` config file

Create an `opencode.json` file at your project root:

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

**Field explanations:**

| Field                | Purpose                                                                           |
| -------------------- | --------------------------------------------------------------------------------- |
| `$schema`            | Enables autocomplete/validation in your editor                                    |
| `model`              | Default model — format `<provider-key>/<model-id>`                                |
| `provider.MAAS-chat` | Provider key — must exactly match the part before `/` in `model`                  |
| `npm`                | Adapter package — `@ai-sdk/openai-compatible` works for any OpenAI-style endpoint |
| `options.baseURL`    | MaaS endpoint, ending with `/v1`                                                  |
| `options.apiKey`     | MaaS token — use `{env:MAAS_API_KEY}` instead of hardcoding                       |
| `models`             | List of models exposed from this provider                                         |

{% hint style="warning" %}
Common mistake: setting `"model"` to a name that doesn't match a registered provider key. OpenCode splits on the first `/` to find the provider — if it doesn't match, the model won't load. Always use `MAAS-chat/openai/gpt-oss-120b`.
{% endhint %}

***

## Step 4 — Provide the API key

Since the config uses `{env:MAAS_API_KEY}`, the key isn't in the file but is read from an environment variable at runtime. There are two ways:

**Option A — Export an environment variable (recommended)**

Export the key in your shell, then run OpenCode in the same session:

```bash
export MAAS_API_KEY="vn-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
opencode
```

To do this automatically every time you open a terminal, add it to `~/.zshrc` or `~/.bashrc`:

```bash
echo 'export MAAS_API_KEY="vn-xxxx..."' >> ~/.zshrc
source ~/.zshrc
```

Or set it inline for a single run:

```bash
MAAS_API_KEY="vn-xxxx..." opencode
```

**Option B — Use a gitignored `.env` file in your project**

Create a `.env` file (add it to `.gitignore`):

```bash
export MAAS_API_KEY="vn-xxxx..."
```

Run OpenCode by loading the `.env` file first:

```bash
source .env && opencode
```

{% hint style="warning" %}
Don't hardcode your API key directly in `opencode.json` if that file gets committed. If a key has already been committed, rotate it immediately in the MAAS Console since it must be treated as leaked.
{% endhint %}

***

## Step 5 — Run OpenCode and select a model

1.  Navigate to your project directory and run:

    ```bash
    opencode
    ```

    OpenCode starts with `MAAS-chat/openai/gpt-oss-120b` as the default model.
2. Switch models within the session with the `/models` command, then choose **MAAS chat → openai/gpt-oss-120b** from the list.

<figure><img src="../../../.gitbook/assets/using-opencode-with-maas (1).png" alt=""><figcaption><p>OpenCode running with the openai/gpt-oss-120b model via GreenNode MaaS</p></figcaption></figure>

***

## Adding other MaaS models

To expose more models from the same MaaS endpoint, add entries to `models`:

```json
"models": {
  "openai/gpt-oss-120b": { "name": "openai/gpt-oss-120b" },
  "openai/gpt-oss-20b":  { "name": "openai/gpt-oss-20b" }
}
```

Then select via `/models`, or change the top-level `model` to the new `MAAS-chat/<model-id>`.

***

## Troubleshooting

| Symptom                                 | Cause                                         | Fix                                                            |
| --------------------------------------- | --------------------------------------------- | -------------------------------------------------------------- |
| `provider not found` / model won't load | `model` value doesn't match the provider key  | Use `MAAS-chat/openai/gpt-oss-120b`                            |
| `401 Unauthorized`                      | Wrong, expired, or not-yet-ACTIVE API key     | Re-export `MAAS_API_KEY`; rotate the token in the MAAS Console |
| `404` when sending a request            | Wrong Base URL or missing `/v1`               | Check `baseURL` ends with `/v1`                                |
| Connection timeout                      | Endpoint unreachable from the current network | Check VPN / connection to `*.api.vngcloud.vn`                  |
| Model errors but auth is correct        | Wrong model ID                                | Use the exact ID published by MaaS (`openai/gpt-oss-120b`)     |

***

## Result

Once done, OpenCode routes all requests through GreenNode MaaS. Usage is logged on the [AI Platform Console → Usage](https://aiplatform.console.greennode.ai/).

| I want to next...               | Go to                                                           |
| ------------------------------- | --------------------------------------------------------------- |
| Use Codex with Minimax via MaaS | [Use Codex with Minimax via GreenNode MaaS](codex-cli.md)       |
| Connect Claude Code to MaaS     | [Connect Claude Code to GreenNode MaaS](claude-code.md)         |
| View usage and billing          | [AI Platform Console](https://aiplatform.console.greennode.ai/) |

***

## Need help?

If you've followed the steps and it's still not working, feel free to contact GreenNode Customer Support:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Help center: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Thank you for using GreenNode's services.
