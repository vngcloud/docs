# Usage & Budget

**Usage & Budget** helps you monitor resource consumption and control monthly spending — all within a single menu group on AgentBase.

---

## Overview

**Usage & Budget** contains two main pages:

| Page | Description | Access |
|---|---|---|
| **Usage & Cost** | Dashboard for viewing usage (requests, tokens, active agents) and cost by agent, provider, and model — with flexible filters and month-end cost projection | Root, Admin, Viewer (full org data); Member (own agents only) |
| **Budget & Alerts** | Set a monthly budget limit (VND) and configure automated alerts when spending approaches the limit | Root only |

---

## Key Features

### Usage & Cost Dashboard

A unified dashboard for org-wide usage and cost with multi-dimensional filters:

- **Global filters:** Agent (including **Others** — direct MaaS calls not routed through an agent), Provider, Model, API Key, Time Range
- **Usage tab:** Requests, Tokens, Active Agents; Requests over time chart; Token Breakdown chart; **Top Expensive Agent** table (top 10 agents by total cost, aggregated per agent)
- **Cost tab:** Total Cost, Budget Used %, Monthly Projection; Cost by Agent, by Provider, by Model; Monthly Cost Trend

### Budget & Alerts

Root sets a monthly budget limit in **VND** (fixed currency — no other currency option). When spending reaches a threshold:

- **80%:** Email alert sent to Root + yellow warning banner pinned to the **Usage tab**
- **100%:** Email alert sent + red warning banner pinned to the **Usage tab**

The budget automatically rolls over to the next month (always recurring) — no reconfiguration needed each month.

---

## Getting Started

| I want to... | Go to |
|---|---|
| View usage, cost, and month-end projection | [View Usage & Cost](view-usage-cost.md) |
| Set a budget limit and configure alerts | [Configure Budget & Alerts](budget-alert.md) |
