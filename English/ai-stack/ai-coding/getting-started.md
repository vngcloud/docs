# Getting Started with AI Coding (Prerequisites)

> **Root page.** Read this page once to get everything ready, then pick a tool at the bottom of the page. Every tool guide assumes you've already completed the steps here.

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

## 2. Identify which service type you're on

GreenNode offers **two service types** for calling models, each with its **own host** and **own key type**. This is the step people most often get wrong when copying examples — settle it here before reading on.

| Service type | Key used to call | Where to get the key | Base URL host |
|---|---|---|---|
| **PAYG** — pay per token actually used | API Key | AI Platform → **API Keys** | `maas-llm-aiplatform-hcm.api.vngcloud.vn` |
| **Token Plan** — prepaid 30-day package with fixed quota | subscription-key | AI Platform → **Token Plan** → **My Token Plans** → open the plan → **Subscription keys** tab | `tokenplan.api.greennode.ai` |

### 2.1 — Base URL lookup table

Base URL = the **host for your service type** (table above) + **`/v1` suffix or not, depending on your tool's standard**:

| Service type | **Anthropic**-standard tools<br>(Claude Code, Claude Desktop) | **OpenAI**-standard tools<br>(Codex, OpenCode, Cursor, LiteLLM, OpenAI SDK) |
|---|---|---|
| **PAYG** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| **Token Plan** | `https://tokenplan.api.greennode.ai` | `https://tokenplan.api.greennode.ai/v1` |

{% hint style="warning" %}
**Your key and Base URL must belong to the same service type.** Sending a PAYG API Key to the `tokenplan…` host — or a subscription-key to the `maas-llm-aiplatform-hcm…` host — returns `401 Unauthorized`, even though both the key and the URL are perfectly valid on their own.

You **cannot tell the key types apart by looking at them** — go by **where you got the key**: the **API Keys** page means PAYG, a plan's **Subscription keys** tab means Token Plan.
{% endhint %}

### 2.2 — Self-check before copying any example

These three questions decide which tab you copy from on every tool page:

| # | Question | How to answer |
|---|---|---|
| 1 | Which type is my key? | From the **API Keys** page → **PAYG**. From a plan's **Subscription keys** tab → **Token Plan** |
| 2 | Which standard is my tool? | Claude Code / Claude Desktop → **Anthropic**, Base URL has **no** `/v1`. Everything else → **OpenAI**, Base URL **has** `/v1` |
| 3 | Where does the Model ID come from? | **PAYG:** the model's detail page in the [Models portal](https://aiplatform.console.greennode.ai/models) (e.g. `z-ai/glm-5.2`). **Token Plan:** the **Model code** column on the plan's **Models** tab (e.g. `glm-5.2`) |

{% hint style="info" %}
The Model ID for the same model **can differ** between the two service types. Always copy from the right source in question 3 — one wrong character gives you a `404` or a model that won't load.
{% endhint %}

---

## 3. Prerequisites checklist

