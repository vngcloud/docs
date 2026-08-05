# Manage AgentBase with the GreenNode MCP

### Introduction

**AgentBase MCP** lets AI assistants (Claude Desktop, Claude Code, Cursor, Windsurf, or any MCP-compatible client) operate **GreenNode AgentBase** directly through natural language — list Runtimes, create an MCP Gateway, look up a Policy, inspect Memory — without memorizing command syntax or clicking through the Portal.

AgentBase MCP is a server built on the [Model Context Protocol](https://modelcontextprotocol.io/) standard. Repo: [https://github.com/GreenNodeHub/greennode-agentbase-mcp](https://github.com/GreenNodeHub/greennode-agentbase-mcp)

What sets it apart from a conventional MCP server: instead of exposing hundreds of tools — one per API — AgentBase MCP exposes only **3 meta-tools**: `list_servers`, `search_tools`, `execute`. The AI assistant discovers the operation it needs and then runs it, so your client's context stays small no matter how many APIs AgentBase has.

MCP is one of several ways to work with AgentBase, alongside the [Portal](README.md) and the [CLI](manage-agentbase-with-the-greennode-cli.md). Choose MCP when you want an AI assistant to look up resources, suggest configurations, and perform operations on your behalf.

{% hint style="info" %}
AgentBase MCP currently supports the **prod** environment only — the services behind `agentbase.api.vngcloud.vn`.
{% endhint %}

---

### 1. Prerequisites

You need two things before configuring any client:

| Requirement | Details |
|---|---|
| **Bearer token** | An IAM Service Account token, set in the `GREENNODE_MCP_TOKEN` environment variable. Required for both connection paths |
| **Node.js ≥ 20** | Only needed for the local (stdio) path. The HTTP path installs nothing on your machine |

The token is minted from your Service Account's **Client ID** and **Client Secret** (available under **GreenNode IAM Portal → Service Accounts**):

```bash
export GREENNODE_MCP_TOKEN=$(curl -s -X POST \
  https://iam.api.vngcloud.vn/accounts-api/v2/auth/token \
  -u "$GREENNODE_CLIENT_ID:$GREENNODE_CLIENT_SECRET" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=client_credentials" | jq -r .access_token)
```

{% hint style="warning" %}
`GREENNODE_MCP_TOKEN` is a short-lived JWT (roughly **30 minutes**) and carries real permissions over your AgentBase resources — treat it like a password. Never commit it to git or paste it into shared config. The configs below reference it through an environment variable so the value stays out of the file. When the token expires, every call returns `401` — see [5. Token rotation](#id-5-token-rotation).
{% endhint %}

---

### 2. Two ways to connect

| Path | Mechanism | Suitable clients |
|---|---|---|
| **Local stdio** | The client spawns the server as a subprocess on your machine | Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Roo Code |
| **Remote HTTP** | The client talks to the AgentBase MCP Gateway over HTTPS; nothing is installed locally | Claude.ai (web) and any client that supports Streamable HTTP |

Choose **local stdio** when you control the machine and want to experiment quickly. Choose **remote HTTP** when you cannot or do not want to run the server locally — the Gateway enforces IAM inbound auth and centralizes access logging.

---

### 3. Install the server for the local stdio path

```bash
git clone https://github.com/GreenNodeHub/greennode-agentbase-mcp.git
cd greennode-agentbase-mcp
npm install

export GREENNODE_MCP_TOKEN="<your-token>"
```

Check that the server runs — it prints a startup banner and waits for input; press `Ctrl-C` to exit:

```bash
npx tsx src/index.ts
```

The server reads the following environment variables (all have defaults, so you rarely need to change them):

| Environment variable | Default | Purpose |
|---|---|---|
| `GREENNODE_MCP_TOKEN` | — | Bearer token used to call the AgentBase services |
| `TOKEN_ENV` | `GREENNODE_MCP_TOKEN` | Rename the variable that holds the token, if you prefer a different name |
| `TRANSPORT` | `stdio` | `stdio` or `http` |
| `PORT` | `8080` | Listening port when `TRANSPORT=http` |
| `MAX_RESPONSE_BYTES` | `25000` | Response truncation threshold, so large payloads don't flood the client's context |
| `SEARCH_LIMIT_DEFAULT` | `5` | Default number of results returned by `search_tools` |

{% hint style="info" %}
The stdio path requires cloning the repo because the server loads a bundled operation registry (`registry.generated.json`) at startup, and that file ships with the source. The HTTP endpoint already has the registry baked into its image, so no clone is needed.
{% endhint %}

---

### 4. Connect an MCP client

#### Claude Desktop

Open (or create) the MCP config file:

* macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
* Windows: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "agentbase": {
      "command": "npx",
      "args": ["tsx", "/ABSOLUTE/PATH/TO/greennode-agentbase-mcp/src/index.ts"],
      "cwd": "/ABSOLUTE/PATH/TO/greennode-agentbase-mcp",
      "env": {
        "GREENNODE_MCP_TOKEN": "<your-token>"
      }
    }
  }
}
```

Quit Claude Desktop fully (not just close the window) and relaunch. In a new chat, `agentbase` appears in the list of connected MCP servers.

{% hint style="warning" %}
Claude Desktop launches from a different working directory than your shell, so `args` and `cwd` must be **absolute paths**. With relative paths the server will not start.
{% endhint %}

#### Claude Code

The quickest way — run this in the repo directory:

```bash
claude mcp add agentbase \
  -e GREENNODE_MCP_TOKEN="<your-token>" \
  -- npx tsx src/index.ts
