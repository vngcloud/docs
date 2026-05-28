# MCP Gateway

MCP Gateway gives you centralized control over all MCP tool calls from agents to external services — authentication and Policy Group enforcement — without changing agent code.

***

## Architecture

Every MCP tool call from an agent passes through the MCP Gateway (Kong OSS) before reaching an MCP Tool Server. LLM calls follow a separate path through the Sidecar LLM Proxy (auto-injected, bypasses Kong).

***

## Key Components

### Inbound Authentication

Controls how agents authenticate when calling the gateway. Three modes are supported:

* **IAM Permissions** — uses the GreenNode AI Platform IAM token
* **JSON Web Tokens (JWT)** — the agent attaches a JWT; the gateway validates it using a Discovery URL (automatically fetches and refreshes public keys) or inline JWKS. This is the default mode.
* **No authorization** — gateway is publicly accessible with no access control

The JWT claim used as the principal when enforcing Policy Group is configured via the **Principal claim** field (default `sub`).

### MCP Servers (Outbound)

Each gateway can route to multiple MCP Tool Servers. For each server, you configure:

* **MCP endpoint URL** — the URL of the MCP server
* **Outbound Auth** — how the gateway authenticates when calling out: OAuth 2.0, API Key, or No authentication
* **Mode** — `2LO (Machine to machine)` for service-to-service flows; `3LO (User federation)` when user redirect is needed (Return URL required)

Secrets (client credentials) are sourced from the **Identity** component — the gateway references the secret without storing it directly.

### Policy Group

A Policy Group is a set of rules defining which agents can call which tools under which conditions. A gateway can attach at most **1 Policy Group**.

Each MCP tool call goes through the following evaluation pipeline:

1. Validate API Key (Inbound Auth)
2. Evaluate Policy Group rules in `order` sequence
3. First match wins: **ALLOW** → forward to MCP server; **DENY** → return 403
4. No rule matches → hard-block 403

{% hint style="warning" %}
If a gateway has no Policy Group attached, **all** MCP tool calls are blocked with 403 (`No policy allows this request`). Always attach a Policy Group before agents start calling through the gateway.
{% endhint %}

`tools/list` always bypasses policy evaluation — only `tools/call` goes through it.

### Network & Compute

* **Public** — The system manages zone assignment automatically; no zone selection required
* **Private** — select VPC and Subnet; zone is inferred from the selected subnet; DNS resolution must be enabled in the VPC

Compute consists of **Flavor** (vCPU / RAM) and **Replicas** (1–10 instances) to ensure HA and throughput.

***

## MCP Gateway vs Sidecar LLM Proxy

|                        | MCP Gateway                   | Sidecar LLM Proxy                   |
| ---------------------- | ----------------------------- | ----------------------------------- |
| **Handles**            | MCP tool calls (`tools/call`) | LLM calls                           |
| **Infrastructure**     | Kong OSS, created on demand   | Auto-injected at agent creation     |
| **Endpoint**           | Configured in the portal      | `localhost:18080` (in agent config) |
| **Policy enforcement** | Yes — via Policy Group        | No                                  |

***

## Get Started

| I want to...                            | Go to                                       |
| --------------------------------------- | ------------------------------------------- |
| Create my first MCP Gateway             | [Manage MCP Gateway](manage-mcp-gateway.md) |
| Understand what MCP Governance includes | [MCP Governance](../)                       |
