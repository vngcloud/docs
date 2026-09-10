# Connect Codex Desktop to GreenNode MaaS (GLM 5.2)

> For **beginners** on macOS or Windows. Configure it by editing a `config.toml` file from Settings — you can ask an AI to help draft it, no need to know TOML syntax. Codex Desktop will use GreenNode's self-hosted **GLM 5.2** model.

{% hint style="info" %}
**First, complete the [Prerequisites](../getting-started.md):** an **ACTIVE** key, the Base URL for your service type, and the model **ENABLED**. This page only covers install and configuration.
{% endhint %}

---

## Pick your configuration by service type

Codex Desktop uses the **OpenAI standard** → `base_url` **includes** `/v1` on both service types. Only the host and the key type differ:

| Service type | `base_url` | Key | `model` |
|---|---|---|---|
| **PAYG** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | API Key from the [API Keys page](https://aiplatform.console.greennode.ai/keys) | `z-ai/glm-5.2` |
| **Token Plan** | `https://tokenplan.api.greennode.ai/v1` | subscription-key from Plan Detail → **Subscription keys** tab | Model code on the **Models** tab (e.g. `glm-5.2`) |

{% hint style="warning" %}
**Your key and `base_url` must belong to the same service type.** A PAYG API Key sent to the `tokenplan…` host (or the reverse) returns `401 Unauthorized` even while the key is still valid. You can't tell the key types apart by looking at them — go by where you got the key. See [section 2 of the Prerequisites page](../getting-started.md).
{% endhint %}

{% hint style="info" %}
**GLM 5.2 is just an example model.** GreenNode offers many models — swap in whichever one you want. On PAYG, find the Model ID on the [model detail page](https://aiplatform.console.greennode.ai/models); on Token Plan, check your plan's **Models** tab.
{% endhint %}

---

## Step 1 — Download and install Codex Desktop

Go to **[openai.com/index/introducing-the-codex-app](https://openai.com/index/introducing-the-codex-app/)**, download the app for your machine, and install it like any normal application.

---

## Step 2 — Open the app and sign in

Open Codex and sign in with your ChatGPT/OpenAI account.

<figure><img src="../../../.gitbook/assets/ai-coding/codex-ui-chat.png" alt=""><figcaption><p>Codex home screen after logging in</p></figcaption></figure>

---

## Step 3 — Open the config.toml file

1. Click your avatar/account name in the bottom-left corner → **Settings**.
2. In the search box on the left, type **"config.toml"**.
3. Click **Open config.toml** in the top-right of the **Custom config.toml settings** section — the file opens in your machine's default editor.

<figure><img src="../../../.gitbook/assets/ai-coding/find-config-toml-file.png" alt=""><figcaption><p>Find and open config.toml in Settings</p></figcaption></figure>

---

## Step 4 — Add the self-hosted model configuration

Append the block below to the **end** of `config.toml` (leave everything above it untouched). Copy the tab matching your service type:

{% tabs %}
{% tab title="PAYG" %}
```toml
[model_providers.vngcloud-glm]
name = "VNGCloud GLM"
base_url = "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1"
experimental_bearer_token = "<your-PAYG-API-key>"
wire_api = "responses"
stream_idle_timeout_ms = 3000000
request_max_retries = 3
supports_websockets = false

[profiles.glm]
model = "z-ai/glm-5.2"
model_provider = "vngcloud-glm"
model_context_window = 200000
model_auto_compact_token_limit = 200000
model_reasoning_effort = "medium"
model_reasoning_summary = "auto"
```
{% endtab %}

{% tab title="Token Plan" %}
```toml
[model_providers.greennode-tokenplan]
name = "GreenNode Token Plan"
base_url = "https://tokenplan.api.greennode.ai/v1"
experimental_bearer_token = "<your-subscription-key>"
wire_api = "responses"
stream_idle_timeout_ms = 3000000
request_max_retries = 3
supports_websockets = false

[profiles.glm]
model = "glm-5.2"   # replace with the Model code from your plan's Models tab
model_provider = "greennode-tokenplan"
model_context_window = 200000
model_auto_compact_token_limit = 200000
model_reasoning_effort = "medium"
model_reasoning_summary = "auto"
```

{% hint style="info" %}
`model` must match the **Model code** exactly as shown on the plan's **Models** tab, and that model must be included in the plan — calling a model outside the plan returns `403 Forbidden`.
{% endhint %}
{% endtab %}
{% endtabs %}

**Key fields explained:**

| Field | Purpose |
|---|---|
| `model_providers.<name>` | A provider name you choose — reused in `model_provider` below |
| `base_url` | The endpoint for your service type, **with** `/v1` |
| `experimental_bearer_token` | Your key, pasted directly into the file — Codex Desktop doesn't need an exported environment variable like the CLI |
| `wire_api` | Leave as `"responses"` — matches the Responses API that Codex Desktop uses |
| `stream_idle_timeout_ms` | Max wait time (ms) before the stream is treated as timed out |
| `request_max_retries` | How many times a failed request is retried |
| `supports_websockets` | Leave as `false` — MaaS doesn't support websockets yet |
| `profiles.glm` | A profile name you choose — appears in the app's model picker |
| `model` | Model ID sent upstream — PAYG uses the Models portal ID, Token Plan uses the plan's Model code |
| `model_provider` | Points back to the provider declared above |
| `model_context_window` | Declared manually because MaaS doesn't expose model metadata |
| `model_auto_compact_token_limit` | Token threshold at which Codex auto-compacts the context |
| `model_reasoning_effort` | Default reasoning level (`low` / `medium` / `high`) |
| `model_reasoning_summary` | Leave as `"auto"` — Codex decides whether to summarize reasoning |

{% hint style="warning" %}
**Don't copy Claude Code's environment-variable style config** (`export ANTHROPIC_BASE_URL=...`, `claude --model ...`) — that syntax is specific to the Claude Code CLI and does **not** work for Codex. Codex Desktop reads its config from `config.toml` using `model_providers` / `profiles` as shown above.
{% endhint %}

{% hint style="info" %}
**Not familiar with TOML syntax?** Copy your current `config.toml` contents, paste them into an AI chat (Codex, ChatGPT, Claude...) along with the Base URL / key / Model ID for **your service type**, and ask it to write the `[model_providers.*]` and `[profiles.*]` blocks in valid Codex format, then paste the result back into the file.
{% endhint %}

---

## Step 5 — Save the file and restart Codex

1. Save `config.toml`.
2. Quit Codex Desktop completely and reopen it.

---

## Step 6 — Verify

1. In the chat box, click the model selector (bottom-right, e.g. **"5.6 Terra Medium"**).
2. Find the profile you just added (e.g. **glm**) in the list and select it.
3. Try a prompt, e.g. *"Write a Python function that adds two numbers."* If it answers, you're done.
4. Check the **[AI Platform Console](https://aiplatform.console.greennode.ai/)** to see the call logged.

<figure><img src="../../../.gitbook/assets/ai-coding/done-setup-glm-into-codex.png" alt=""><figcaption><p>Configuration succeeded — chat responds and the model picker shows "Custom" instead of the default model</p></figcaption></figure>

{% hint style="warning" %}
**Note when switching between the default model and your self-hosted model:** If you pick one of Codex's default models from the model picker (UI), the app **only overwrites the `model` field** in `config.toml` — it does **not** reset `model_provider` back to the default provider (`openai`). If you then want to return to the self-hosted model, clicking through the UI can leave `model` and `model_provider` mismatched. To be safe, when switching between the default and self-hosted models, **edit `model` / `model_provider` directly in `config.toml`** (or ask an AI to do it) instead of only toggling the model picker.
{% endhint %}

---

## Troubleshooting

| Symptom | Cause | Fix |
|------------|-------------|------------|
| New profile doesn't appear in the model picker | App not restarted, or a wrong `[profiles.*]` section name | Quit and reopen Codex; re-check the TOML syntax |
| `401` / "Unauthorized" | Wrong or not-yet-ACTIVE key | Re-check the key; wait for **ACTIVE** status |
| `401` while the key is still valid | **Key and `base_url` belong to different service types** | Re-check the table at the top: a key from the **API Keys** page → the `maas-llm-…` host; a key from the **Subscription keys** tab → the `tokenplan…` host |
| `403 Forbidden` (Token Plan) | Model isn't included in the plan | Set `model` to a Model code listed on the plan's **Models** tab |
| `402 Payment Required` (Token Plan) | Plan expired or was deleted | Buy the plan again or enable **Auto-renew** |
| `404` / "Not Found" | Wrong Base URL (missing `/v1`) | Codex Desktop is OpenAI-standard — `base_url` must end with `/v1` |
| App errors on launch / can't read the config | Invalid TOML syntax (missing `"`, wrong indentation) | Ask an AI to check the block you added, or compare it against the Step 4 sample |
| AI doesn't respond even with the right model selected | PAYG out of credit, or Token Plan out of token quota | PAYG: top up credit. Token Plan: wait for the next cycle, buy another plan, or temporarily switch to a PAYG API Key |
| Self-hosted model stops working after switching via the model picker (UI) | `model` and `model_provider` in `config.toml` are mismatched — the picker only overwrites `model`, it doesn't reset `model_provider` | Reopen `config.toml`, set `model` / `model_provider` to a matching pair (see the Step 4 sample), save, and restart Codex |

---

| I want to next... | Go to |
|------------------------|--------|
| Use it from the command line | [Codex CLI](../cli-tools/codex-cli.md) |
| See the prerequisites | [Getting Started with AI Coding](../getting-started.md) |
| Learn about Token Plan packages | [Token Plan](../../token-plan/README.md) |
| View usage & billing | [AI Platform Console](https://aiplatform.console.greennode.ai/) |

---

## Need help?

If you've followed the steps and it's still not working, feel free to contact GreenNode Customer Support:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Help center: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Thank you for using GreenNode's services.
