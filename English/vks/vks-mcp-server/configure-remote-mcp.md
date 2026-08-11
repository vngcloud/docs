# Configure Remote MCP

Remote MCP is VKS MCP Server already hosted for you: **a single endpoint**, with no Python/`uv` install, no repo to clone, and no `~/.greennode` on the machine. The MCP client connects over HTTP (**streamable-http**) and signs in with its own **GreenNode IAM user**.

The endpoint sits behind the **AgentBase Gateway** — the gateway handles authentication and forwards the caller's identity to the server, so every VKS call runs under the signed-in user's account, project and permissions. Many users share one endpoint and each still sees only their own resources.

### Prerequisites

* An **MCP client** that supports remote MCP + OAuth: Claude Code, Claude Desktop / claude.ai, Cursor, Visual Studio Code.
* A **GreenNode IAM user** with VKS permissions (the same account you use to sign in to the [GreenNode Portal](https://vks.console.greennode.ai)).

> No API token and no `client_id` / `client_secret` required. The client runs the OAuth login in the browser and refreshes the token on its own — no secret ever lands in a config file.

### Remote MCP endpoint

| Service                                | Remote MCP Server URL                                                                  | Service key |
| -------------------------------------- | -------------------------------------------------------------------------------------- | ----------- |
| **VKS — GreenNode Kubernetes Service** | `https://gw-vks-mcp-server-81.agentbase-gateway.aiplatform.vngcloud.vn/vks_mcp_server` | `vks`       |

This endpoint exposes the same tool set as local mode — see MCP Tools.

### Authentication

The endpoint is a full **OAuth 2.1 resource server** per the MCP spec; the client drives the whole flow:

1. The client calls the endpoint without a token → gets a **401** plus a `WWW-Authenticate` header pointing at the authorization server metadata.
2. The client discovers that metadata, registers itself (Dynamic Client Registration), and opens the browser at the login page (authorization code + PKCE `S256`).
3. After sign-in the client keeps the access token and **refreshes it automatically** — no re-login every session.

Only a **Root / IAM user** gets through this gateway. A **service-account** token (`client_id` / `client_secret`, i.e. client-credentials) is rejected with `403 Access denied` — service-account credentials are for Configure Local MCP only.

### Add to MCP client

#### Claude Code

```bash
claude mcp add --transport http vks \
  https://gw-vks-mcp-server-81.agentbase-gateway.aiplatform.vngcloud.vn/vks_mcp_server

# Verify + sign in
claude mcp list
```

Run `/mcp` in Claude Code → select `vks` → **Authenticate** to open the browser sign-in flow.

#### Claude Desktop / claude.ai

Settings → **Connectors** → **Add custom connector** → paste the endpoint URL. Claude opens the GreenNode sign-in page on first use.

Remote MCP does **not** use `command` / `args` / environment variables the way stdio does.

#### Cursor

Add a remote-style entry to `mcp.json` — only `url` is needed, no headers:

```json
{
  "mcpServers": {
    "vks": {
      "url": "https://gw-vks-mcp-server-81.agentbase-gateway.aiplatform.vngcloud.vn/vks_mcp_server"
    }
  }
}
```

See [Cursor — Model Context Protocol](https://docs.cursor.com/context/model-context-protocol).

#### Visual Studio Code

Add the same kind of entry to `.vscode/mcp.json`. See [Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers).

### Troubleshooting

**401 `iam_unauthenticated`:** Not signed in, or the session expired. Re-run the client's authenticate flow (`/mcp` → `vks` → Authenticate in Claude Code).

**403 `Access denied: you are not authorized to access this gateway`:** The token is valid but the principal is not authorized on the gateway. Sign in with an **IAM user** of an authorized account — a service-account token (`client_id`/`client_secret`) does not work against the remote endpoint.

**The client never opens the sign-in page:** The entry is configured as the wrong type (stdio instead of remote), or the client does not support OAuth for remote MCP. Check that the entry has only `url` and no `command` / `args`.

**A cluster you expected is missing:** Check the region (`HCM-3` / `HAN`) — every `list_*` tool echoes back the region it queried. If it still looks wrong, confirm you are signed in as the right IAM user/account.

**The agent reports a tool as unavailable:** The hosted endpoint's access level is fixed by whoever deployed it (read-only / write / sensitive data); the client cannot add flags. If you need a write operation the endpoint does not allow, use Configure Local MCP.
