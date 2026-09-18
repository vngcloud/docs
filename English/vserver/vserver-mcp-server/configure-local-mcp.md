# Configure Local MCP

**Local MCP** runs **vServer MCP Server** as a process on your own machine, connecting the MCP client to vServer over **stdio**. The server authenticates with the credentials in `~/.greennode` (shared with `greennode-cli`) to reach the vServer API.

Choose local when you need to set the access level yourself via the `--allow-write` flag or to run under service-account credentials. If you want to start using vServer MCP with nothing to install, see **Configure Remote MCP**.

### Requirements

* **Python ≥ 3.11**.
* [`uv`](https://docs.astral.sh/uv/) for environment management and Python execution.
* The [`greennode-mcp`](https://github.com/GreenNodeHub/greennode-mcp) repository cloned locally. The client points `--directory` at the repository, and `uv run` installs dependencies on the first run.
* An **MCP client**: Claude Desktop, Claude Code, Cursor, or VS Code (Copilot MCP).
* **GreenNode credentials**, provided in one of two ways:
  * Files at `~/.greennode/credentials` and `~/.greennode/config`: install `greennode-cli` according to the [GreenNode CLI guide](https://docs.greennode.ai/vserver/getting-started/manage-vserver-with-the-greennode-cli), then run `grn configure`.
  * Environment variables `GRN_CLIENT_ID` and `GRN_CLIENT_SECRET`, optionally with `GRN_DEFAULT_REGION`: no files are required, and environment variables always override files when both exist.

**Security**: Never commit `client_secret` to Git. The server keeps tokens in memory only — they are never written to disk or logged.

### Configuration

Credentials and region are read from `~/.greennode/credentials` and `~/.greennode/config`. The pre-rename `~/.greenode` directory is still read as a fallback when only that directory exists.

Environment variables have the highest priority and override file-based configuration:

| Variable             | Effect                                                                                   |
| -------------------- | ---------------------------------------------------------------------------------------- |
| `GRN_CLIENT_ID`      | Overrides `client_id`.                                                                   |
| `GRN_CLIENT_SECRET`  | Overrides `client_secret`.                                                               |
| `GRN_PROFILE`        | Selects a profile. The default is `default`.                                             |
| `GRN_DEFAULT_REGION` | Overrides the region: `HCM-3` or `HAN`.                                                  |
| `GRN_PROJECT_ID`     | Overrides `project_id` for the default region only; other regions resolve automatically. |

### Add to an MCP client

With **stdio**, the MCP client spawns the server itself from the `command` and `args` in its configuration. There is no server to start by hand.

**Read-only** is the default. Add `--allow-write` to `args` to widen access:

| Flag            | Effect                                                                                                                                                                                                                                    |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _(no flag)_     | Read-only: list, get, discovery, and dry-run tools only — **84 tools**.                                                                                                                                                                   |
| `--allow-write` | Registers all create, update, delete, and power tools — **183 tools**. Destructive tools, such as delete, rollback, and resize with data loss, additionally carry a `destructiveHint` annotation so clients can warn before running them. |

#### Claude Desktop / Cursor

Add an entry under `mcpServers`, pointing `--directory` at the `greennode-mcp` repository root:

```json
{
  "mcpServers": {
    "vserver": {
      "command": "uv",
      "args": [
        "run",
        "--directory", "/path/to/greennode-mcp",
        "vserver-mcp-server",
        "--allow-write"
      ]
    }
  }
}
```

Remove `--allow-write` when read-only access is sufficient.

#### Claude Code

```bash
claude mcp add vserver -- \\
  uv run --directory /path/to/greennode-mcp vserver-mcp-server --allow-write

# Verify
claude mcp list
```

#### Visual Studio Code (Copilot MCP)

Add a similar entry to `.vscode/mcp.json` or `settings.json`, using the same `command` and `args` as the Claude Desktop configuration.

### Troubleshooting

**Authentication fails (401)**\
Check `client_id` and `client_secret` in `~/.greennode/credentials`, then run `grn configure` if needed. Call `get_access_token` to confirm that an IAM bearer token can be obtained.

**Wrong region or resources are missing**\
Check the region in `~/.greennode/config` or `GRN_DEFAULT_REGION`: `HCM-3` or `HAN`. Every `list_*` tool echoes the region it queried, and each region has its own project. A resource in HAN is invisible from HCM-3, and vice versa.

**The agent reports that a tool is unavailable**\
The server is running in read-only mode. Add `--allow-write`, then restart the client.

**A `list_*` call returns fewer resources than the console shows**\
Some catalogues are gated by the caller's IAM policy:

* `list_active_vpcs`
* `list_elastic_ips`
* `list_shared_server_snapshots`
* `list_interconnect_circuit_types`
* `get_volume_snapshot_policy`

When the required grant is missing, these tools return `403 IAM_PERMISSION_DENIED`. The relevant tool docstring names the fallback in each case.

**Cannot connect**\
Verify that `--directory` points to the repository root and that `uv sync` has finished. Check the MCP client's log for startup errors.
