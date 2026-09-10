# vMonitor MCP Server

**vMonitor MCP Server** is a [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server that gives AI assistants (Claude, Cursor, Gemini, …) a set of tools to manage the **vMonitor Platform** — GreenNode's observability service: dashboards, metric queries, alarms, infrastructure hosts, logs, notifications, quota & usage, and synthetic uptime monitors.

MCP is an open standard for supplying structured context to LLMs. Instead of clicking through the vMonitor console or calling five different vMonitor APIs, the AI assistant selects and invokes the tools that vMonitor MCP Server exposes — driven by a natural-language request.

The server covers **all five vMonitor APIs** (metric/dashboard, Log, notification, quota-usage, and synthetic/uptime) behind a **single IAM authentication** — requests are routed to the right API automatically.

Once connected, ask the AI assistant in plain language to:

* **Manage dashboards & widgets**: list, inspect, create, clone, update, delete dashboards; add / move / resize widgets; manage variables and saved views.
* **Query metrics**: explore the metric catalogue, run time-series queries, read a resource's metrics straight off its default dashboard.
* **Manage alarms**: create / update / delete metric, log and change-detection alarms; review histories and current status.
* **Monitor infrastructure hosts**: list hosts across GreenNode products (vServer, vStorage, vDB, vLB, vBackup, …), check their current metrics, pause / resume monitoring.
* **Work with logs**: search and export logs; manage log projects, pipelines, processors, archives, refills and resource log mappings.
* **Manage notifications**: create OTP-verified channels — Email, SMS, Slack, Webhook, Telegram, Teams.
* **Track quota & usage**: read usage and prices, then buy / resize quotas (quote first, order after).
* **Run synthetic tests**: manage uptime monitors and probing locations.

**Safe by default:** the server runs **read-only** — inspect only, nothing is changed. Mutating operations (create/update/delete) register only when the server starts with `--allow-write` (see Configure Local MCP). Quota-order tools spend money — every order offers a zero-cost price quote first.

### Getting started

This documentation set covers:

| Page                 | Contents                                                                                                                          |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Configure Remote MCP | **Host the server over HTTP** (uv or Docker, e.g. behind the AgentBase Gateway) and connect MCP clients with just a URL.          |
| Configure Local MCP  | Run the server locally over **stdio** — suits Claude Desktop, Cursor, Claude Code, VS Code. Setup, client config, and run flags.  |
| vMonitor MCP Tools   | All 213 tools by feature area, with access level (read / write / destructive), plus the 11 feature-guide prompts and key workflows. |

#### Which mode?

* **Local (stdio)** — run the server on your own machine, authenticating with the credentials in `~/.greennode`. The access level is yours to choose via flags (`--allow-write`). See Configure Local MCP.
* **Remote (HTTP)** — host the server yourself (or let your platform team host it) and connect with only a URL — nothing to install on the client machine. See Configure Remote MCP.

### Requirements

* An **MCP client**: Claude Desktop, Claude Code, Cursor, VS Code (Copilot MCP), or any client that speaks MCP.
* **Local (stdio)**: **Python ≥ 3.11**, [`uv`](https://docs.astral.sh/uv/), and **GreenNode credentials** — a service account's `client_id` / `client_secret` from the GreenNode IAM Portal, in `~/.greennode/credentials` (shared with greennode-cli; run `grn configure` once if you haven't).
* **Remote (HTTP)**: the host needs credentials (env vars or mounted `~/.greennode`) — or none at all when every caller brings their own token behind the AgentBase Gateway.

### Region

vMonitor is a **global service** — there is no region selection: `GRN_DEFAULT_REGION` is ignored, and every tool talks to the same vMonitor endpoints. (The VKS / vServer MCP servers, by contrast, are region-scoped.)

### Resources

* **GreenNode MCP on GitHub** — [https://github.com/GreenNodeHub/greennode-mcp](https://github.com/GreenNodeHub/greennode-mcp) (this server's source: `src/vmonitor-mcp-server`)
* **vMonitor Platform docs** — see the vMonitor Platform section of this documentation
* **Model Context Protocol** — the MCP specification: [modelcontextprotocol.io](https://modelcontextprotocol.io)
