# Configure Local MCP

**Local MCP** runs **vMonitor MCP Server** as a process on your own machine, connecting the MCP client to vMonitor over **stdio**. The server authenticates with the credentials in `~/.greennode` (shared with greennode-cli) to reach the vMonitor APIs.

Choose local when you need to set the access level yourself via flags (`--allow-write`) or to run under service-account credentials. If the server is already hosted over HTTP for you, see Configure Remote MCP.

### Requirements

* **Python ≥ 3.11**.
* [`uv`](https://docs.astral.sh/uv/) — environment management and Python execution.
* The [`greennode-mcp`](https://github.com/GreenNodeHub/greennode-mcp) repo cloned locally (the client points `--directory` at it; `uv run` installs dependencies on first run).
* An **MCP client**: Claude Desktop, Claude Code, Cursor, or VS Code (Copilot MCP).
* **GreenNode credentials** — two ways to provide them:
  * Files `~/.greennode/credentials` + `~/.greennode/config`: install greennode-cli, then run `grn configure`. A service account's `client_id` / `client_secret` from the GreenNode IAM Portal is all that is required.
  * Environment variables `GRN_CLIENT_ID` / `GRN_CLIENT_SECRET` (+ `GRN_PROJECT_ID`) — no files needed, and they always override files when both exist.

> ⚠️ **Security**: never commit `client_secret` to Git. The server keeps tokens in memory only — never written to disk, never logged.

### Configuration

Credentials are read from `~/.greennode/credentials` + `~/.greennode/config` (INI format, shared with greennode-cli). Environment variables override the files (highest priority):

| Variable            | Effect                                                          |
| ------------------- | --------------------------------------------------------------- |
| `GRN_CLIENT_ID`     | Override `client_id`                                            |
| `GRN_CLIENT_SECRET` | Override `client_secret`                                        |
| `GRN_PROFILE`       | Select a profile (default: `default`)                           |
| `GRN_PROJECT_ID`    | Override `project_id`                                           |

vMonitor is a **global service** — this server takes no region setting: `GRN_DEFAULT_REGION` is ignored even when set.

### Add to MCP client

With **stdio** the MCP client spawns the server itself from the `command` / `args` in its config — there is no server to start by hand. **Read-only** is the default; add flags to `args` to widen access:

| Flag            | Effect                                                                                                                        |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| _(no flag)_     | Read-only: read / query / guide tools only — **110 tools**.                                                                   |
| `--allow-write` | Registers all create / update / delete tools → **213 tools**, including quota orders (money-spending).                        |

#### Claude Desktop / Cursor

Add an entry under `mcpServers`, pointing `--directory` at the `greennode-mcp` repo root:

```json
{
  "mcpServers": {
    "vmonitor": {
      "command": "uv",
      "args": [
        "run",
        "--directory", "/path/to/greennode-mcp",
        "vmonitor-mcp-server",
        "--allow-write"
      ]
    }
  }
}
```

Drop `--allow-write` if read-only is enough for your use case.

#### Claude Code

```bash
claude mcp add vmonitor -- \
  uv run --directory /path/to/greennode-mcp vmonitor-mcp-server --allow-write

# Verify
claude mcp list
```

#### Visual Studio Code (Copilot MCP)

Add a similar entry to `.vscode/mcp.json` or `settings.json`, with the same `command` / `args` as the Claude Desktop section.

### Test the server

To try the tools before wiring a client, run the **MCP Inspector** from the repo root:

```bash
npx @modelcontextprotocol/inspector uv run vmonitor-mcp-server                 # read-only, 110 tools
npx @modelcontextprotocol/inspector uv run vmonitor-mcp-server --allow-write   # all 213 tools
```

In the UI: Transport Type = `STDIO` → **Connect** → **Tools** → **List Tools**. A good first call is `list_dashboards` — if it returns your dashboards, authentication works.

### Troubleshooting

**Authentication fails (401):** Check `client_id` / `client_secret` in `~/.greennode/credentials` (run `grn configure`), or the `GRN_CLIENT_ID` / `GRN_CLIENT_SECRET` env vars. Call `list_dashboards` to confirm the IAM token can be obtained and vMonitor answers.

**Wrong project / resources missing:** Check `GRN_PROJECT_ID` and `GRN_PROFILE`. vMonitor is global — there is no region to double-check on this server.

**The agent reports a tool as unavailable:** The server is running read-only. Add `--allow-write`, then restart the client — write tools are not registered at all without the flag, so the agent cannot see them.

**Cannot connect:** Verify `--directory` points at the repo root and that `uv sync` has finished. Check the client log for startup errors.
