# AgentBase

## Start with a real example

You want to build a customer support AI Agent: it takes questions via chat, looks up orders in a database, sends notifications through Slack, and remembers what was discussed in last week's conversation.

Sounds straightforward — but in practice you'll need to handle:

- **Where does the agent run?** Containers, servers, autoscaling, CI/CD deployments...
- **Where do credentials live?** Database passwords, Slack tokens, API keys — you can't hardcode them.
- **Can the agent call any tool it wants?** You need guardrails to prevent it from accidentally calling a data-deletion API.
- **What did the LLM cost this month?** No dashboard, no way to know when you're about to exceed budget.
- **When something breaks in production?** No centralized logs, no visibility into which requests failed.

**AgentBase handles all of this** — so you can focus entirely on your agent's logic.

---

## What is AgentBase?

**GreenNode AgentBase** is a purpose-built infrastructure platform for AI Agents — providing the full operational, security, and governance layer needed to take an agent from code to production.

![AgentBase — Architecture Overview](../../.gitbook/assets/Agentbase-image/AgentBase-Architecture.png)

AgentBase consists of the following modules:

| Module                       | Function                                                                                                          |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Agent Runtime**      | Deploy and operate agents — container lifecycle management, versioning, rollback, scaling                        |
| **Marketplace**        | Deploy pre-built agents (OpenClaw and templates) with 1 click, no code required                                   |
| **Access Control**     | Manage Agent Identity and store credentials (API Key, OAuth2) — automatically injected into the agent at runtime |
| **MCP Governance**     | Control all MCP tool calls from agents — authentication and authorization via MCP Gateway + Policy Group         |
| **Protect & Govern**   | Rate Limiting by model or API Key — prevent agents from consuming excessive resources                            |
| **Memory**             | Give agents cross-session memory — Short-Term (conversation history) and Long-Term (semantic search)             |
| **Container Registry** | Private image registry automatically created per org — stores container images for Custom Agents                 |
| **Team & Permissions** | Manage members with 4 roles (Root / Admin / Member / Viewer) and granular permission control                      |
| **Usage & Budget**     | Dashboard tracking requests, tokens, and cost by agent/model/provider; set budget limits and automated alerts     |

---

## Two ways to get started

**No code — use immediately:**
Go to the [Marketplace](marketplace/README.md), select **OpenClaw**, enter your API key and chat channel — the agent is running in minutes.

**Build your own agent:**
Package your agent as a Docker image, push it to [Container Registry](container-registry/README.md), and deploy via [Agent Runtime](agent-runtime/README.md). Add credentials in [Access Control](../agent-base/README.md), and attach an [MCP Gateway](mcp-governance/mcp-gateway/README.md) if the agent needs to call external tools.

---

## Who is it for?

| Audience                            | What AgentBase delivers                                                    |
| ----------------------------------- | -------------------------------------------------------------------------- |
| **AI Engineers / Developers** | Focus on agent logic — infra, credentials, and observability are built in |
| **Startups / Product Teams**  | Ship AI products faster.                                                   |
| **Enterprises**               | Cost control, team-based access, enterprise-grade credential security      |
