# Release Notes — GreenNode AI Stack

A single timeline of updates across all GreenNode AI Stack products — GreenNode AgentBase, Model as a Service, AI Gateway, AI Platform, AI Coding, and GenAI Studio.

***

## August 2026

**GreenNode MaaS — Model Catalog & Pricing Update**

To deliver a better experience, GreenNode is updating the MaaS model catalog, now organized into two groups:

* **Models self-hosted directly by GreenNode.**
* **Third-party models from officially contracted partners.**

**Transition Timeline**

| Event                                                                                      | Date            |
| -------------------------------------------------------------------------------------------- | --------------- |
| Current models are discontinued & the new catalog is published on the portal               | August 3, 2026  |
| Automatic 30-day extension — you may keep using current models until                       | September 2, 2026 |
| After this date, requests to the old models will return an error and will not be processed | From September 3, 2026 |

**What You Need to Do**

* Compare your **current models** with the [new model catalog](model-as-a-service/available-models.md). If your current model remains in the catalog, **no action is needed**. Only if it is no longer available should you review the [pricing](model-as-a-service/model-pricing-list.md) and select a suitable replacement.
* **Technical check before switching** (if a replacement is needed): replacement models may differ in model ID/endpoint and output behavior. Please test in advance and adjust your configuration and prompts to avoid disruption.
* If you need **more transition time** beyond September 2, 2026, or have a specific model requirement, please contact the GreenNode team for guidance.

**Benefits After the Transition**

* **Transparency on model source:** the portal clearly shows which models are GreenNode self-hosted and which are third-party.
* **More competitive pricing:** many models in the new catalog are priced better than before — see details in [Model Pricing List](model-as-a-service/model-pricing-list.md).
* **Comprehensive & continuously growing catalog:** covering most top-tier open-source and closed-source models (Claude, GPT,…).

{% hint style="info" %}
Need support during the transition? Contact us via email at [support@greennode.ai](mailto:support@greennode.ai), hotline **19001549**, or the [Help Center](https://helpdesk.greennode.ai/portal/en/home).
{% endhint %}

* See the new model catalog in [Available Models](model-as-a-service/available-models.md).
* See full pricing details in [Model Pricing List](model-as-a-service/model-pricing-list.md).

***

## July 2026

**GreenNode AgentBase — Security Runtime & MCP Connectors**

GreenNode AgentBase adds new security and integration capabilities for AI Agents:

**New Features:**

* **Security Runtime:** Control which clients can reach a Runtime and how incoming requests are authenticated — configure **IP Access Control** (allowed source IP CIDR ranges) and **Inbound Identity** (IAM Permissions, JWT, or No authorization) directly when creating a Runtime.
  * Learn more at [Create Runtime](agent-base/agent-runtime/create-runtime.md).

* **MCP Connectors:** Connect an agent to external services — GitHub, Slack, Microsoft 365 (M365 VNG bundle)... — in minutes via a prebuilt catalog, without building an MCP server or hand-coding OAuth.
  * Learn more at [MCP Connectors](agent-base/mcp-connectors/README.md).

***

## May 2026

**GreenNode AgentBase — Phase 2**

GreenNode AgentBase releases **Phase 2** with new features expanding governance, security, and integration capabilities for AI Agents:

**New Features:**

* **Marketplace:** Browse and deploy AI agents from a template library organized by category — AI Chat, Coding, Automation. Filter, view details, and deploy with one click.
  * Learn more at [Marketplace](agent-base/marketplace/README.md).

* **Container Registry:** A private container image repository automatically provisioned for your organization. Push images via AgentBase Skills (recommended) or Docker CLI manually; images are used directly when creating a Runtime.
  * Learn more at [Container Registry](agent-base/container-registry/README.md).

* **Rate Limit:** Control API call frequency by requests or tokens per model and API key, preventing system overload and managing costs.
  * Learn more at [Rate Limit](agent-base/protect-govern/rate-limit.md).

* **MCP Governance:** Centralized control over connections between AI Agents and external services:
  * **MCP Gateway** — Centralized proxy that auto-detects protocol, enforces Policies, and supports Private mode via VPC Peering.
  * **Policy Groups** — Allow/Deny rule sets based on tool name, input, and output patterns.
  * Learn more at [MCP Governance](agent-base/mcp-governance/README.md).

* **AI Coding:** Connect Claude Code CLI and OpenAI-compatible AI coding tools (OpenAI SDK, LiteLLM, Cursor...) directly to GreenNode MaaS — billed via internal credit-tokens.
  * Learn more at [AI Coding](ai-coding/README.md).

* **Usage & Budget:** Real-time dashboard tracking token consumption and costs by agent, model, API key, and time range; set monthly budget limits with automatic alerts at 80% and 100%.
  * Learn more at [Usage & Budget](usage-budget/README.md).

* **Private Networking:** VPC Peering for Agent Runtime and MCP Gateway — allowing agents to reach internal services without exposing them to the internet.
  * Learn more at [Private Networking](agent-base/private-networking.md).

***

## April 2026

**GreenNode AgentBase — OpenClaw 1-Click**

GreenNode releases **OpenClaw 1-Click** on AgentBase, enabling anyone to deploy a personal AI Agent powered by OpenClaw directly from the **Agent Marketplace** — no technical knowledge required, no manual setup, ready in just 40–60 seconds.

**New Features:**

* **OpenClaw 1-Click:** Deploy an OpenClaw instance directly from the Marketplace with minimal configuration.
  * **Auto-connected to GreenNode MaaS:** GreenNode users are automatically granted LLM access without manually configuring API keys. Default model: **qwen3-5-27b**.
  * **BYOK — Bring Your Own Key:** Supports bringing an API key from external providers (OpenAI, Anthropic, Gemini...).
  * **Channel integrations:** Configure Telegram and Zalo connections directly during the deploy step.
  * **My Agents:** Manage all OpenClaw instances with status filtering, stop, restart, and delete.
  * Learn more at [OpenClaw 1-Click](agent-base/agent-runtime/openclaw/openclaw-1-click.md).

***

## March 2026

**GreenNode AgentBase — Phase 1**

GreenNode AgentBase releases **Phase 1** — a purpose-built infrastructure platform for AI Agents, enabling developers to deploy and operate AI Agents on the cloud without managing servers, scaling, or credentials.

**New Features:**

* **Agent Runtime:** Deploy agents as containers with autoscaling, versioning, and zero-downtime deployment; supports Custom Agent and OpenClaw 1-Click.
* **Access Control & Team Permissions:** Manage agent identity, automatically inject credentials into containers; role-based member permissions with Service Accounts.
* **Memory Service:** Store conversation history (short-term) and extract semantic facts (long-term).
* **GreenNode MaaS Integration:** Direct connection to LLM models via an OpenAI-compatible API.
* Learn more at [GreenNode AgentBase](agent-base/README.md).
