# Configure Local MCP

**Local MCP** runs **VKS MCP Server** as a process on your own machine, connecting the MCP client to VKS over **stdio**. The server authenticates with the credentials in `~/.greennode` (shared with greennode-cli) to reach VKS.

Choose local when you need to set the access level yourself via flags (`--allow-write`, `--allow-sensitive-data-access`) or to run under service-account credentials. If you just want to start using it with nothing to install, see Configure Remote MCP.

### Requirements

* **Python ≥ 3.11**.
* [`uv`](https://docs.astral.sh/uv/) — environment management and Python execution.
* The [`greennode-mcp`](https://github.com/GreenNodeHub/greennode-mcp) repo cloned locally (the client points `--directory` at it; `uv run` installs dependencies on first run).
* An **MCP client**: Claude Desktop, Claude Code, Cursor, or VS Code (Copilot MCP).
* **GreenNode credentials** — two ways to provide them:
  * Files `~/.greennode/credentials` + `~/.greennode/config`: install greennode-cli per the [GreenNode CLI guide](https://docs.greennode.ai/vks/getting-started/manage-vks-with-the-greennode-cli), then run `grn configure`.
  * Environment variables `GRN_CLIENT_ID` / `GRN_CLIENT_SECRET` (+ `GRN_DEFAULT_REGION`) — no files needed, and they always override files when both exist.

> ⚠️ **Security**: never commit `client_secret` to Git. The server keeps tokens in memory only — never written to disk, never logged.

### Configuration

Credentials and region are read from `~/.greennode/credentials` + `~/.greennode/config` (the pre-rename `~/.greenode` directory is still read as a fallback when only it exists). Environment variables override the files (highest priority):

| Variable             | Effect                                                          |
| -------------------- | --------------------------------------------------------------- |
| `GRN_CLIENT_ID`      | Override `client_id`                                            |
| `GRN_CLIENT_SECRET`  | Override `client_secret`                                        |
| `GRN_PROFILE`        | Select a profile (default: `default`)                           |
| `GRN_DEFAULT_REGION` | Override the region (`HCM-3` or `HAN`)                          |
| `GRN_PROJECT_ID`     | Override `project_id` (auto-discovered from vServer when unset) |

### Add to MCP client

With **stdio** the MCP client spawns the server itself from the `command` / `args` in its config — there is no server to start by hand. **Read-only** is the default; add flags to `args` to widen access:

| Flag                            | Effect                                                                                                                                               |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| _(no flag)_                     | Read-only: read / discovery / dry-run tools only — **29 tools**.                                                                                     |
| `--allow-write`                 | Registers 12 more create / update / delete tools → **41 tools**.                                                                                     |
| `--allow-sensitive-data-access` | Allows reading the kubeconfig, Secrets, pod logs and events. Adds no new tools — those tools are always listed but refuse the call without the flag. |

Both flags together → all 41 tools, with no block on sensitive-data reads.

#### Claude Desktop / Cursor

Add an entry under `mcpServers`, pointing `--directory` at the `greennode-mcp` repo root:

```json
{
  "mcpServers": {
    "vks": {
      "command": "uv",
      "args": [
        "run",
        "--directory", "/path/to/greennode-mcp",
        "vks-mcp-server",
        "--allow-write"
      ]
    }
  }
}
```

Drop `--allow-write` if read-only is enough; add `--allow-sensitive-data-access` when you need to read the kubeconfig / Secrets / logs.

#### Claude Code

```bash
claude mcp add vks -- \
  uv run --directory /path/to/greennode-mcp vks-mcp-server --allow-write

# Verify
claude mcp list
```

#### Visual Studio Code (Copilot MCP)

Add a similar entry to `.vscode/mcp.json` or `settings.json`, with the same `command` / `args` as the Claude Desktop section.

### Troubleshooting

**Authentication fails (401):** Check `client_id` / `client_secret` in `~/.greennode/credentials` (run `grn configure`). Call `get_access_token` to confirm an IAM bearer token can be obtained.

**Wrong region / resources missing:** Check the region in `~/.greennode/config` or `GRN_DEFAULT_REGION` (`HCM-3` or `HAN`). Every `list_*` tool echoes back the region it queried.

**The agent reports a tool as unavailable:** The server is running read-only. Add `--allow-write` (and/or `--allow-sensitive-data-access`), then restart the client.

**Cannot connect:** Verify `--directory` points at the repo root and that `uv sync` has finished. Check the client log for startup errors.
