# Buy a Token Plan

> Guide to browsing the Packages catalog, viewing plan details, and buying a Token Plan.

---

## Prerequisites

- A GreenNode account with the **Root** or **Admin** role — only these 2 roles can buy plans
- The organization has enough **Credits** for the selected plan's price (billed in credits, 1 credit = 1 VND)

---

## Browse & view plan details

**Step 1: Open Packages**

1. Go to **AI Platform** → sidebar → **API Key** → **Token Plan** → **Packages**
2. The list shows each Plan Type as a card — for example **Token Plan Alpha**: `1,080,000 VND / 30 days`, included model (GLM 5.2), max subscription-key count (5 keys)

![Packages list](../../.gitbook/assets/Package-plan/packages-list.png)

**Step 2: View details before buying**

1. Click a Plan Type to open **Package Detail**
2. Review Max keys, Model count, Duration, the token/request allowance per cycle, the **Included Models** table (Model, Status, Model code, Provider), **What happens when activated**, and the **Subscription Endpoint** — host `tokenplan.api.greennode.ai`, with `/v1` for OpenAI-standard tools and **no** `/v1` for Anthropic-standard tools

{% hint style="warning" %}
Once purchased, a plan **cannot be swapped for a different Plan Type or returned on request**. To stop a plan mid-cycle, use **Delete** instead — the unused allowance for the current cycle is refunded pro rata to Credits (see [Manage Token Plan](manage-token-plan.md)).
{% endhint %}

---

## Buy a plan

**Step 1: Start the purchase**

1. Click **Buy Now** on the Plan Type card in the Packages list (or open Package Detail and click **Buy package**)

**Step 2: Confirm & pay**

The **Confirm & checkout** screen shows:

| Field | Example value | Notes |
|---|---|---|
| **Plan name** (required) | `ENG-GLM-1` | Letters a-z, A-Z, digits 0-9, `_`, `-`, `.` only; max 50 characters |
| **Plan price / Duration / VAT / Total** | `1,080,000 VND` / `30 days` / `Included` / `1,080,000 VND` | Computed from the selected Plan Type |
| **Auto-renew** | ON (default) | Renews automatically at the end of each cycle — can be turned off after purchase |
| **Payment method** | Credits (1 credit = 1 VND) | Deducted directly from the organization's Credits |
| **Balance** | Current Credits balance | Shown for you to check before confirming |

1. Fill in **Plan name**
2. Double-check the price against your **Balance**
3. Click **Confirm & Pay**

{% hint style="warning" %}
Confirming immediately deducts the amount shown as **Total** from the organization's Credits. Provisioning runs in the background — the gateway endpoint and subscription-key only appear fully on Plan Detail once provisioning finishes.
{% endhint %}

---

## Result

The plan appears in **My Token Plans** with status `ACTIVE`, **Auto-renew** ON, and the system auto-creates 1 default subscription-key named `default-key` with access to every model in the plan — ready to use once provisioning finishes.

---

## Integrate the subscription-key into an AI coding tool

To let an AI coding tool call the models in your plan, you need exactly **3 values**:

| Value | Where to get it |
|---|---|
| **Base URL** | The **Subscription Endpoint** in Package Detail — `https://tokenplan.api.greennode.ai/v1` for OpenAI-standard tools, `https://tokenplan.api.greennode.ai` (**no** `/v1`) for Anthropic-standard tools such as Claude Code |
| **API key** | The **Subscription keys** tab in Plan Detail — use the built-in `default-key` or one you create |
| **Model code** | The **Models** tab in Plan Detail — e.g. `glm-5.2` |

With all 3 values in hand, pick the guide for the tool you use:

| Tool | Setup guide |
|---|---|
| Not sure which tool to pick | [Getting Started with AI Coding](../ai-coding/getting-started.md) |
| Any OpenAI-compatible tool (Cursor, Continue.dev, LiteLLM, OpenAI SDK...) | [Connect OpenAI-compatible Clients to GreenNode MaaS](../ai-coding/connect-openai-compatible-to-maas.md) |
| Claude Code | [Claude Code](../ai-coding/cli-tools/claude-code.md) |
| Codex CLI | [Codex CLI](../ai-coding/cli-tools/codex-cli.md) |
| OpenCode | [OpenCode](../ai-coding/cli-tools/opencode.md) |
| Codex Desktop | [Codex Desktop](../ai-coding/gui-tools/codex-desktop.md) |
| Add an MCP Server to your tool | [Using MCP Servers with AI Coding](../ai-coding/mcp-servers.md) |

{% hint style="info" %}
The AI Coding pages are written for PAYG API Keys. With Token Plan, keep every step exactly the same and swap just 2 values: **API key** to your plan's subscription-key, and **Base URL** to the Subscription Endpoint above — in the form your tool's standard expects (`/v1` for OpenAI, no `/v1` for Anthropic).
{% endhint %}

---

## Next steps

| I want to... | Go to |
|---|---|
| Create more subscription-keys & manage the plan | [Manage Token Plan](manage-token-plan.md) |
| Walk the full path from purchase to a working tool | [A-Z Guide](a-z-guide.md) |
| See the Token Plan overview | [Token Plan](README.md) |
| Track the plan's usage | [View Usage & Cost](../usage-budget/view-usage-cost.md) |
