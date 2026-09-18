# vServer MCP Server

**vServer MCP Server** is a [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server that gives AI assistants (Claude, Cursor, Gemini, …) a set of tools to manage **vServer — GreenNode's compute / IaaS product**: virtual machine instances, block-storage volumes, snapshots, images, networking (VPC, subnet, security group, network ACL, route table, peering, interconnect, virtual IP, floating IP, network interface, DHCP option set), SSH keys, and placement groups.

MCP is an open standard for supplying structured context to LLMs. Instead of typing `grn` commands ([GreenNode CLI](https://docs.greennode.ai/vserver/getting-started/manage-vserver-with-the-greennode-cli)) or calling the public API directly, the AI assistant selects and invokes the tools that vServer MCP Server exposes, driven by a natural-language request.

Once connected, ask the AI assistant in plain language to:

* **Manage instances**: list, inspect, create, resize, power on/off, delete servers; capture user images; read the serial console.
* **Manage storage**: create, attach, resize, and delete volumes; move a volume to a new IOPS tier; inspect volume history.
* **Manage networking**: VPCs and subnets, security groups and rules, network ACLs, route tables, VPC peering, interconnects, virtual IPs, floating IPs, elastic network interfaces, and DHCP option sets.
* **Manage snapshots**: block-level snapshot points and policies for servers and volumes; roll back or delete points.
* **Manage keys, placement, and tags**: SSH keys, placement groups (affinity / anti-affinity), and the tag vocabulary.

Coverage goes beyond the GreenNode CLI command set: snapshots, route tables, network ACLs, VPC peering, interconnects, and virtual IPs have no CLI equivalent.

**Safe by default**: the server runs read-only — inspect only, nothing is changed. Mutating operations (create, update, delete, and power actions) work only when explicitly enabled at server startup. See **Configure Local MCP**.

### Getting started

This documentation set covers:

| Page                 | Contents                                                                                                       |
| -------------------- | -------------------------------------------------------------------------------------------------------------- |
| Configure Remote MCP | Use the hosted endpoint over HTTP — nothing to install; sign in with a GreenNode IAM user through the browser. |
| Configure Local MCP  | Run the server locally over stdio — suitable for Claude Desktop, Cursor, Claude Code, and VS Code.             |
| MCP Tools            | All 183 tools by handler, with parameters and access level (read / write / destructive).                       |

### Which mode?

* **Remote (hosted)** — the fastest path: point your MCP client at one URL and sign in with an IAM user through the browser. No Python, `uv`, or credentials on the machine. See **Configure Remote MCP**.
* **Local (stdio)** — run the server on your own machine, authenticating with the credentials in `~/.greennode`. Choose the access level with the `--allow-write` flag. See **Configure Local MCP**.

### Requirements

* An **MCP client**: Claude Desktop, Claude Code, Cursor, VS Code (Copilot MCP), or any client that speaks MCP.
* **Remote (hosted)**: a **GreenNode IAM user** with vServer permissions. The client opens the sign-in flow itself; nothing needs to be installed and no secret needs to be declared.
* **Local (stdio)**: **Python ≥ 3.11**, [`uv`](https://docs.astral.sh/uv/), and **GreenNode credentials** (`client_id` / `client_secret` in `~/.greennode/credentials`, shared with `greennode-cli`). Run `grn configure` once if needed.

### Region

vServer serves two regions, declared as `Literal["HCM-3", "HAN"]`:

| Region  | Location         |
| ------- | ---------------- |
| `HCM-3` | Ho Chi Minh City |
| `HAN`   | Hanoi            |

Every resource is region-scoped, and each region's gateway exposes its own project. The server resolves the project ID itself, so tools never take a `project_id` parameter. Zone IDs are readable strings (`HCM03-1A` … `HCM03-BKK-01`), not UUIDs. Every `list_*` tool echoes back the region it queried, so results from the two regions never get mixed up.

### Resources

* **GreenNode CLI** — manage vServer from the command line: [Manage vServer with the GreenNode CLI](https://docs.greennode.ai/vserver/getting-started/manage-vserver-with-the-greennode-cli)
* **GreenNode MCP on GitHub** — [GreenNodeHub/greennode-mcp](https://github.com/GreenNodeHub/greennode-mcp)
* **Model Context Protocol** — the MCP specification: [modelcontextprotocol.io](https://modelcontextprotocol.io)
