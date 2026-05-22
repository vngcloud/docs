# Team & Permissions

**Team & Permissions** helps Root and Admin control who can access AgentBase and with what level of access — through pre-built roles wrapped by AgentBase, easy to assign without manual IAM policy configuration.

Access at: [https://aiplatform.console.vngcloud.vn/team-permissions](https://aiplatform.console.vngcloud.vn/team-permissions)

![Team & Permissions — member list](../../../.gitbook/assets/Agentbase-image/Members-list.png)

---

## Overview

**Team & Permissions** contains three tabs:

| Tab | Description |
|---|---|
| **Members** | View the org member list; invite new members by copying the IDP Login URL; assign/change roles via the ⋮ icon |
| **Roles & Permissions** | Read-only permission matrix — understand what each role can do before assigning |
| **Service Accounts** | View SAs auto-created when deploying agents; click a SA to go to IAM and manage credentials |

---

## Roles in AgentBase

AgentBase provides 4 pre-built roles wrapping IAM policies — simply select the right role, no manual policy configuration needed:

| Role | Summary |
|---|---|
| **Root** | Org owner — full access including billing and SA secrets. One per org. |
| **Admin** | Admin appointed by Root — manage members, agents, and org config. No billing, quota, or model config permissions. |
| **Member** | Active contributor — create and run own agents; view SAs for agents they created |
| **Viewer** | Read-only — view agent config, logs, and conversation history. Cannot perform any side-effect actions. |

---

## Invite Members

New members log in to AgentBase through a configured **Identity Provider (IDP)** in IAM — no separate account creation needed. To invite:

1. Go to the **Members** tab → click **Invite Member**
2. Copy the **Login URL** for the appropriate IDP
3. Send the URL to the member — they visit the link, authenticate via IDP, and are automatically added to the org

After the member logs in for the first time, Root assigns the appropriate role via the ⋮ icon on the member's row.

---

## Getting Started

| I want to... | Go to |
|---|---|
| View, invite, remove members and assign roles | [Manage Members](manage-members.md) |
| Understand permissions for each role | [Roles & Permissions](roles-and-permissions.md) |
| View Service Accounts for agents | [Manage Service Accounts](manage-service-accounts.md) |