```

Or add the entry directly to `~/.claude.json`:

```json
{
  "mcpServers": {
    "agentbase": {
      "type": "stdio",
      "command": "npx",
      "args": ["tsx", "src/index.ts"],
      "cwd": "/ABSOLUTE/PATH/TO/greennode-agentbase-mcp",
      "env": {
        "GREENNODE_MCP_TOKEN": "<your-token>"
      }
    }
  }
}
```

Restart Claude Code, then run `/mcp` in a session to confirm `agentbase` is connected with 3 tools.

#### Cursor and Windsurf

Both use the same config as Claude Desktop; only the file location differs:

* Cursor: **Settings → Cursor Settings → MCP → Add new MCP server**, or edit `~/.cursor/mcp.json`
* Windsurf: **Settings → MCP Servers**, or edit `~/.codeium/windsurf/mcp_config.json`

#### Cline and Roo Code

* Cline: open the Cline panel → **MCP** icon → **Edit MCP Settings** (`~/.cline/mcp_settings.json`)
* Roo Code: **Settings → MCP Servers → Edit** (`~/.roo/mcp_settings.json`)

Same config as above, plus two extension-specific fields:

```json
{
  "mcpServers": {
    "agentbase": {
      "command": "npx",
      "args": ["tsx", "/ABSOLUTE/PATH/TO/greennode-agentbase-mcp/src/index.ts"],
      "cwd": "/ABSOLUTE/PATH/TO/greennode-agentbase-mcp",
      "env": {
        "GREENNODE_MCP_TOKEN": "<your-token>"
      },
      "disabled": false,
      "alwaysAllow": []
    }
  }
}
```

The `alwaysAllow` array pre-approves tool names so the extension does not prompt on every call. Add `"list_servers"` and `"search_tools"` for read-heavy workflows, but keep `"execute"` prompted since that tool changes real resources.

#### Claude.ai and other HTTP clients

No clone required. Add an HTTP MCP server pointing at the Gateway endpoint, with an `Authorization` header:

```json
{
  "mcpServers": {
    "agentbase": {
      "type": "http",
      "url": "https://<agentbase-mcp-gateway-endpoint>/agentbase_mcp/mcp",
      "headers": {
        "Authorization": "Bearer ${GREENNODE_MCP_TOKEN}"
      }
    }
  }
}
```

For Claude.ai on the web, go to **Settings → Connectors → Add custom connector** and supply the URL and the Bearer header. The connector runs server-side, so your token is stored with Anthropic — use a token scoped for this purpose if that matters to you.

{% hint style="info" %}
The Gateway endpoint is issued once the feature is enabled for your project. Contact [support@greennode.ai](mailto:support@greennode.ai) to get the exact endpoint.
{% endhint %}

---

### 5. Token rotation

stdio clients read the token **at spawn time** and hold it static, so a long-running server can outlive its token. The repo ships `scripts/mcp-launch.sh` — it mints a fresh token and then `exec`s the server, so every client spawn rotates the token automatically. Point your client at the script instead of `npx tsx`:

```json
"command": "bash",
"args": ["/ABSOLUTE/PATH/TO/greennode-agentbase-mcp/scripts/mcp-launch.sh"]
```

The script needs `GREENNODE_CLIENT_ID` and `GREENNODE_CLIENT_SECRET` in the environment. Each client has its own way of forcing a respawn:

| Client | How to respawn the server |
|---|---|
| Claude Desktop | Quit the app fully and relaunch |
| Claude Code | Run `/mcp` and reconnect the `agentbase` server |
| Cursor / Windsurf | Click **Restart** next to the `agentbase` server in the MCP panel |
| Cline / Roo Code | Restart the `agentbase` server in the extension's MCP panel |
| Claude.ai (HTTP) | Cannot self-rotate — mint a new token and update the connector |

If you only have a static token and no Client Secret on the machine, skip the script and re-export `GREENNODE_MCP_TOKEN` before respawning the client.

---

### 6. The three meta-tools

Every interaction follows the same three steps: `list_servers` (orient) → `search_tools` (discover) → `execute` (run).

| Tool | Parameters | Purpose |
|---|---|---|
| `list_servers` | — | List the available AgentBase services with operation counts and tags. Call this first to orient |
| `search_tools` | `query`, `server` (optional), `limit` (max 25) | Search for an operation by intent in natural language. Returns matches with their full input schema inline, ready to pass to `execute` |
| `execute` | `id`, `args`, `fields` (optional) | Run an operation by the `id` returned from `search_tools`. `fields` is a JMESPath expression that projects the response to reduce its size |

`list_servers` returns 6 services:

| Service | Scope |
|---|---|
| `runtime` | The Runtime that runs the agent code, endpoints, logs, metrics, traces |
| `gateway` | MCP Gateway, Inbound Auth, access logs, private networking |
| `identity` | Workload Identity and Outbound Auth |
| `memory` | Memory containers, strategies, sessions, events, records |
| `policy` | Policy Groups, policies and decisions |
| `cr` | Repositories, images and artifacts on vCR |

{% hint style="warning" %}
Always take the `id` from the `search_tools` results — never guess it. Operation ids mirror the `operationId` in the upstream OpenAPI spec, so they are not always pretty (`runtime.list_1`, `runtime.get`, `runtime.listEndpoints`…) and can shift between spec versions.
{% endhint %}

---

### Quick example: ask the AI assistant to deploy an agent

Once connected, just ask the AI assistant in natural language:

```
List the Agent Runtimes running in my project,
then tell me which one used the most CPU in the last hour.
```

The AI assistant calls `list_servers` to identify the `runtime` service, calls `search_tools` with the query "list agent runtimes" to get the operation id and input schema, then calls `execute` to run it — asking you for any missing required information along the way.

If you're building an agent in code rather than using a chat client, connect with the official MCP SDK and follow the same three-step pattern:

```typescript
const { tools } = await client.listTools();
console.log(tools.map(t => t.name));   // ["list_servers","search_tools","execute"]

const search = await client.callTool({
  name: "search_tools",
  arguments: { query: "list agent runtimes", limit: 5 },
});

const result = await client.callTool({
  name: "execute",
  arguments: { id: "runtime.list_1", args: {} },
});
```

---

If you run into any issues, contact GreenNode via email: [**support@greennode.ai**](mailto:support@greennode.ai) - hotline: **19001549**. Support center: [https://helpdesk.greennode.ai](https://helpdesk.greennode.ai)
