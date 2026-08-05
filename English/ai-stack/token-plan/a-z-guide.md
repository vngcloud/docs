# A-Z Guide: Buy a Token Plan and roll it out to your team

**Who this is for:** individuals buying for themselves (B2C), and whoever holds the company's Root/Admin account and needs to give AI access to non-technical departments (B2B).

---

## 0. Understand it in 2 minutes

For an AI tool (Cursor, OpenCode, Codex, Claude Desktop…) to run on GreenNode models, you only need **2 pieces of information**:

| What you need | What it is | Analogy |
|---|---|---|
| **Base URL** | The address of the AI server | The street address of the "brain" |
| **API key** (called a **subscription-key** here) | The key that gets you in | The door key |

**Token Plan** is how you get those two on a **30-day prepaid** basis: you buy one plan, get a fixed token allowance up front, and know your monthly cost in advance — instead of paying per token actually consumed (PAYG).

```
Buy a plan  →  Plan auto-creates a subscription-key  →  Copy the key + Base URL
            →  Paste into your tool  →  Run  →  Watch usage in the portal
```

{% hint style="info" %}
Want the deeper picture — how Token Plan differs from PAYG and how it's wired together → see [Token Plan (overview)](README.md).
{% endhint %}

---

## 1. Prerequisites — check these before you start

Tick all 3 rows before moving to step 2:

