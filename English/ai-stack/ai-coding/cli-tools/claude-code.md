# Connect Claude Code to GreenNode MaaS (GLM 5.2)

> For terminal users (macOS / Linux / WSL / Windows). The Claude Code CLI will use GreenNode's **GLM 5.2** model via MaaS instead of calling Anthropic directly.

{% hint style="info" %}
**First, complete the [Prerequisites](../getting-started.md):** an **ACTIVE** key, the Base URL for your service type, and the model **ENABLED**.
{% endhint %}

---

## Pick your configuration by service type

Claude Code uses the **Anthropic standard** → the Base URL has **no** `/v1` on either service type. Only the host and the key type differ:

| Service type | Base URL | Key | Model ID |
|---|---|---|---|
| **PAYG** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | API Key from the [API Keys page](https://aiplatform.console.greennode.ai/keys) | `z-ai/glm-5.2` |
| **Token Plan** | `https://tokenplan.api.greennode.ai` | subscription-key from Plan Detail → **Subscription keys** tab | Model code on the **Models** tab (e.g. `glm-5.2`) |

{% hint style="warning" %}
**Your key and Base URL must belong to the same service type.** A PAYG API Key sent to the `tokenplan…` host (or the reverse) returns `401 Unauthorized` even while the key is still valid. You can't tell the key types apart by looking at them — go by where you got the key. See [section 2 of the Prerequisites page](../getting-started.md).
{% endhint %}

{% hint style="info" %}
**GLM 5.2 is just an example model.** GreenNode offers many models — swap in whichever one you want. On PAYG, find the Model ID on the [model detail page](https://aiplatform.console.greennode.ai/models); on Token Plan, check your plan's **Models** tab.
{% endhint %}

---

## Step 1 — Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

---

## Step 2 — Declare the Base URL & API key

Pick the tab matching your **service type** and **OS**, then copy it as-is — only replace the key value.

{% tabs %}
{% tab title="PAYG — macOS / Linux / WSL" %}
Set them temporarily for the current session:

```bash
export ANTHROPIC_BASE_URL="https://maas-llm-aiplatform-hcm.api.vngcloud.vn"
export ANTHROPIC_AUTH_TOKEN="<your-PAYG-API-key>"
```

To have this happen automatically every time you open a terminal, add the two lines above to the end of `~/.zshrc` (macOS) or `~/.bashrc` (Linux/WSL), then reload:

```bash
source ~/.zshrc      # or: source ~/.bashrc
```
{% endtab %}

{% tab title="PAYG — Windows PowerShell" %}
Set them temporarily for the current PowerShell window:

```powershell
$env:ANTHROPIC_BASE_URL = "https://maas-llm-aiplatform-hcm.api.vngcloud.vn"
$env:ANTHROPIC_AUTH_TOKEN = "<your-PAYG-API-key>"
```

To persist them for your account (run once, then **reopen PowerShell**):

```powershell
[Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "https://maas-llm-aiplatform-hcm.api.vngcloud.vn", "User")
[Environment]::SetEnvironmentVariable("ANTHROPIC_AUTH_TOKEN", "<your-PAYG-API-key>", "User")
```
{% endtab %}

{% tab title="Token Plan — macOS / Linux / WSL" %}
Set them temporarily for the current session:

```bash
export ANTHROPIC_BASE_URL="https://tokenplan.api.greennode.ai"
export ANTHROPIC_AUTH_TOKEN="<your-subscription-key>"
```

To have this happen automatically every time you open a terminal, add the two lines above to the end of `~/.zshrc` (macOS) or `~/.bashrc` (Linux/WSL), then reload:

```bash
source ~/.zshrc      # or: source ~/.bashrc
```
{% endtab %}

{% tab title="Token Plan — Windows PowerShell" %}
Set them temporarily for the current PowerShell window:

```powershell
$env:ANTHROPIC_BASE_URL = "https://tokenplan.api.greennode.ai"
$env:ANTHROPIC_AUTH_TOKEN = "<your-subscription-key>"
```

To persist them for your account (run once, then **reopen PowerShell**):

```powershell
[Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "https://tokenplan.api.greennode.ai", "User")
[Environment]::SetEnvironmentVariable("ANTHROPIC_AUTH_TOKEN", "<your-subscription-key>", "User")
```
{% endtab %}
{% endtabs %}

<figure><img src="../../../.gitbook/assets/AI-coding-change-baseurl-apikey (1).png" alt=""><figcaption><p>ANTHROPIC_AUTH_TOKEN and ANTHROPIC_BASE_URL configured in the shell profile</p></figcaption></figure>

---

## Step 3 — Run Claude Code

In your project directory, run the command for your service type:

{% tabs %}
{% tab title="PAYG" %}
```bash
claude --model z-ai/glm-5.2
```
{% endtab %}

{% tab title="Token Plan" %}
```bash
claude --model glm-5.2
```

Replace `glm-5.2` with the exact **Model code** shown on your plan's **Models** tab.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The `--model` flag sets the model for the current session. Inside Claude Code you can also switch models with the `/model` command.
{% endhint %}

---

## Step 4 — Verify

In Claude Code, type `/status` and compare:

| Check | PAYG | Token Plan |
|---|---|---|
| Base URL points to | `maas-llm-aiplatform-hcm.api.vngcloud.vn` | `tokenplan.api.greennode.ai` |
| Model | `z-ai/glm-5.2` | Your plan's Model code (e.g. `glm-5.2`) |

Then check the **[AI Platform Console](https://aiplatform.console.greennode.ai/)** to see the call logged.

<figure><img src="../../../.gitbook/assets/ai-coding/claude-code-with-glm.png" alt=""><figcaption><p>Claude Code responding successfully with the z-ai/glm-5.2 model via GreenNode MaaS</p></figcaption></figure>

---

## Troubleshooting

| Symptom | Cause | Fix |
|------------|-------------|------------|
| `401` / "Unauthorized" | Wrong or not-yet-ACTIVE key | Check `ANTHROPIC_AUTH_TOKEN`; wait for the key to become **ACTIVE** |
| `401` while the key is still valid | **Key and Base URL belong to different service types** — e.g. a PAYG API Key sent to the `tokenplan…` host | Re-check the table at the top of this page: a key from the **API Keys** page → the `maas-llm-…` host; a key from the **Subscription keys** tab → the `tokenplan…` host |
| `403 Forbidden` (Token Plan) | Model isn't included in the plan | Only call models listed on the plan's **Models** tab |
| `402 Payment Required` (Token Plan) | Plan has expired or was deleted | Buy the plan again or enable **Auto-renew** |
| `404` / "Not Found" | Wrong Base URL (extra `/v1` or trailing `/`) | Claude Code is Anthropic-standard — the Base URL has **no** `/v1` |
| Requests go straight to Anthropic | Old `ANTHROPIC_API_KEY` variable still set | Run `unset ANTHROPIC_API_KEY` (macOS/Linux) or remove that variable on Windows |
| Wrong model is used | Missing `--model` flag, or a Model ID from the other service type | Run `claude --model <model-id-for-your-service-type>` or use `/model` to switch |
| AI doesn't respond | PAYG out of credit, or Token Plan out of token quota | PAYG: top up credit. Token Plan: wait for the next cycle, buy another plan, or temporarily switch to a PAYG API Key |
| Connection timeout | Can't reach the endpoint over the network | Check VPN / network access to `*.api.vngcloud.vn` (PAYG) or `tokenplan.api.greennode.ai` (Token Plan) |

---

| I want to next... | Go to |
|------------------------|--------|
| Use OpenCode | [OpenCode](opencode.md) |
| See the prerequisites | [Getting Started with AI Coding](../getting-started.md) |
| Learn about Token Plan packages | [Token Plan](../../token-plan/README.md) |

---

## Need help?

If you've followed the steps and it's still not working, feel free to contact GreenNode Customer Support:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Help center: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Thank you for using GreenNode's services.
