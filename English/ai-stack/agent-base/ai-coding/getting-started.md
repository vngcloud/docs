# Getting Started with AI Coding (Prerequisites)

> **Root page.** Read this page once to get everything ready, then pick a tool at the bottom of the page. Every tool guide assumes you've already completed the 3 steps here.

---

## 1. Quick overview in 1 minute

To use AI Coding, you combine 2 things:

* **Agent** — the software you install on your machine to "chat" with and ask AI to do work (e.g. Claude Desktop, Claude Code…).
* **LLM (model)** — the actual AI brain that answers. Here it's **GLM 5.2**, self-hosted by GreenNode, called through GreenNode's **MaaS** system.

Your job is to **point the agent to talk to GreenNode's GLM 5.2** — by declaring 2 pieces of information: a **Base URL** and an **API key**.

{% hint style="info" %}
An easy way to remember: **Base URL** = the address of the GLM "brain". **API key** = the key that lets you in. Missing either one and you can't get in.
{% endhint %}

---

## 2. Prerequisites checklist

| # | You need | What it is | Where to get it |
|---|--------|-------|-----------|
| 1 | **API key** | Your personal key, format `--` / `vn-...` | [API Keys page](https://aiplatform.console.greennode.ai/keys) |
| 2 | **Base URL** | MaaS address: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | Fixed — copy it exactly as shown here |
| 3 | **GLM 5.2 model ENABLED** | Make sure GLM 5.2 is turned on for use | [Models page](https://aiplatform.console.greennode.ai/models) → search for **GLM 5.2** |

Model ID used in configuration (example): **`z-ai/glm-5.2`**

{% hint style="info" %}
**GLM 5.2 here is just an example model.** GreenNode self-hosts **many models** — swap in whichever model you want to use. The exact **Model ID** and **Base URL** for each model are on that model's **detail page** in the [Models portal](https://aiplatform.console.greennode.ai/models).
{% endhint %}

---

## 3. How to get each prerequisite

### 3.1 — Get your API key

1. Open **[https://aiplatform.console.greennode.ai/keys](https://aiplatform.console.greennode.ai/keys)** and log in with your GreenNode account.
2. Click **Create API Key**.
3. Give it a memorable name, e.g. `ai-coding-<your-name>` (lowercase letters, numbers, hyphens; 5–50 characters).
4. Click create, then **Copy** the key that appears and paste it somewhere temporary like Notepad.

{% hint style="warning" %}
A newly created key may be in **pending** status. Wait until the status becomes **ACTIVE** before using it — refresh the page to check.
{% endhint %}

### 3.2 — Get the Base URL

The Base URL is also shown on each **model's detail page**. For models served through MaaS, the shared address is:

```
https://maas-llm-aiplatform-hcm.api.vngcloud.vn
```

{% hint style="warning" %}
**This address differs by tool type:**
* **Anthropic**-standard tools (Claude Desktop, Claude Code): use `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` — **no** `/v1`.
* **OpenAI**-standard tools (OpenCode, Codex, Cursor…): add `/v1` at the end → `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1`.

Each tool's page will tell you which one you need.
{% endhint %}

### 3.3 — Confirm the GLM 5.2 model is enabled

1. Open the **[Models page](https://aiplatform.console.greennode.ai/models)** and search for the model you want (e.g. **GLM 5.2**).
2. Open that model and confirm its status is **ENABLED**.
3. Right on the **model detail page**, copy the **Model ID** and **Base URL** to fill into your tool (e.g. GLM 5.2 → Model ID `z-ai/glm-5.2`).

{% hint style="info" %}
If the model isn't ENABLED yet, contact GreenNode's AI Platform admin team to have it enabled — you can't do this step yourself.
{% endhint %}

✅ Once you have all 3 (an **ACTIVE** key, the Base URL, and an **ENABLED** model), you're ready to pick a tool.

---

## 4. Choose the right tool

| You prefer... | OS | Use |
|--------------|--------------|----------|
| **Clicking, not comfortable typing commands yet** | macOS / Windows | GUI tools group → **Claude Desktop** *(coming soon)* |
| Typing commands in a terminal | macOS / Linux / WSL / Windows | [CLI tools group](cli-tools/README.md) → **Claude Code**, OpenCode, Codex CLI… |

{% hint style="info" %}
The **Claude Desktop app is only available for macOS and Windows.** If you use **Linux or WSL**, go with the **CLI** group (Claude Code) — same GLM 5.2 model, just a different install method.
{% endhint %}

---

## 5. Quick reference values

| Info | Value |
|-----------|---------|
| Base URL (Anthropic standard) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` |
| Base URL (OpenAI standard) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| Model ID | See the model's detail page (e.g. GLM 5.2 → `z-ai/glm-5.2`) |
| Create / get API key | https://aiplatform.console.greennode.ai/keys |
| Check GLM 5.2 model | https://aiplatform.console.greennode.ai/models (search for GLM 5.2) |
| View usage & billing | https://aiplatform.console.greennode.ai/ |

---

## Need help?

If you've followed the steps and it's still not working, feel free to contact GreenNode Customer Support:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Help center: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Thank you for using GreenNode's services.
