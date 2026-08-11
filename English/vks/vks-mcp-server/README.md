# VKS MCP Server

**VKS MCP Server** is a [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server that gives AI assistants (Claude, Cursor, Gemini, …) a set of tools to manage **VKS — GreenNode Kubernetes Service**: clusters, node groups, and the Kubernetes resources _inside_ those clusters.

MCP is an open standard for supplying structured context to LLMs. Instead of typing `grn` commands ([GreenNode CLI](https://docs.greennode.ai/vks/getting-started/manage-vks-with-the-greennode-cli)) or calling the public API directly, the AI assistant selects and invokes the tools that VKS MCP Server exposes — driven by a natural-language request.

Once connected, ask the AI assistant in plain language to:

* **Manage clusters**: list, inspect, create, update, delete clusters; view events; fetch the kubeconfig; enable auto-upgrade / auto-healing.
* **Manage node groups**: create, change the node count, autoscale, upgrade version, delete node groups.
* **Manage Kubernetes resources**: view/edit resources, apply YAML, read pod logs and events.

**Safe by default:** the server runs **read-only** — inspect only, nothing is changed. Mutating operations (create/update/delete) and sensitive-data reads (Secret, logs, events) work only when explicitly enabled at server startup (see Configure Local MCP).

### Getting started

This documentation set covers:

| Page                 | Contents                                                                                                                         |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Configure Remote MCP | Use the **hosted endpoint** over HTTP — nothing to install, sign in with a GreenNode IAM user straight from the browser.         |
| Configure Local MCP  | Run the server locally over **stdio** — suits Claude Desktop, Cursor, Claude Code, VS Code. Setup, client config, and run flags. |
| MCP Tools            | All 41 tools by handler, with parameters and access level (read / write / sensitive).                                            |

#### Which mode?

* **Remote (hosted)** — the fastest path: point your MCP client at one URL and sign in with an IAM user through the browser. No Python/`uv`, no credentials on the machine. See Configure Remote MCP.
* **Local (stdio)** — run the server on your own machine, authenticating with the credentials in `~/.greennode`. Access level is yours to choose via flags (`--allow-write`, `--allow-sensitive-data-access`). See Configure Local MCP.

### Requirements

* An **MCP client**: Claude Desktop, Claude Code, Cursor, VS Code (Copilot MCP), or any client that speaks MCP.
* **Remote (hosted)**: a **GreenNode IAM user** with VKS permissions — the client opens the sign-in flow itself; nothing to install, no secret to declare.
* **Local (stdio)**: **Python ≥ 3.11**, [`uv`](https://docs.astral.sh/uv/), and **GreenNode credentials** (`client_id` / `client_secret` in `~/.greennode/credentials` — shared with greennode-cli; run `grn configure` once if you haven't).

### Region

VKS currently serves two regions, declared as `Literal["HCM-3", "HAN"]`:

| Region  | Location         |
| ------- | ---------------- |
| `HCM-3` | Ho Chi Minh City |
| `HAN`   | Hanoi            |

Every `list_*` tool echoes back the region it queried, so results from the two regions never get mixed up.

### Resources

* **GreenNode CLI** — manage VKS from the command line: [Manage VKS with the GreenNode CLI](https://docs.greennode.ai/vks/getting-started/manage-vks-with-the-greennode-cli)
* **GreenNode MCP on GitHub** — [https://github.com/GreenNodeHub/greennode-mcp](https://github.com/GreenNodeHub/greennode-mcp)
* **Model Context Protocol** — the MCP specification: [modelcontextprotocol.io](https://modelcontextprotocol.io)