| # | You need | How to check |
|---|---|---|
| 1 | **A GreenNode account** that can sign in to AI Platform | Open [aiplatform.console.greennode.ai](https://aiplatform.console.greennode.ai/) |
| 2 | **The Root or Admin role** | Only these 2 roles can buy plans. See [Roles and Permissions](../agent-base/team-permissions/roles-and-permissions.md) |
| 3 | **Enough Credits** in the account to cover the plan price | The balance is shown right on the checkout screen (**Balance**). 1 credit = 1 VND |

{% hint style="warning" %}
If you are a **Developer/Viewer**, you **cannot** buy a plan — ask a Root/Admin to buy one and issue you a subscription-key (see [Section 6](#6-manage-issue-a-key-to-each-member)).
{% endhint %}

{% hint style="info" %}
Not enough credit? Top up in the AI Platform Console before buying — the system deducts credit the moment you confirm, and does not allow buying on credit.
{% endhint %}

---

## 2. Pick a plan

**Portal path:** `AI Platform` → sidebar → **Token Plan** → **Packages**

1. The **Plan Types** appear as cards. Each card shows the price, duration, included models, and max subscription-key count at a glance.
   *Example, the **Token Plan Alpha** card: `1,080,000 VND / 30 days` — GLM 5.2 model — up to 5 keys.*
2. Click a card to open **Package Detail** and read it carefully before spending:

| Look at | To learn |
|---|---|
| **Max keys** | How many people/tools you can issue keys to |
| **Duration** | The plan cycle (usually 30 days) |
| **Tokens / Requests per cycle** | The allowance per cycle — tracked **independently per model**, with no transfer between them |
| **Included Models** | The models you can call (Model, Status, **Model code**, Provider) — remember the **Model code**, you'll need to enter it in your tool shortly |
| **Subscription Endpoint** | `https://tokenplan.api.greennode.ai/v1` — this is the **Base URL** you will use |
| **What happens when activated** | What happens right after activation |

{% hint style="warning" %}
Once purchased, a plan **cannot be swapped for a different Plan Type** and **cannot be returned on request**. If you must stop mid-cycle, use **Delete** — the unused allowance is refunded pro rata to Credits. Think it through at this step.
{% endhint %}

**Which size should you pick?** A simple rule for non-technical teams: one person using a coding assistant steadily all day consumes a fair number of tokens — if you have no data yet, buy the smallest plan for 1 cycle to measure, check the real numbers in [Section 7](#7-track-usage-per-plan), and only then buy bigger.

📎 *Full detail on the Packages screen: [Buy a Token Plan](buy-token-plan.md)*

---

## 3. Buy the plan

1. Click **Buy Now** on the card (or **Buy package** inside Package Detail).
2. The **Confirm & checkout** screen appears — fill it in and double-check:

| Field | Example | Notes |
|---|---|---|
| **Plan name** (required) | `ENG-GLM-1` | Only `a-z A-Z 0-9 _ - .`, max 50 characters. **Name it after the department/project** so filtering usage later is easy |
| **Plan price / Duration / VAT / Total** | `1,080,000 VND` / `30 days` / Included / `1,080,000 VND` | Computed from the Plan Type |
| **Auto-renew** | ON (default) | Renews at the end of each cycle — can be turned off after purchase |
| **Payment method** | Credits | 1 credit = 1 VND |
| **Balance** | Your current balance | Check that it covers the total |

3. Click **Confirm & Pay**.

{% hint style="warning" %}
Confirming **immediately deducts** the amount on the Total row. Provisioning runs in the background — the gateway endpoint and subscription-key only appear in full on Plan Detail **once provisioning finishes**. Wait a few seconds and refresh if you don't see them yet.
{% endhint %}

**Result:** the plan appears in **My Token Plans** with status `ACTIVE`, Auto-renew ON, and the system **auto-creates 1 key named `default-key`** that works right away — no need to create a key manually to get started.

📎 *Detail: [Buy a Token Plan](buy-token-plan.md)*

---

## 4. Get the API key + Base URL

**Path:** `API Key` → `Token Plan` → **My Token Plans** → click the **plan name** you just bought

The **Plan Detail** page has 2 tabs — you need information from both:

**The `Models` tab** → grab 2 things:

- The **Gateway base URL** shared by the whole plan: `https://tokenplan.api.greennode.ai/v1`
- The **Model code** of the model you want (e.g. `glm-5.2`) — copy it exactly, one wrong character breaks the call

**The `Subscription keys` tab** → grab the key:

- Copy `default-key` (or a key you created yourself in [Section 6](#6-manage-issue-a-key-to-each-member))

Jot these 3 values down:

| Information | Value |
|---|---|
| **Base URL** | `https://tokenplan.api.greennode.ai/v1` |
| **API key** | the subscription-key you just copied |
| **Model** | the model code from the Models tab (e.g. `glm-5.2`) |

{% hint style="warning" %}
A subscription-key is a **secret** — anyone holding it can call models and burn the plan's allowance. Don't paste it into group chats, don't commit it to Git. Issue a separate key per person (see [Section 6](#6-manage-issue-a-key-to-each-member)) so a leak only costs you one key.
{% endhint %}

---

## 5. Set it up in the tool running your agent

The Token Plan Subscription Endpoint follows the **OpenAI-compatible** standard. That means any tool that lets you change `base_url` in the OpenAI format will work — just enter the 3 values from Section 4 and change nothing else.

### 5.1 Tools with built-in config fields (Cursor, Continue.dev, and similar)

In the tool's Settings, fill in:

| Field | Value |
|---|---|
| **Base URL** | `https://tokenplan.api.greennode.ai/v1` |
| **API Key** | `<your subscription-key>` |
| **Model** | `<model code>` — e.g. `glm-5.2` |

### 5.2 Tools that read environment variables (CLI)

{% tabs %}
{% tab title="macOS / Linux / WSL" %}

```bash
export OPENAI_BASE_URL="https://tokenplan.api.greennode.ai/v1"
export OPENAI_API_KEY="<your subscription-key>"
```

Add those 2 lines to the end of `~/.zshrc` (macOS) or `~/.bashrc` (Linux/WSL) so you don't retype them every time, then run `source ~/.zshrc`.
{% endtab %}

{% tab title="Windows PowerShell" %}

```powershell
$env:OPENAI_BASE_URL = "https://tokenplan.api.greennode.ai/v1"
$env:OPENAI_API_KEY  = "<your subscription-key>"
```

To persist it for your account (run once, then **reopen PowerShell**):

```powershell
[Environment]::SetEnvironmentVariable("OPENAI_BASE_URL", "https://tokenplan.api.greennode.ai/v1", "User")
[Environment]::SetEnvironmentVariable("OPENAI_API_KEY", "<your subscription-key>", "User")
```

{% endtab %}
{% endtabs %}

### 5.3 Calling it from code (OpenAI SDK)

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://tokenplan.api.greennode.ai/v1",
    api_key="<your subscription-key>",
)

response = client.chat.completions.create(
    model="glm-5.2",
    messages=[{"role": "user", "content": "Hello"}],
)
print(response.choices[0].message.content)
```

### 5.4 Test the connection (30 seconds)

Paste this whole block into a terminal, replacing the 2 values in `<>`:

```bash
curl https://tokenplan.api.greennode.ai/v1/chat/completions \
  -H "Authorization: Bearer <your subscription-key>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "<model code>",
    "messages": [{"role": "user", "content": "ping"}]
  }'
```

✅ **It works when:** the JSON response contains a `choices[0].message.content` field.

### 5.5 Common errors

| Symptom | Cause | Fix |
|---|---|---|
| `401 Unauthorized` | Wrong key, key Disabled, or characters missing from the copy | Re-copy the key from the **Subscription keys** tab, check Status = `ACTIVE` |
| `403 Forbidden` | Calling a model **not included in the plan** | Only call models listed in that plan's **Models** tab |
| `402 Payment Required` | The plan has expired or was deleted | **Buy again** or turn Auto-renew back on |
| `404 Not Found` | Base URL missing `/v1` | The Base URL must end with `/v1` |
| Requests run out of tokens mid-cycle | That model's token pool hit 0 | Wait for the new cycle, buy another plan, or switch to a PAYG API Key for now |
| Response parse error | The tool appends `/v1` to the base URL itself | Try dropping `/v1` if the tool handles it for you |

📎 *Detailed configuration for specific tools (LiteLLM, Cursor, Continue.dev, Node.js SDK…): [Connect OpenAI-compatible Clients to GreenNode MaaS](../ai-coding/connect-openai-compatible-to-maas.md) — the steps stay the same, just point the Base URL and key at your Token Plan values from Section 4.*

📎 *Supported tools and how to pick the right one: [AI Coding](../ai-coding/README.md) · [Getting Started with AI Coding](../ai-coding/getting-started.md) · [CLI Tools](../ai-coding/cli-tools/README.md)*

{% hint style="warning" %}
**Claude Code / the Anthropic SDK** follow the Anthropic standard (the base URL has **no** `/v1`), which differs from the OpenAI-compatible Subscription Endpoint above. If you want to use that family of tools, see [Claude Code](../ai-coding/cli-tools/claude-code.md) and confirm the applicable Token Plan endpoint with the support team.
{% endhint %}

---

## 6. Manage: issue a key to each member

This section is for whoever holds **Root/Admin** and needs to share a plan across a team.

### 6.1 View your purchased plans & each plan's detail

**Path:** `API Key` → `Token Plan` → **My Token Plans**

The list shows: plan name, Plan Type, expiry date (**Expires**), and **Auto-renew** status.

| Status | Meaning |
|---|---|
| `ACTIVE` | The plan is running |
| `EXPIRED` | The plan expired without renewal — every key in it stops working |

Click a plan name to open **Plan Detail**:

- **General information:** Package, Price, Purchase date, Expiry date, Cycle, keys in use (e.g. `1/5 in use`), Auto-renew, and the Tokens/cycle and Requests/cycle allowances
- **`Models` tab:** Gateway base URL + the model table (Model, Model code, Enabled types, Endpoint) — everything you need to call the API
- **`Subscription keys` tab:** the keys in this plan (Name, Status, Key, Created at)
- **Actions, top right:** **Buy again** (buy another plan of the same type) and **Delete** (cancel the plan)

{% hint style="info" %}
Buying several plans in parallel gives you several **independent** plan instances — quota is **never pooled**, even across the same Plan Type. To split budget by department, buy one plan per department and name each plan after it.
{% endhint %}

### 6.2 Issue a subscription-key to each member

**The rule: one key per person / per tool.** They share the plan's allowance, but separate keys let you revoke per person and filter usage per person.

**Step 1 — Plan before you create.** The plan has a **Max keys** limit (say 5), so list who needs what first:

| Key name | Issued to | Used for |
|---|---|---|
| `default-key` | (created by the system) | Keep for testing, don't hand it out |
| `mkt-an` | An — Marketing | Cursor on a personal machine |
| `sale-binh` | Bình — Sales | Codex Desktop |
| `ops-agent-prod` | (not a person) | An automated agent running in the background |

Name them `{department}-{name}` or `{system}-{environment}` — the name alone should tell you which one to revoke.

**Step 2 — Create the key.**

1. Go to **Plan Detail** → **Subscription keys** tab → click **+ Add key**
2. Fill in **Key name** following your plan table
3. The popup shows what the key inherits from the plan: access to **every model in the plan**, the plan's **shared** token/request allowance, and **the same gateway endpoint**
4. Click **Create key**

The new key appears with status `ACTIVE` and automatically shows up on the [Access Control](../agent-base/access-control/README.md) page with `Key Type = Plan: {plan name}` — the same record, no duplicate.

**Step 3 — Hand the key to the member.** Send each person exactly 3 values:

```
Base URL : https://tokenplan.api.greennode.ai/v1
API key  : <that person's own key>
Model    : <model code>
```

Include a link to [Section 5](#5-set-it-up-in-the-tool-running-your-agent) so they can set it up themselves.

{% hint style="warning" %}
Send keys over a private channel (1-1, a password manager), **never** in a shared channel.
{% endhint %}

**Step 4 — Revoke / edit a key.** In the **Subscription keys** tab, click the **⋮** icon on the key's row → choose **Enable** / **Disable** / **Rename** / **Delete**.

| Situation | What to do |
|---|---|
| Member leaves / changes project | **Disable** (temporarily) or **Delete** (permanently) |
| Suspected key leak | **Delete** the old key → **+ Add key** to create a new one, then resend |
| Wrong name | **Rename** |
| Out of Max keys and need to add someone | **Delete** an unused key, or **Buy again** to buy another plan |

{% hint style="warning" %}
**Disable** and **Delete** take effect **immediately** — that person's tool stops being able to call models from the very next request.
{% endhint %}

### 6.3 Turn Auto-renew on/off

Click the **Auto-renew** toggle in the list or in Plan Detail. The **Turn off auto-renew?** popup spells out:

- The plan will **not** renew, but stays `ACTIVE` **until its exact expiry date**
- On the expiry date, **every** subscription-key in the plan stops working immediately
- No credit is charged now, and **no refund** is issued for turning Auto-renew off
- You can turn it back on, or **Buy again**, anytime before the plan expires

{% hint style="info" %}
With Auto-renew ON, the system renews before expiry. If credit is short, it retries — and if that still fails, the plan becomes `EXPIRED` and the whole team loses model access. **Keep enough credit on hand before the expiry date.**
{% endhint %}

### 6.4 Delete/cancel a plan

In **Plan Detail** click **Delete**, or in **My Token Plans** tick the checkbox and click the trash icon (bulk). The popup spells it out: every key is torn down **immediately**, the unused allowance is refunded **pro rata** to Credits, and the plan disappears from the list while usage history is retained for auditing.

{% hint style="warning" %}
Deleting a plan **cannot be undone**. Tell the team before you click.
{% endhint %}

📎 *Full detail for Section 6: [Manage Token Plan](manage-token-plan.md)*

---

## 7. Track usage per plan

**Path:** `AI Platform Console` → sidebar → **Usage & Budget** → **Usage & Cost** → **Usage tab**

{% hint style="info" %}
**With Token Plan you only look at the Usage tab — not the Cost tab.** The plan is **prepaid**: the cost was fixed at purchase and no extra charge accrues per request. That's why subscription-keys have **no** per-token cost breakdown like PAYG API Keys do. What matters is **how much of the allowance you already paid for has been consumed**, not how much money was spent.
{% endhint %}

### 7.1 Filtering to the right plan

1. Open the **All API Keys** dropdown on the filter bar (single select)
2. Select the **subscription-key of the plan** you want to inspect
3. Set the **Time Range** to match the plan cycle — use the **Absolute** tab in the picker panel, set From = purchase date, To = today

Every figure on the Usage tab immediately narrows to that key.

{% hint style="info" %}
The **All API Keys** filter is **single select** — one key at a time. To get a total for a plan with several keys, add the keys up manually, or compare directly against the remaining allowance already shown in **Plan Detail**.
{% endhint %}

### 7.2 Reading the Usage tab

| Metric | What it means for a Token Plan |
|---|---|
| **Tokens Consumed** | The number that matters most — total Input + Output + Cache. Compare against **Tokens/cycle** in Plan Detail to see what's left |
| **Total Requests** | Compare against **Requests/cycle** in Plan Detail |
| **Errors** | Failed requests — a sudden spike usually means a wrong key, a model outside the plan, or an exhausted allowance |
| **Requests over time** | Line chart by hour/day — shows whether usage is steady or bursty |
| **Token Breakdown** | Doughnut splitting Cache / Output / Input |

{% hint style="info" %}
The most accurate source for remaining allowance is still the plan's **Plan Detail** (Tokens/cycle, Requests/cycle). Use the Usage tab to **break it down per key** — to see who is consuming which share of the shared pool.
{% endhint %}

### 7.3 What to do with the numbers

| Question | How to answer it |
|---|---|
| Who is using the most? | Filter each member's key in turn and compare **Tokens Consumed** |
| Is the plan about to run dry? | Compare Tokens Consumed against **Tokens/cycle** in Plan Detail |
| Should next cycle be a bigger or smaller plan? | Look at total consumption over a full cycle (Time Range = Absolute, purchase date to expiry date) |
| Is anyone erroring out repeatedly? | Check the **Errors** card while filtered to that key |

📎 *Dashboard detail, the other filters, and per-role view permissions: [View Usage & Cost](../usage-budget/view-usage-cost.md)*

---

## 8. FAQ

**Several people share one plan — how is the quota split?**
It isn't. Every key in the same plan **shares one pool** of tokens/requests per model — first call, first served. For a hard split by department, buy a **separate plan** per department.

**What if tokens run out mid-cycle?**
Calls to that model pause until the new cycle. To keep going right away: buy another plan, or switch to a [PAYG API Key](../ai-coding/getting-started.md) for now.

**Do subscription-keys show up alongside PAYG API Keys?**
No. The two are entirely separate and never share a dropdown anywhere in AgentBase. Subscription-keys are also excluded from the [Rate Limit](../agent-base/protect-govern/rate-limit.md) page.

**Can I call a model outside the plan?**
No — the gateway blocks it with `403 Forbidden`. Only models in the plan's **Models** tab can be called.

**Can I switch to a different Plan Type mid-cycle?**
No. You have to **Delete** the old plan (unused allowance refunded pro rata) and buy a new one.

---

## What's next

| I want to... | Go to |
|---|---|
| Understand Token Plan vs PAYG and how it's wired | [Token Plan (overview)](README.md) |
| Detail on the Packages screen & checkout | [Buy a Token Plan](buy-token-plan.md) |
| Detail on managing plans & subscription-keys | [Manage Token Plan](manage-token-plan.md) |
| Detailed setup for each AI coding tool | [Connect OpenAI-compatible Clients to GreenNode MaaS](../ai-coding/connect-openai-compatible-to-maas.md) |
| Pick the right tool (GUI or CLI) | [Getting Started with AI Coding](../ai-coding/getting-started.md) |
| The usage dashboard (Usage tab) | [View Usage & Cost](../usage-budget/view-usage-cost.md) |
| Manage member permissions in the organization | [Roles and Permissions](../agent-base/team-permissions/roles-and-permissions.md) |

---

## Need help?

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Support center: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Thank you for using GreenNode services.
