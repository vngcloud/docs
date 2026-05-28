# View Usage & Cost

> Guide for Root, Admin, and Viewer to monitor resource consumption (MaaS and Runtime/Agent), cost breakdown, and month-end cost projection on the **Usage & Cost** dashboard.

***

## Prerequisites

* Signed in with role **Root**, **Admin**, or **Viewer** to see full org data
* Or role **Member** to see data for agents you created

***

## Open Usage & Cost

1. Go to **AgentBase** → sidebar → **Usage & Budget** → **Usage & Cost**
2. The dashboard opens on the **Usage tab** by default with Time Range = **Last 1h**

***

## Apply Filters

The global filter bar is pinned at the top of the page and applies to both the Usage and Cost tabs:

| Filter           | Description                                                                                         |
| ---------------- | --------------------------------------------------------------------------------------------------- |
| **Agent**        | Multi-select — choose specific agents or **Others** (direct MaaS calls not routed through an agent) |
| **All Provider** | Multi-select — filter by LLM provider (OpenAI, Anthropic, VNG AIP, ...)                             |
| **All Models**   | Multi-select — filter by AI model (gpt-4o, claude-sonnet-4-6, ...)                                  |
| **All API Keys** | Single select — filter by API Key                                                                   |
| **Time Range**   | Quick bar + picker panel                                                                            |

***

## Select a Time Range

**Quick bar:** Click any preset directly: **15m · 30m · 1h · 2h · 3h · 6h · 12h · 1d**

**Picker panel** (click **∨** to open):

| Tab          | How to use                                                                                            |
| ------------ | ----------------------------------------------------------------------------------------------------- |
| **Quick**    | Select a preset: Last 15 minutes through Last 6 months; Today, This week, This month, Last month, ... |
| **Relative** | Enter a custom relative range (e.g., Last 45 minutes)                                                 |
| **Absolute** | Select a specific From date and To date; validates that To ≥ From                                     |

***

## Usage Tab — View Usage Metrics

The Usage tab shows 4 KPI cards and 3 main sections:

**KPI cards:**

| Card                | Description                                                             |
| ------------------- | ----------------------------------------------------------------------- |
| **Total Requests**  | Total API calls within the filter range                                 |
| **Tokens Consumed** | Total Input Tokens + Output Tokens (including Cache)                    |
| **Active Agents**   | Number of agents with at least 1 request — Others (MaaS) is not counted |
| **Errors**          | Total number of failed requests within the filter range                 |

**Charts:**

* **Requests over time**: Line chart — X-axis grouped by hour (≤ 1 day) or by day (> 1 day); hover tooltip shows breakdown by model and total request count
* **Token Breakdown**: Doughnut chart separating Cache / Output / Input tokens — hover to see values and percentages

**Top Expensive Agent table:**

Shows the top 10 agents by total cost within the selected time range:

| Column          | Description                                         |
| --------------- | --------------------------------------------------- |
| **Agent**       | Agent name with icon                                |
| **Tokens Used** | Total tokens consumed                               |
| **Cost (VND)**  | Total cost (VND), sorted by highest cost by default |
| **Started At**  | Timestamp of the most recent session start          |

An **Others** row appears at the bottom of the table when there is MaaS usage not attached to any agent.

**Budget warning banner:**

When current month spending reaches ≥ 80% of the budget limit, a warning banner is pinned to the top of the Usage tab:

* **80–99%**: Yellow banner — "⚠️ 80% of this month's budget used. Consider reducing load or reviewing active agents." \[**View budget** link]
* **100%+**: Red banner — "⚠️ Monthly budget exceeded. Immediate action required."

***

## Cost Tab — View Cost Breakdown

Switch to the **Cost tab** for detailed cost analysis:

**KPI cards:**

| Card                   | When shown                                   |
| ---------------------- | -------------------------------------------- |
| **Total Cost**         | Always visible                               |
| **Budget Used**        | Only when Root has set a budget limit        |
| **Monthly Projection** | Always visible (after ≥ 3 days in the month) |

**Cost breakdown:**

* **Cost by Agent**: Table + chart; click an agent row → filters the entire dashboard to that agent
* **Cost by Provider**: Doughnut chart — OpenAI / Anthropic / VNG AIP with % contribution
* **Cost by Model**: Table + chart — Model Name, Provider, Total Cost, % of Total; sortable by cost descending
* **Monthly Cost Trend**: Bar/line chart — daily cost for the current month; hover tooltip shows date, total cost, and request count

***

## Role-based Visibility

| Role       | Data visible                                                                            |
| ---------- | --------------------------------------------------------------------------------------- |
| **Root**   | Full org data (all agents, providers, models, MaaS/Runtime) + access to Budget & Alerts |
| **Admin**  | Full org data — no access to Budget & Alerts                                            |
| **Viewer** | Full org data — no access to Budget & Alerts                                            |
| **Member** | Only data for agents they created; **Others** (MaaS) option is not shown                |

***

## Result

| I want to...                          | Go to                                        |
| ------------------------------------- | -------------------------------------------- |
| Set a budget limit and receive alerts | [Configure Budget & Alerts](budget-alert.md) |
| Usage & Budget overview               | [Usage & Budget](./)                         |
