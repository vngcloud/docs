# Connect Claude Code to GreenNode MaaS (GLM 5.2)

> For terminal users (macOS / Linux / WSL / Windows). The Claude Code CLI will use GreenNode's **GLM 5.2** model via MaaS instead of calling Anthropic directly.

{% hint style="info" %}
**First, complete the [Prerequisites](../getting-started.md):** an **ACTIVE** API key, the Base URL, and the GLM 5.2 model **ENABLED**.
{% endhint %}

| Info | Value |
|-----------|---------|
| Base URL | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` (Anthropic standard, **no** `/v1`) |
| Base URL (Token Plan / package key) | `https://tokenplan.api.greennode.ai` (**no** `/v1`) — see [Token Plan](../../token-plan/README.md) |
| API key | your key |
| Model ID | `z-ai/glm-5.2` |

{% hint style="info" %}
**GLM 5.2 is just an example model.** GreenNode offers many models — swap in whichever one you want. Each model's Model ID and Base URL are on the [model detail page](https://aiplatform.console.greennode.ai/models).
{% endhint %}

---

## Step 1 — Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

---

## Step 2 — Declare the Base URL & API key

Pick the right section for your OS.

{% tabs %}
{% tab title="macOS / Linux / WSL (bash or zsh)" %}
Set them temporarily for the current session:

```bash
export ANTHROPIC_BASE_URL="https://maas-llm-aiplatform-hcm.api.vngcloud.vn"
export ANTHROPIC_AUTH_TOKEN="--"   # replace with your API key
```

To have this happen automatically every time you open a terminal, add the two lines above to the end of `~/.zshrc` (macOS) or `~/.bashrc` (Linux/WSL), then reload:

```bash
source ~/.zshrc      # or: source ~/.bashrc
```
{% endtab %}

{% tab title="Windows PowerShell" %}
Set them temporarily for the current PowerShell window:

```powershell
$env:ANTHROPIC_BASE_URL = "https://maas-llm-aiplatform-hcm.api.vngcloud.vn"
$env:ANTHROPIC_AUTH_TOKEN = "--"   # replace with your API key
```

To persist them for your account (run once, then **reopen PowerShell**):

```powershell
[Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "https://maas-llm-aiplatform-hcm.api.vngcloud.vn", "User")
[Environment]::SetEnvironmentVariable("ANTHROPIC_AUTH_TOKEN", "--", "User")
```
{% endtab %}
{% endtabs %}

<figure><img src="../../../.gitbook/assets/AI-coding-change-baseurl-apikey (1).png" alt=""><figcaption><p>ANTHROPIC_AUTH_TOKEN and ANTHROPIC_BASE_URL configured in the shell profile</p></figcaption></figure>

---

## Step 3 — Run Claude Code with GLM 5.2

In your project directory, run:

```bash
claude --model z-ai/glm-5.2
```

{% hint style="info" %}
The `--model z-ai/glm-5.2` flag sets the model for the current session. Inside Claude Code you can also switch models with the `/model` command.
{% endhint %}

---

## Step 4 — Verify

In Claude Code, type `/status` — it's correct when:

* The Base URL points to `maas-llm-aiplatform-hcm.api.vngcloud.vn`
* The model is `z-ai/glm-5.2`

Then check the **[AI Platform Console](https://aiplatform.console.greennode.ai/)** to see the call logged.

<figure><img src="../../../.gitbook/assets/ai-coding/claude-code-with-glm.png" alt=""><figcaption><p>Claude Code responding successfully with the z-ai/glm-5.2 model via GreenNode MaaS</p></figcaption></figure>

---

## Troubleshooting

| Symptom | Cause | Fix |
|------------|-------------|------------|
| `401` / "Unauthorized" | Wrong or not-yet-ACTIVE API key | Check `ANTHROPIC_AUTH_TOKEN`; wait for the key to become **ACTIVE** |
| `404` / "Not Found" | Wrong Base URL (extra `/v1` or trailing `/`) | Should be exactly `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` |
| Requests go straight to Anthropic | Old `ANTHROPIC_API_KEY` variable still set | Run `unset ANTHROPIC_API_KEY` (macOS/Linux) or remove that variable on Windows |
| Wrong model is used | Missing `--model` flag | Run `claude --model z-ai/glm-5.2` or use `/model` to switch |
| AI doesn't respond | Out of credit, model auto-disabled | Top up credit in the AI Platform Console |
| Connection timeout | Can't reach MaaS over the network | Check VPN / network access to `*.api.vngcloud.vn` |

---

| I want to next... | Go to |
|------------------------|--------|
| Use OpenCode | [OpenCode](opencode.md) |
| See the prerequisites | [Getting Started with AI Coding](../getting-started.md) |

---

## Need help?

If you've followed the steps and it's still not working, feel free to contact GreenNode Customer Support:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Help center: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Thank you for using GreenNode's services.
