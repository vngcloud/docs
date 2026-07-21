# Using MCP Servers with AI Coding

> **MCP (Model Context Protocol)** lets your AI Coding agent connect to external tools and data sources — for example, web lookups, reading/writing files, querying a database, or working with Jira, GitHub… This is how you "extend" an agent's capabilities, which is **different** from attaching a model.

{% hint style="info" %}
An easy way to tell them apart:
* **Attaching a model (GLM 5.2)** = giving the agent a **brain** to think with → see [Getting Started with AI Coding](getting-started.md).
* **Attaching an MCP server** = giving the agent extra **hands** to work with external systems (the topic of this page).

The two are independent: you can use GLM 5.2 without MCP, and vice versa.
{% endhint %}

---

## 1. What is an MCP server

An **MCP server** is a small program that gives an agent a set of "tools". When you ask the agent to do something that needs external data, the agent automatically calls the matching tool through that MCP server. There are 2 common types:

| Type | Runs where | Example |
|------|-----------|-------|
| **Local (stdio)** | Right on your machine | reading files, running commands, accessing an internal DB |
| **Remote (HTTP/SSE)** | On a remote server | enterprise connectors (Jira, GitHub, internal search) |

---

## 2. Prerequisites

* You've attached the GLM 5.2 model to your agent following [Getting Started with AI Coding](getting-started.md).
* Details of the MCP server you want to add (the run command if local; or the URL + token if remote).

---

## 3. Adding an MCP server

### On Claude Desktop (GUI)

1. Enable **Developer Mode** (same as when configuring the model): **Help → Troubleshooting → Enable Developer Mode**.
2. Go to **Developer → configure the MCP server (Local MCP)** and declare the server: name, run command (local) or URL (remote).
3. Restart the app. During your session, the agent will automatically use tools from the MCP server when needed.

### On Claude Code (CLI)

Quickly add an MCP server with:

```bash
claude mcp add <server-name> -- <server-run-command>
```

List servers you've added:

```bash
claude mcp list
```

---

## 4. Governing MCP within GreenNode

If you're rolling out MCP at an organizational scale (controlling which servers are allowed, permissions per tool, routing through a shared gateway), see AgentBase's **MCP Governance** section:

* [MCP Gateway](../agent-base/mcp-governance/mcp-gateway/README.md)
* [Policy Groups](../agent-base/mcp-governance/policy-groups/README.md)

---

## Need help?

If you've followed the steps and it's still not working, feel free to contact GreenNode Customer Support:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Help center: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Thank you for using GreenNode's services.
