# Token Plan

**Token Plan** helps you lock in a predictable monthly AI budget with a **30-day prepaid** subscription that has a fixed token/request allowance per model — instead of paying per token actually consumed like PAYG.

---

## Architecture

Token Plan is a subscription entirely separate from your existing PAYG API Key, accessed through a **subscription-key** and a dedicated endpoint.

```
Portal (Packages / My Token Plans)
   → Billing API (purchase, renewal)
   → Subscription Service (create/manage subscription-key, plan limits)
   → MaaS Gateway (enforce rate limit + model access per plan)
   → Model Providers
```

- **Portal:** Token Plan sits under the **API Key** group, next to **API Keys**, on **AI Platform**.
- **Subscription Endpoint:** `https://tokenplan.api.greennode.ai/v1` — OpenAI SDK compatible, separate from the GreenNode MaaS Endpoint used by PAYG API Keys.

---

## Key Components

### Packages
A catalog of plans configured by Admin/Pricing — each plan bundles a name, included models, per-model token/request limits, price, and a maximum subscription-key count. You browse, view details, and purchase directly.

### My Token Plans
The list of plans you've purchased. Each plan is an **independent plan instance** — buying multiple plans in parallel never pools quota, even across the same Plan Type or overlapping models. Each plan has its own Plan Detail page with 2 tabs: **Models** (call reference — endpoint, model code) and **Subscription keys** (the keys created in this plan).

### Subscription Key
A dedicated key for calling models within a plan's allowance, entirely separate from your PAYG API Key — it never appears in the same key-selector dropdown anywhere in AgentBase. When you buy a plan, the system auto-creates 1 default key (`default-key`); you can create more keys up to the plan's max-key limit — every key in the same plan **shares** that plan's token/request allowance, no per-key quota. A subscription-key automatically shows up on the [Access Control](../agent-base/access-control/README.md) page with Key Type = `Plan: {plan name}`, and is excluded from the [Rate Limit](../agent-base/protect-govern/rate-limit.md) page.

---

## PAYG vs Token Plan Comparison

| Criteria | PAYG | Token Plan |
|---|---|---|
| Billing model | Pay per token actually used | Fixed 30-day prepaid |
| Allowance | Unlimited — pay as you go | Fixed token/request allowance per model, tracked independently per model, shared across the plan's subscription-keys |
| Key used | API Key (PAYG) | Subscription-key |
| Endpoint | GreenNode MaaS Endpoint | Subscription Endpoint |
| Cost predictability | Hard, varies with usage | Easy — known monthly cost upfront |
| Best for | Variable usage, experimentation | Steady daily usage (e.g. a coding assistant) |

---

## Getting Started with Token Plan

| I want to... | Go to |
|---|---|
| **Brand new — walk the full path from purchase to a working tool** | [A-Z Guide](a-z-guide.md) |
| Browse & buy a Token Plan | [Buy a Token Plan](buy-token-plan.md) |
| Manage a purchased plan & its subscription-keys | [Manage Token Plan](manage-token-plan.md) |
| Use a subscription-key with an AI coding tool (Claude Code, Cursor,...) | [Connect OpenAI-compatible tools to GreenNode MaaS](../ai-coding/connect-openai-compatible-to-maas.md) |
| View overall usage & cost | [Usage & Budget](../usage-budget/README.md) |
| Manage Rate Limit | [Rate Limit](../agent-base/protect-govern/rate-limit.md) |
