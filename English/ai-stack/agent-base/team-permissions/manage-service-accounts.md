# Manage Service Accounts

> Service Accounts (SAs) are automatically created when an agent is deployed — this tab lets Root and Admin view the list of active SAs and navigate to IAM to manage credentials.

---

## Prerequisites

- Signed in with role **Root** or **Admin**

---

## Open the Service Accounts Tab

Go to [Team & Permissions](https://aiplatform.console.vngcloud.vn/team-permissions) → **Service Accounts** tab

The list shows:

| Column | Description |
|---|---|
| **SA Name** | SA name following the convention `auto-sa-{agent-slug}` |
| **Client ID** | 8-character prefix + `***` (masked) |
| **Type** | "Auto-generated" — SAs are only created by the system when an agent is deployed |
| **Associated Agent** | Name of the linked agent; shows "—" if the agent has been deleted |
| **Created By** | The member who deployed the agent |
| **Created Date** | Creation date |
| **Status** | Active / Revoked |

---

## View and Manage Credentials in IAM

Click any SA in the list → the system takes you to **IAM** where you can view the Client Secret, revoke credentials, and perform full credential management.

{% hint style="warning" %}
The Client Secret is only shown once immediately after the agent is deployed. After that, only Root can view it again through IAM — each view is recorded in the Audit Log.
{% endhint %}

---

## Orphaned SAs — Agent Deleted

When a linked agent is deleted, the corresponding SA displays an **Orphaned** badge in the **Associated Agent** column. Navigate to IAM to revoke the SA and prevent uncontrolled credentials from persisting in the system.

---

## Next Steps

| I want to... | Go to |
|---|---|
| Manage members and assign roles | [Manage Members](manage-members.md) |
| Understand permissions for each role | [Roles & Permissions](roles-and-permissions.md) |