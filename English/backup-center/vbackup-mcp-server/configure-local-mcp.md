# Configure Local MCP

**Local MCP** runs **vBackup MCP Server** as a process on your own machine, connecting the MCP client to vBackup over **stdio**. The server authenticates with the credentials in `~/.greennode` (shared with greennode-cli) to reach the vBackup API.

Choose local when you need to set the access level yourself via the `--allow-write` flag or to run under service-account credentials. If you just want to start using it with nothing to install, see Configure Remote MCP.

### Requirements

* **Python ≥ 3.11**.
* [`uv`](https://docs.astral.sh/uv/) — environment management and Python execution.
* The [`greennode-mcp`](https://github.com/GreenNodeHub/greennode-mcp) repo cloned locally (the client points `--directory` at it; `uv run` installs dependencies on first run).
* An **MCP client**: Claude Desktop, Claude Code, Cursor, or VS Code (Copilot MCP).
* **GreenNode credentials** — two ways to provide them:
  * Files `~/.greennode/credentials` + `~/.greennode/config`: install greennode-cli and run `grn configure`.
  * Environment variables `GRN_CLIENT_ID` / `GRN_CLIENT_SECRET` (+ `GRN_DEFAULT_REGION`) — no files needed, and they always override files when both exist.

> ⚠️ **Security**: never commit `client_secret` to Git. The server keeps tokens in memory only — never written to disk, never logged.

### Configuration

Credentials and region are read from `~/.greennode/credentials` + `~/.greennode/config` (the pre-rename `~/.greenode` directory is still read as a fallback when only it exists). Environment variables override the files (highest priority):

| Variable             | Effect                                 |
| -------------------- | -------------------------------------- |
| `GRN_CLIENT_ID`      | Override `client_id`                   |
| `GRN_CLIENT_SECRET`  | Override `client_secret`               |
| `GRN_PROFILE`        | Select a profile (default: `default`)  |
| `GRN_DEFAULT_REGION` | Override the region (`HCM-3` or `HAN`) |
| `GRN_PROJECT_ID`     | Override `project_id`                  |

### Add to MCP client

With **stdio** the MCP client spawns the server itself from the `command` / `args` in its config — there is no server to start by hand. **Read-only** is the default; add `--allow-write` to `args` to widen access:

| Flag            | Effect                                                                                                                                                                                                                                       |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _(no flag)_     | Read-only: list / get / discovery tools only — **41 tools**.                                                                                                                                                                                 |
| `--allow-write` | Registers all create / update / delete tools → **68 tools**. Destructive ones (deleting a destination, a policy, a backup server, a backup database, a restore point) additionally carry a `destructiveHint` annotation so clients can warn. |

### Claude Desktop / Cursor

Add an entry under `mcpServers`, pointing `--directory` at the `greennode-mcp` repo root:

```json
{
  "mcpServers": {
    "vbackup": {
      "command": "uv",
      "args": [
        "run",
        "--directory", "/path/to/greennode-mcp",
        "vbackup-mcp-server",
        "--allow-write"
      ]
    }
  }
}
```

Drop `--allow-write` if read-only is enough.

### Claude Code

```bash
claude mcp add vbackup -- \
  uv run --directory /path/to/greennode-mcp vbackup-mcp-server --allow-write

# Verify
claude mcp list
```

### Visual Studio Code (Copilot MCP)

Add a similar entry to `.vscode/mcp.json` or `settings.json`, with the same `command` / `args` as the Claude Desktop section.

### Troubleshooting

**Authentication fails (401):** Check `client_id` / `client_secret` in `~/.greennode/credentials` (run `grn configure`). Call `get_access_token` to confirm an IAM bearer token can be obtained.

**Wrong region / resources missing:** Check the region in `~/.greennode/config` or `GRN_DEFAULT_REGION` (`HCM-3` or `HAN`). Every `list_*` tool echoes back the region it queried. The two gateways see different resources — the HAN gateway returns both HAN and HCM backends while the HCM gateway returns only its own, so an unfound resource might just live in the other region.

**"Nothing is protected" is a lie about the vDB side:** `list_databases` shows every vDB instance the account owns and reports eligibility per instance in `ineligible_reason` — a single-node PostgreSQL is ineligible for backup and comes back with a reason, not silently omitted. Only cluster deployments can be backed up.

**The agent reports a write tool as unavailable:** The server is running read-only. Add `--allow-write`, then restart the client.

**A `list_*_history` call returns an empty or short list:** `list_backup_history` and `list_database_backup_history` apply a silent **180-day** default window on the API side. An empty response is never proof that a backup did not run — pass `from_date` (epoch milliseconds or ISO-8601) to reach further back.

**A destination edit was refused with `Cannot edit vault lock`:** The lock is permanent. That happens when a vault lock was created with `changeDuration=0`, or the lock's change window has expired. The DTO forbids the zero value on new locks; an existing permanent lock cannot be edited or disabled through any tool.

**A vDB backup delete keeps failing:** Two 409s block a delete. `Your resource is being processed.` is a wait — retry after the point finishes uploading. `Your resource is being managed by Vault.` is not — it succeeds only once the vault-lock retention expires or the lock is lifted.

**Cannot connect:** Verify `--directory` points at the repo root and that `uv sync` has finished. Check the client log for startup errors.
