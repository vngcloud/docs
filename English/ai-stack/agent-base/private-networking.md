# Private Networking

Connect your VPC to AgentBase via VPC Peering — giving Agent Runtime and MCP Gateway direct access to your databases, internal APIs, and MCP Servers without routing traffic through the public internet.

---

## Public vs Private

AgentBase supports two network modes when creating an Agent Runtime or MCP Gateway:

| | **Public** | **Private** |
|---|---|---|
| **Access** | Through AgentBase's shared public gateway | Through a private gateway dedicated to your org |
| **Traffic path** | Over the internet | Internal — never leaves the private network |
| **Reach internal resources** | No | Yes — agent/gateway calls directly into your VPC |
| **Requires** | Nothing | VPC Peering between your VPC and AgentBase |

When you select **Private**, AgentBase provisions a dedicated private gateway for your org and routes all traffic through VPC Peering — ensuring that every call between your agent and your internal infrastructure stays on the private network.

![AgentBase Private Networking — VPC Peering](../../.gitbook/assets/Agentbase-image/VPC-Peering-Diagram.png)

{% hint style="info" %}
To use **Private** mode, VPC Peering between your VPC and the AgentBase VPC must be set up beforehand. Contact GreenNode support to activate it.
{% endhint %}

---

## Configure Private for Agent Runtime

> Performed at the **Network settings** step during Agent Runtime creation.

**Step 1: Select Private mode**

1. Open the Agent Runtime creation flow — see [Create a Runtime](agent-runtime/khoi-tao-runtime.md)
2. At the **Network settings** step, select **Private**
3. The **VPC**, **Subnet**, and **Route CIDRs** fields appear

![Select Private — Agent Runtime](../../.gitbook/assets/Agentbase-image/Create-runtime-choose-private-pvc.png)

**Step 2: Choose VPC and Subnet**

1. Select a **VPC** from the dropdown — only VPCs already peered with AgentBase are listed
2. Click the refresh icon if a recently created VPC does not appear
3. Select the **Subnet** for the Runtime

| Field | Required | Notes |
|---|---|---|
| **VPC** | Yes | VPC with VPC Peering established to AgentBase |
| **Subnet** | Yes | Subnet within the selected VPC |
| **Route CIDRs** | No | Add CIDR ranges if the Runtime needs to route to other subnets in your infrastructure |

**Step 3: Complete the Runtime**

Fill in the remaining fields (Run command, Flavor, environment variables...) and click **CREATE RUNTIME**.

---

## Configure Private for MCP Gateway

> Performed at the **Network & Compute** step during MCP Gateway creation.

**Step 1: Select Private mode**

1. Open the MCP Gateway creation flow — see [Manage MCP Gateway](mcp-governance/mcp-gateway/manage-mcp-gateway.md)
2. At the **Network & Compute** step, select **Private**
3. The **VPC**, **Subnet**, **Route CIDRs**, **Flavor**, and **Replicas** fields appear

![Select Private — MCP Gateway](../../.gitbook/assets/Agentbase-image/mcp-gateway-private-pvc.png)

**Step 2: Choose VPC, Subnet, and Flavor**

1. Select a **VPC** already peered with AgentBase
2. Click the refresh icon if a recently created VPC does not appear
3. Select a **Subnet** — each option shows Zone and CIDR
4. Enter **Route CIDRs** if the Gateway needs to reach additional subnets
5. Select a **Flavor** appropriate for the Gateway's expected load
6. Enter the number of **Replicas**

| Field | Required | Notes |
|---|---|---|
| **VPC** | Yes | VPC with VPC Peering established to AgentBase |
| **Subnet** | Yes | Subnet within the selected VPC, displayed with Zone and CIDR |
| **Route CIDRs** | No | Additional CIDRs if the Gateway needs to reach more subnets |
| **Flavor** | Yes | Compute size for the Gateway — e.g. `general-2×4` (2 CPU, 4 GB RAM) |
| **Replicas** | Yes | Number of parallel Gateway instances |

**Step 3: Complete the Gateway**

Fill in the remaining fields (Inbound Auth, MCP Servers, Policy Group...) and click **SAVE**.

---

## Result

After creation with Private mode:

- **Agent Runtime**: runs on the private network and calls directly into your VPC's databases and internal APIs — no public internet exposure
- **MCP Gateway**: receives MCP tool calls from agents and forwards them to MCP Servers inside your VPC over the private connection

| I want to... | Go to |
|---|---|
| Create an Agent Runtime with a private network | [Create a Runtime](agent-runtime/khoi-tao-runtime.md) |
| Create an MCP Gateway with a private network | [Manage MCP Gateway](mcp-governance/mcp-gateway/manage-mcp-gateway.md) |
| Understand how MCP Gateway controls tool calls | [MCP Governance](mcp-governance/README.md) |