| # | You need | What it is | Where to get it |
|---|--------|-------|-----------|
| 1 | **API key** | Your personal key | **PAYG:** [API Keys page](https://aiplatform.console.greennode.ai/keys) · **Token Plan:** the plan's **Subscription keys** tab |
| 2 | **Base URL** | The endpoint for your service type | Lookup table in **section 2.1** above |
| 3 | **Model ENABLED** | Make sure the model is turned on for use | **PAYG:** [Models page](https://aiplatform.console.greennode.ai/models) · **Token Plan:** the plan's **Models** tab |

Model ID used in configuration (PAYG example): **`z-ai/glm-5.2`**

{% hint style="info" %}
**GLM 5.2 here is just an example model.** GreenNode MaaS offers **many models** — swap in whichever model you want to use. On PAYG, the exact **Model ID** and **Base URL** for each model are on that model's **detail page** in the [Models portal](https://aiplatform.console.greennode.ai/models). On Token Plan, check your purchased plan's **Models** tab.
{% endhint %}

---

## 4. How to get each prerequisite

### 4.1 — Get your key

{% tabs %}
{% tab title="PAYG — API Key" %}
1. Open **[https://aiplatform.console.greennode.ai/keys](https://aiplatform.console.greennode.ai/keys)** and log in with your GreenNode account.
2. Click **Create API Key**.
3. Give it a memorable name, e.g. `ai-coding-<your-name>` (lowercase letters, numbers, hyphens; 5–50 characters).
4. Click create, then **Copy** the key that appears and paste it somewhere temporary like Notepad.

{% hint style="warning" %}
A newly created key may be in **pending** status. Wait until the status becomes **ACTIVE** before using it — refresh the page to check.
{% endhint %}
{% endtab %}

{% tab title="Token Plan — subscription-key" %}
1. Go to **API Key** → **Token Plan** → **My Token Plans** and click the **name of the plan** you bought.
2. Open the **Subscription keys** tab.
3. Copy `default-key` (created automatically when you buy the plan), or a key you created yourself.
4. Switch to the **Models** tab and copy the **Model code** of the model you want.

No plan yet? See [Buy Token Plan](../token-plan/buy-token-plan.md), or walk the whole path end-to-end with the [A-Z Guide](../token-plan/a-z-guide.md).

{% hint style="warning" %}
A subscription-key is a **secret** — anyone holding it can call models and burn your plan's quota. Don't paste it into group chats and don't commit it to Git.
{% endhint %}
{% endtab %}
{% endtabs %}

### 4.2 — Get the Base URL

Pick the right cell from the lookup table in **section 2.1** above based on your key's **service type** and your tool's **standard**:

{% tabs %}
{% tab title="PAYG" %}
```
# Anthropic-standard tools (Claude Code, Claude Desktop) — NO /v1
https://maas-llm-aiplatform-hcm.api.vngcloud.vn

# OpenAI-standard tools (Codex, OpenCode, Cursor, LiteLLM…) — WITH /v1
https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1
```

This Base URL is also shown on each **model's detail page** in the Models portal.
{% endtab %}

{% tab title="Token Plan" %}
```
# Anthropic-standard tools (Claude Code, Claude Desktop) — NO /v1
https://tokenplan.api.greennode.ai

# OpenAI-standard tools (Codex, OpenCode, Cursor, LiteLLM…) — WITH /v1
https://tokenplan.api.greennode.ai/v1
```

This Base URL appears on the plan's **Models** tab, labelled **Gateway base URL**. See [Token Plan](../token-plan/README.md) for more.
{% endtab %}
{% endtabs %}

### 4.3 — Confirm the model is enabled

{% tabs %}
{% tab title="PAYG" %}
1. Open the **[Models page](https://aiplatform.console.greennode.ai/models)** and search for the model you want (e.g. **GLM 5.2**).
2. Open that model and confirm its status is **ENABLED**.
3. Right on the **model detail page**, copy the **Model ID** and **Base URL** to fill into your tool (e.g. GLM 5.2 → Model ID `z-ai/glm-5.2`).

{% hint style="info" %}
If the model isn't ENABLED yet, contact GreenNode's AI Platform admin team to have it enabled — you can't do this step yourself.
{% endhint %}
{% endtab %}

{% tab title="Token Plan" %}
1. Open the plan's **Plan Detail** page → **Models** tab.
2. The model table lists exactly the models **included in the plan** — those are the only ones you can call.
3. Copy the **Model code** of the model you want (e.g. `glm-5.2`).

{% hint style="warning" %}
Calling a model **not included in the plan** returns `403 Forbidden`. To use another model, buy a plan that includes it or temporarily switch to a PAYG API Key.
{% endhint %}
{% endtab %}
{% endtabs %}

### 4.4 — Verify the Base URL + key pair before configuring any tool

Test it straight from your terminal. Once this works, every tool afterwards is just filling in the same two values:

{% tabs %}
{% tab title="PAYG" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/models \
  -H "Authorization: Bearer <your-PAYG-API-key>"
```
{% endtab %}

{% tab title="Token Plan" %}
```bash
curl https://tokenplan.api.greennode.ai/v1/chat/completions \
  -H "Authorization: Bearer <your-subscription-key>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "<model-code-from-Models-tab>",
    "messages": [{"role": "user", "content": "ping"}]
  }'
```
{% endtab %}
{% endtabs %}

Reading the result:

| Result | What it means | What to do |
|---|---|---|
| Valid JSON response | The URL + key pair is correct | Move on to section 5 and pick a tool |
| `401 Unauthorized` | Wrong key, key not **ACTIVE** yet, or **key and host belong to different service types** | Re-check section 2 — use the host that matches where you got the key |
| `403 Forbidden` | Model isn't included in the Token Plan | Only call models listed on the plan's **Models** tab |
| `404 Not Found` | Base URL has the wrong shape | Check the `/v1` rule for your tool's standard in section 2.1 |

✅ Once you have all 3 (an **ACTIVE** key, the Base URL for your service type, and an **ENABLED** model) and the check above passes, you're ready to pick a tool.

---

## 5. Choose the right tool

| You prefer... | OS | Use |
|--------------|--------------|----------|
| **Clicking, not comfortable typing commands yet** | macOS / Windows | GUI tools group → **Claude Desktop** *(coming soon)* |
| Typing commands in a terminal | macOS / Linux / WSL / Windows | [CLI tools group](cli-tools/README.md) → **Claude Code**, OpenCode, Codex CLI… |

{% hint style="info" %}
The **Claude Desktop app is only available for macOS and Windows.** If you use **Linux or WSL**, go with the **CLI** group (Claude Code) — same GLM 5.2 model, just a different install method.
{% endhint %}

---

## 6. Quick reference values

| Info | PAYG | Token Plan |
|---|---|---|
| Base URL (Anthropic standard) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | `https://tokenplan.api.greennode.ai` |
| Base URL (OpenAI standard) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | `https://tokenplan.api.greennode.ai/v1` |
| Key type | API Key | subscription-key |
| Get the key | [API Keys page](https://aiplatform.console.greennode.ai/keys) | Plan Detail → **Subscription keys** tab |
| Model ID | Model detail page (e.g. `z-ai/glm-5.2`) | **Models** tab → **Model code** column (e.g. `glm-5.2`) |
| List of available models | [Models page](https://aiplatform.console.greennode.ai/models) | The plan's **Models** tab |
| View usage | [AI Platform Console](https://aiplatform.console.greennode.ai/) → **Usage** & **Cost** tabs | [AI Platform Console](https://aiplatform.console.greennode.ai/) → **Usage** tab only |

---

## Need help?

If you've followed the steps and it's still not working, feel free to contact GreenNode Customer Support:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Help center: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Thank you for using GreenNode's services.
