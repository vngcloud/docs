# Configure Remote MCP

**Remote MCP** is vServer MCP Server already hosted for you: a single endpoint, with no Python/`uv` installation, no repository to clone, and no `~/.greennode` directory on the machine. The MCP client connects over HTTP (**streamable-http**) and signs in with its own **GreenNode IAM user**.

The endpoint sits behind the **AgentBase Gateway**. The gateway handles authentication and forwards the caller's identity to the server, so every vServer call runs under the signed-in user's account, project, and permissions. Many users can share one endpoint while each user sees only their own resources.

### Prerequisites

* An **MCP client** that supports remote MCP and OAuth: Claude Code, Claude Desktop / [claude.ai](http://claude.ai), Cursor, or Visual Studio Code.
* A **GreenNode IAM user** with vServer permissions — the same account used to sign in to the [GreenNode Portal](https://console.greennode.ai).

**Authentication note**: No API token and no `client_id` / `client_secret` are required. The client runs the OAuth login in the browser and refreshes the token automatically; no secret is written to a configuration file.

### Remote MCP endpoint

> Replace `<XX>` with the actual deployment number once the endpoint is provisioned.

| Service                         | Remote MCP Server URL                                                                            | Service key |
| ------------------------------- | ------------------------------------------------------------------------------------------------ | ----------- |
| **vServer — GreenNode Compute** | `https://gw-vserver-mcp-server-<XX>.agentbase-gateway.aiplatform.vngcloud.vn/vserver_mcp_server` | `vserver`   |

This endpoint exposes the same tool set as local mode. See [MCP Tools](https://app.notion.com/p/MCP-Tools-869503ca97684ee0aacf3bf09eba56e6?pvs=21).

### Authentication

The endpoint is a full **OAuth 2.1 resource server** per the MCP specification. The client drives the complete flow:

1. The client calls the endpoint without a token and receives a **401** response with a `WWW-Authenticate` header pointing to the authorization-server metadata.
2. The client discovers that metadata, registers itself through Dynamic Client Registration, and opens the browser login page using the authorization-code flow with PKCE `S256`.
3. After sign-in, the client stores the access token and refreshes it automatically. You do not need to sign in again for every session.

Only a **Root / IAM user** is accepted by this gateway. A **service-account** token using `client_id` / `client_secret` with the client-credentials flow is rejected with `403 Access denied`. Service-account credentials are for [Configure Local MCP](https://app.notion.com/p/Configure-Local-MCP-964aa1792c884daf80c3d02e01a19a32?pvs=21) only.

### Add to an MCP client

#### Claude Code

```bash
claude mcp add --transport http vserver \\
  https://gw-vserver-mcp-server-<XX>.agentbase-gateway.aiplatform.vngcloud.vn/vserver_mcp_server

# Verify + sign in
claude mcp list
```

Run `/mcp` in Claude Code, select `vserver`, then choose **Authenticate** to open the browser sign-in flow.

#### Claude Desktop / [claude.ai](http://claude.ai)

Go to **Settings → Connectors → Add custom connector** and paste the endpoint URL. Claude opens the GreenNode sign-in page on first use.

Remote MCP does **not** use `command`, `args`, or environment variables in the way that stdio configuration does.

#### Cursor

Add a remote-style entry to `mcp.json`. Only `url` is needed; do not add authentication headers:

```json
{
  "mcpServers": {
    "vserver": {
      "url": "https://gw-vserver-mcp-server-<XX>.agentbase-gateway.aiplatform.vngcloud.vn/vserver_mcp_server"
    }
  }
}
```

See [Cursor — Model Context Protocol](https://docs.cursor.com/context/model-context-protocol).

#### Visual Studio Code

Add the same kind of remote entry to `.vscode/mcp.json`. See [Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers).

### Troubleshooting

**401 `iam_unauthenticated`**\
You are not signed in or the session has expired. Re-run the client's authentication flow — in Claude Code, use `/mcp → vserver → Authenticate`.

**403 `Access denied: you are not authorized to access this gateway`**\
The token is valid, but the principal is not authorized on the gateway. Sign in with an IAM user from an authorized account. A service-account token using `client_id` / `client_secret` does not work against the remote endpoint.

**The client never opens the sign-in page**\
The entry may be configured as the wrong type, such as stdio instead of remote, or the client may not support OAuth for remote MCP. Check that the entry contains only `url` and no `command` or `args`.

**A resource you expected is missing**\
Check the region: `HCM-3` or `HAN`. Every `list_*` tool echoes the region it queried, and each region has its own project. If the result still looks wrong, confirm that you are signed in as the correct IAM user and account.

**The agent reports that a write tool is unavailable**\
The hosted endpoint's access level is fixed by whoever deployed it — read-only or write-enabled. The client cannot add flags to change it. If the endpoint does not allow the required write operation, use [Configure Local MCP](https://app.notion.com/p/Configure-Local-MCP-964aa1792c884daf80c3d02e01a19a32?pvs=21) with `--allow-write`.
