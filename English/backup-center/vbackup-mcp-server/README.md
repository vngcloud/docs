# vBackup MCP Server

**vBackup MCP Server** is a [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server that gives AI assistants (Claude, Cursor, Gemini, …) a set of tools to manage **vBackup — GreenNode's scheduled, policy-driven backup service** for vServer instances (with their volumes) and vDB databases, the restore points those backups produce, and the history of backup and restore runs.

MCP is an open standard for supplying structured context to LLMs. Instead of calling the public API directly, the AI assistant selects and invokes the tools that vBackup MCP Server exposes — driven by a natural-language request.

Once connected, ask the AI assistant in plain language to:

* **Manage backup destinations** ("Backup Locations"): create a vault or vStorage container, set the quota, enable soft delete, apply a vault lock.
* **Manage backup policies**: define an hourly/daily/weekly/monthly schedule with retention, promote a policy to default, or retire it.
* **Protect vServer instances**: choose a policy and destination, pick which disks to include, run an ad-hoc backup, pause / resume the schedule, download or delete a restore point.
* **Protect vDB databases** (PostgreSQL and Redis **cluster** deployments only): create a backup database, attach a policy, run an ad-hoc backup, delete a restore point.
* **Inspect coverage and history**: see who is protected and who is not, why last night's run failed, how much a destination is holding, and how the platform's charts trend over time.

vBackup is a different product from vServer's block-level **snapshots** — snapshots stay in vServer MCP Server. Backups are file-level, land in a destination vault, survive the source server, and are billed against the vault's quota.

**Safe by default:** the server runs **read-only** — inspect only, nothing is changed. Mutating operations (create / update / delete of destinations, policies, backup servers, backup databases, restore points) work only when explicitly enabled at server startup (see Configure Local MCP).

### Getting started

This documentation set covers:

| Page                 | Contents                                                                                                                         |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Configure Remote MCP | Use the **hosted endpoint** over HTTP — nothing to install, sign in with a GreenNode IAM user straight from the browser.         |
| Configure Local MCP  | Run the server locally over **stdio** — suits Claude Desktop, Cursor, Claude Code, VS Code. Setup, client config, and run flags. |
| MCP Tools            | All 68 tools by handler, with parameters and access level (read / write / destructive).                                          |

#### Which mode?

* **Remote (hosted)** — the fastest path: point your MCP client at one URL and sign in with an IAM user through the browser. No Python/`uv`, no credentials on the machine. See Configure Remote MCP.
* **Local (stdio)** — run the server on your own machine, authenticating with the credentials in `~/.greennode`. Access level is yours to choose via the `--allow-write` flag. See Configure Local MCP.

### Requirements

* An **MCP client**: Claude Desktop, Claude Code, Cursor, VS Code (Copilot MCP), or any client that speaks MCP.
* **Remote (hosted)**: a **GreenNode IAM user** with vBackup permissions — the client opens the sign-in flow itself; nothing to install, no secret to declare.
* **Local (stdio)**: **Python ≥ 3.11**, [`uv`](https://docs.astral.sh/uv/), and **GreenNode credentials** (`client_id` / `client_secret` in `~/.greennode/credentials` — shared with greennode-cli).

### Region

vBackup serves two regions, declared as `Literal["HCM-3", "HAN"]`:

| Region  | Location         |
| ------- | ---------------- |
| `HCM-3` | Ho Chi Minh City |
| `HAN`   | Hanoi            |

Every tool takes a `region` parameter, and every `list_*` output echoes back the region it queried. The two gateways see different resources — if something is not found in one, try the other. A single backup destination lives in exactly one region; the vMonitor dashboards are the only surface that answer for both regions in one call.

### Resources

* **vServer MCP Server** — for block-level snapshots (a different product on the same gateway): vServer MCP Server
* **GreenNode MCP on GitHub** — [https://github.com/GreenNodeHub/greennode-mcp](https://github.com/GreenNodeHub/greennode-mcp)
* **Model Context Protocol** — the MCP specification: [modelcontextprotocol.io](https://modelcontextprotocol.io)
