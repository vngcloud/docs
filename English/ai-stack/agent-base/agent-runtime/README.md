# Agent Runtime

Agent Runtime is the central place to deploy, operate, and control the lifecycle of all your AI Agents on GreenNode AgentBase — both Custom Agents you build yourself and OpenClaw Agents from the Marketplace, managed in a single interface.

---

## Overview

The **My Agents** page is the main screen of Agent Runtime — it displays all agents running in your organization, with a **Deploy a new Agent** button to create a new one quickly. The agent list supports two display modes: **Grid** (card view) and **List** (row table), toggled by the switch at the top right of the screen.

Agents are organized into two separate tabs:

### Custom Agent tab

Lists agents you built and deployed from your own container image. Each agent card shows:

- **Agent name** and current status
- **Flavor** — compute configuration (vCPU × RAM), e.g. `runtime-s2-general-2×4`
- **Created date** and the **version** currently running (e.g. `VERSION: V10`)
- **View Detail** button → opens the detail page to view logs, metrics, Endpoint, and manage versions

![Agent Runtime — Custom Agent tab](../../../.gitbook/assets/Agentbase-image/agent-runtime-custom-tab-list.png)

### OpenClaw tab

Lists OpenClaw agents deployed from the Marketplace. In addition to the same card information, each card also has quick actions:

- **OPEN** — opens the agent's chat interface (when `ACTIVE`)
- **START** — restarts the agent (when `STOPPED`)
- **Upgrade version** — upgrades to the latest OpenClaw release
- Edit / disable / delete icons directly on the card

![Agent Runtime — OpenClaw tab](../../../.gitbook/assets/Agentbase-image/agent-runtime-openclaw-tab-list.png)

---

## Runtime States

The two Runtime types have different state sets:

**Custom Agent:**

| State | Meaning |
|---|---|
| `ACTIVE` | Running, ready to accept requests |
| `CREATING` | Being initialized for the first time |
| `UPDATING` | Deploying a new version |
| `STARTING` | Restarting after a stop |
| `STOPPING` | In the process of stopping |
| `STOPPED` | Stopped, no compute cost |
| `DELETING` | Being deleted |
| `ERROR` | Startup failed — check logs |

**OpenClaw:**

| State | Meaning |
|---|---|
| `ACTIVE` | Running, ready to accept requests |
| `CREATING` | Being initialized for the first time |
| `STARTING` | Restarting after a stop |
| `STOPPING` | In the process of stopping |
| `STOPPED` | Stopped, no compute cost |
| `DELETING` | Being deleted |
| `DELETED` | Fully deleted |
| `ERROR` | Startup failed — check logs |

---

## Key Features

### Stop / Start Runtime

Stop a Runtime when not in use to save compute costs, then restart when needed — configuration and endpoints are preserved.

### Versioning and Rollback

Each container image update creates a new immutable **Version**. The default Endpoint automatically points to the latest version; you can create additional Endpoints pinned to specific versions for canary traffic or rollback.

### Private VPC

Deploy the Runtime inside your enterprise network — not exposed to the public internet. Configured at Runtime creation time. See [Private VPC](create-runtime.md).

### Private Container Registry

Pull images from your organization's own Container Registry. See [Container Registry](../container-registry/README.md).

---

## Getting Started

| I want to... | Go to |
|---|---|
| Create a new Runtime from a container image | [Create Runtime](create-runtime.md) |
| Stop, start, or update a Runtime | [Manage Runtime](manage-runtime.md) |
| Use an agent from the Marketplace | [Marketplace](../marketplace/README.md) |