# Release Notes — GreenNode AgentBase

## May 2026

GreenNode AgentBase releases **Phase 2** with new features expanding governance, security, and integration capabilities for AI Agents:

**New Features:**

* **Marketplace:** Browse and deploy AI agents from a template library organized by category — AI Chat, Coding, Automation. Filter, view details, and deploy with one click.
  * Learn more at [Marketplace](marketplace/README.md).

* **Container Registry:** A private container image repository automatically provisioned for your organization. Push images via AgentBase Skills (recommended) or Docker CLI manually; images are used directly when creating a Runtime.
  * Learn more at [Container Registry](container-registry/README.md).

* **Rate Limit:** Control API call frequency by requests or tokens per model and API key, preventing system overload and managing costs.
  * Learn more at [Rate Limit](protect-govern/rate-limit.md).

* **MCP Governance:** Centralized control over connections between AI Agents and external services:
  * **MCP Gateway** — Centralized proxy that auto-detects protocol, enforces Policies, and supports Private mode via VPC Peering.
  * **Policy Groups** — Allow/Deny rule sets based on tool name, input, and output patterns.
  * Learn more at [MCP Governance](mcp-governance/README.md).

* **AI Coding:** Connect Claude Code CLI and OpenAI-compatible AI coding tools (OpenAI SDK, LiteLLM, Cursor...) directly to GreenNode MaaS — billed via internal credit-tokens.
  * Learn more at [AI Coding](ai-coding/README.md).

* **Usage & Budget:** Real-time dashboard tracking token consumption and costs by agent, model, API key, and time range; set monthly budget limits with automatic alerts at 80% and 100%.
  * Learn more at [Usage & Budget](usage-budget/README.md).

* **Private Networking:** VPC Peering for Agent Runtime and MCP Gateway — allowing agents to reach internal services without exposing them to the internet.
  * Learn more at [Private Networking](private-networking.md).

***

## April 2026

GreenNode releases **OpenClaw 1-Click** on AgentBase, enabling anyone to deploy a personal AI Agent powered by OpenClaw directly from the **Agent Marketplace** — no technical knowledge required, no manual setup, ready in just 40–60 seconds.

**New Features:**

* **OpenClaw 1-Click:** Deploy an OpenClaw instance directly from the Marketplace with minimal configuration.
  * **Auto-connected to GreenNode MaaS:** GreenNode users are automatically granted LLM access without manually configuring API keys. Default model: **qwen3-5-27b**.
  * **BYOK — Bring Your Own Key:** Supports bringing an API key from external providers (OpenAI, Anthropic, Gemini...).
  * **Channel integrations:** Configure Telegram and Zalo connections directly during the deploy step.
  * **My Agents:** Manage all OpenClaw instances with status filtering, stop, restart, and delete.
  * Learn more at [OpenClaw 1-Click](agent-runtime/openclaw/openclaw-1-click.md).

***

## March 2026

GreenNode AgentBase releases **Phase 1** — a purpose-built infrastructure platform for AI Agents, enabling developers to deploy and operate AI Agents on the cloud without managing servers, scaling, or credentials.

**New Features:**

* **Agent Runtime:** Deploy agents as containers with autoscaling, versioning, and zero-downtime deployment; supports Custom Agent and OpenClaw 1-Click.
* **Access Control & Team Permissions:** Manage agent identity, automatically inject credentials into containers; role-based member permissions with Service Accounts.
* **Memory Service:** Store conversation history (short-term) and extract semantic facts (long-term).
* **GreenNode MaaS Integration:** Direct connection to LLM models via an OpenAI-compatible API.
* Learn more at [GreenNode AgentBase](README.md).

***
