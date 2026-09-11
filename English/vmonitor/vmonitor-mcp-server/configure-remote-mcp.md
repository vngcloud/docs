# Configure Remote MCP

Remote MCP is **vMonitor MCP Server hosted over HTTP** (**streamable-http**): the MCP client connects with nothing but a URL — no Python/`uv` install, no repo clone, and no `~/.greennode` on the client machine.

You host the server yourself (or your platform team does) — either directly, or behind the **AgentBase Gateway**. Behind the gateway, authentication is centralized: the gateway handles the sign-in and forwards the caller's identity to the server, so every vMonitor call runs under the signed-in user's account, project and permissions. Many users can share one endpoint and each still sees only their own resources.

### Host the server

Two ways, both from the [`greennode-mcp`](https://github.com/GreenNodeHub/greennode-mcp) repo:

**Option 1 — run with uv (HTTP transport):**

```bash
uv run vmonitor-mcp-server --transport streamable-http --host 0.0.0.0 --port 8080
```

The default bind is `127.0.0.1:8000` — set `--host 0.0.0.0` (and a port) when clients connect from other machines.

**Option 2 — Docker:**

```bash
# Build (from the repo root)
docker build -f src/vmonitor-mcp-server/Dockerfile -t vmonitor-mcp-server .

# Run (streamable-http on :8080); pass credentials via env or mounted ~/.greennode
docker run --rm -p 8080:8080 \
  -e GRN_CLIENT_ID=<id> -e GRN_CLIENT_SECRET=<secret> \
  vmonitor-mcp-server
```

Notes for either option:

* `GET /health` is always unauthenticated — use it for liveness / readiness checks.
* **Access level is set at server start**: read-only by default (**110 tools**); add `--allow-write` to register all **213 tools**. Decide deliberately — the quota-order tools spend money.
* The HTTP transport can boot with **no credentials at all** when running behind the AgentBase Gateway in passthrough mode — every request then requires a caller token.

### Authentication (HTTP transport)

Identity is resolved **per request**, with no flags:

1. The request carries an IAM bearer token in `Authorization` (the AgentBase Gateway forwards the caller's token) → **every vMonitor call runs as that caller**. A rejected user token errors out — it is never silently retried as the service account.
2. No token, but service-account credentials configured on the host (env vars or `~/.greennode`) → the shared service account is used.
3. Neither → **401** + `WWW-Authenticate: Bearer`.

Additional notes:

* **stdio (local) always requires service-account credentials**; only the HTTP transport supports the no-credentials passthrough mode.
* The server does not verify tokens itself — the vMonitor APIs are the verifier. A stale token surfaces as `500 IAM_VALIDATION_ERROR`, is treated as an auth failure, and is refreshed once.
* `--auth-debug` (or `GRN_MCP_AUTH_DEBUG=1`) enables opt-in, redacted, HTTP-only diagnostic logging of inbound auth summaries and exposes an unauthenticated `GET /whoami`. It never verifies signatures and never logs full tokens — **do not enable it in production**.

### Remote MCP endpoint

| Service                                          | Remote MCP Server URL             | Service key |
| ------------------------------------------------ | --------------------------------- | ----------- |
| **vMonitor — GreenNode observability platform**  | `<YOUR_VMONITOR_MCP_SERVER_URL>`  | `vmonitor`  |

Replace `<YOUR_VMONITOR_MCP_SERVER_URL>` with the endpoint your deployment exposes — e.g. `https://<your-host>:8080` for a direct deployment, or your AgentBase Gateway endpoint (such as `https://gw-vmonitor-mcp-server-<id>.agentbase-gateway.aiplatform.vngcloud.vn/vmonitor_mcp_server`) when fronted by the gateway.

This endpoint exposes the same tool set as local mode — see vMonitor MCP Tools. The access level (read-only / write) is fixed by whoever deployed it.

### Add to MCP client

#### Claude Code

```bash
claude mcp add --transport http vmonitor <YOUR_VMONITOR_MCP_SERVER_URL>

# Verify + sign in
claude mcp list
```

When the endpoint sits behind the AgentBase Gateway, run `/mcp` in Claude Code → select `vmonitor` → **Authenticate** to open the browser sign-in flow (OAuth 2.1, the client refreshes the token on its own).

#### Claude Desktop / claude.ai

Settings → **Connectors** → **Add custom connector** → paste the endpoint URL. Behind the AgentBase Gateway, Claude opens the GreenNode sign-in page on first use.

Remote MCP does **not** use `command` / `args` / environment variables the way stdio does.

#### Cursor

Add a remote-style entry to `mcp.json` — only `url` is needed:

```json
{
  "mcpServers": {
    "vmonitor": {
      "url": "<YOUR_VMONITOR_MCP_SERVER_URL>"
    }
  }
}
```

See [Cursor — Model Context Protocol](https://docs.cursor.com/context/model-context-protocol).

#### Visual Studio Code

Add the same kind of entry to `.vscode/mcp.json`. See [Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers).

#### Direct HTTP without the gateway

For a deployment without the AgentBase Gateway, clients that do not drive an OAuth flow can send a bearer token explicitly:

```json
{
  "mcpServers": {
    "vmonitor": {
      "type": "http",
      "url": "<YOUR_VMONITOR_MCP_SERVER_URL>",
      "headers": {
        "Authorization": "Bearer ${GREENNODE_MCP_TOKEN}"
      }
    }
  }
}
```

The token is an IAM bearer token — every call then runs as that identity.

### Troubleshooting

**401 (unauthenticated):** The caller did not bring a valid token and the host has no service-account credentials. Behind the gateway, re-run the client's authenticate flow (`/mcp` → `vmonitor` → Authenticate in Claude Code); on a direct deployment, check the `Authorization: Bearer` header.

**403 `Access denied`:** The token is valid but the principal is not authorized on the gateway. Sign in with an **IAM user** of an authorized account.

**500 `IAM_VALIDATION_ERROR`:** A stale token — the server refreshes it once; if the error persists, sign in again.

**The agent reports a tool as unavailable:** The hosted endpoint's access level is fixed at deployment (read-only / write) — the client cannot add flags. If you need a write operation the endpoint does not allow, use Configure Local MCP.

**Is the server up?** `GET /health` on the endpoint — always open, no token needed.
