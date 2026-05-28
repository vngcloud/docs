# Manage MCP Gateway

> Step-by-step guide to creating, viewing, editing, and deleting MCP Gateways on the GreenNode AI Platform Portal.

***

## Prerequisites

* A GreenNode AI Platform account with **Root** or **Admin** role
* At least one Secret created in the **Identity** component (required if using Outbound Auth = OAuth 2.0 or API Key)
* If using **Private** network: an existing VPC and Subnet with DNS resolution enabled

***

## View the MCP Gateway List

1. Sign in to the [GreenNode AI Platform Portal](https://console.greennode.ai).
2. Select **AgentBase** in the left menu.
3. Select **MCP Governance** → **MCP Gateway**.

The page displays a table with columns: **Gateway name**, **Description**, **Status**, **Inbound Auth**, **Targets**, **Creation time**, and **Actions**.

| Status       | Meaning                                                     |
| ------------ | ----------------------------------------------------------- |
| **Active**   | Gateway is running normally                                 |
| **Creating** | Being provisioned on Kong (≤ 30 seconds)                    |
| **Updating** | Configuration update in progress (≤ 30 seconds)             |
| **Deleting** | Being removed from Kong                                     |
| **Error**    | Provisioning failed — hover over the badge to see the error |

***

## Create an MCP Gateway

**Step 1: Open the Create Gateway form**

1. On the **MCP Gateway** page, click **Create Gateway**.
2. The **Create MCP Gateway** page opens with a 5-section vertical form.

***

**Step 2: Basic Configuration (① Basic Configuration)**

1. Enter a **Gateway name** — required; only `a–z`, `A–Z`, `0–9`, and hyphens; minimum 5 characters, maximum 50; must be unique within the org.
2. Enter a **Description** (optional).

***

**Step 3: Inbound Authentication (② Inbound Identity)**

1. Select an **Inbound Auth type**:
   * **JSON Web Tokens (JWT)** _(default)_ — agents attach a JWT when calling the gateway
   * **IAM Permissions** — uses the GreenNode AI Platform IAM token
   * **No authorization** — gateway is publicly accessible

{% hint style="warning" %}
Selecting **No authorization** makes the gateway publicly accessible with no access control. Use only in development environments or when the network is protected at another layer.
{% endhint %}

2. If you select **JWT**, configure the following:
   * **JWT key source**: choose **Discovery URL** (gateway automatically fetches and refreshes public keys from the OIDC well-known endpoint) or **JWKS** (paste JSON directly — must be valid JSON with a `keys` field)
   * **Audience** (optional) — JWT audience claim
   * **Allowed clients** (optional) — list of permitted client IDs; type and press Enter to add each tag
   * **Allowed scopes** (optional) — permitted scopes; type and press Enter to add each tag
   * **Principal claim** — the JWT claim used as the principal when enforcing Policy; default `sub`

***

**Step 4: Add MCP Servers (③ MCP Servers)**

1. An **MCP Server 1** card is pre-created. Fill in the fields:

| Field                   | Required                        | Notes                                             |
| ----------------------- | ------------------------------- | ------------------------------------------------- |
| **MCP Server name**     | Yes                             | Identifier for this server                        |
| **MCP endpoint URL**    | Yes                             | Full HTTPS URL of the MCP server                  |
| **Outbound Auth**       | Yes                             | OAuth 2.0 / API Key / No authentication           |
| **Mode**                | When using OAuth 2.0 or API Key | 2LO (Machine to machine) or 3LO (User federation) |
| **Secret Provider**     | When using OAuth 2.0 or API Key | Select from the Identity secrets list             |
| **Scopes**              | When using OAuth 2.0            | Type and press Enter to add each scope            |
| **Return URL**          | When Mode = 3LO                 | Callback URL after user redirect                  |
| **Header key**          | When using OAuth 2.0 or API Key | Default `Authorization`                           |
| **Header value prefix** | When using OAuth 2.0 or API Key | Default `Bearer` (trailing space included)        |

2. To add another MCP server, click **+ Add MCP Server**.

***

**Step 5: Attach a Policy Group (④ Policy group)**

1. Open the **Choose a policy group...** dropdown and select a Policy Group.
2. If no Policy Group exists yet, click **+ Create new policy group** (opens in a new tab), then return and refresh the dropdown.

{% hint style="warning" %}
Policy Group is optional when creating the gateway, but if none is attached, **all MCP tool calls through the gateway are blocked with 403**. Attach a Policy Group before agents start using the gateway.
{% endhint %}

***

**Step 6: Network & Compute (⑤ Network & Compute)**

1. Select a **Network mode**:
   * **Public** — The system manages zone assignment automatically; no additional configuration needed
   * **Private** — select a **VPC** and a **Subnet** (displayed as `<subnet-name> · Zone: <zone-name>`); ensure DNS resolution is enabled in the VPC
2. Select a **Flavor** from the dropdown.
3. Set the number of **Replicas** (1–10, default 1).

***

**Step 7: Submit**

1. Click **Create Gateway** in the footer.
2. The gateway is created with Status = **Creating**.
3. Within 30 seconds, the Status changes to **Active** — IAM Service Account `sa-gateway-<id>` is automatically created and attached to the gateway.

***

## View Gateway Details

1. On the **MCP Gateway** page, click the gateway name (hyperlink).
2. The **Gateway Detail** page shows:
   * **General information**: ID, Description, Inbound Auth, Network mode, Created on, Last updated, Endpoint URL, Service account
   * **Detail information** with 4 tabs:

| Tab                   | Content                                                                                  |
| --------------------- | ---------------------------------------------------------------------------------------- |
| **MCP Servers**       | List of MCP servers attached to the gateway; Root/Admin can add, edit, or delete servers |
| **Inbound Auth**      | Inbound authentication configuration; Root/Admin can edit                                |
| **Policy**            | Attached Policy Group and its policy list (with ENABLE/DISABLE/DENY status)              |
| **Network & Compute** | Network mode, VPC, Subnet, Flavor, Replicas, and estimated cost                          |

***

## Edit an MCP Gateway

1. On the **MCP Gateway** page, click **⋮** on the target row and select **Edit**.
2. The Edit Gateway form opens with pre-filled values — update the fields you want to change.
3. Click **Save**.
4. The gateway transitions to Status = **Updating**, then returns to **Active** within 30 seconds.

{% hint style="warning" %}
If you switch to a different Policy Group while the gateway has active traffic, a confirmation dialog appears before the change is applied. The new policy takes effect within 30 seconds after saving.
{% endhint %}

***

## Delete an MCP Gateway

1. On the **MCP Gateway** page, tick the checkbox on the target row.
2. Click **Delete** on the toolbar (red icon).
3. Confirm in the dialog.
4. The gateway transitions to Status = **Deleting** and is removed from the list after Kong deprovisions it (within 30 seconds).

{% hint style="warning" %}
Deleting a gateway cannot be undone. Agents currently calling through this gateway will immediately start receiving errors. Ensure no agents are using the gateway before deleting it.
{% endhint %}

***

## Result

Once successfully created, the gateway is in **Active** status and agents can start routing MCP tool calls through the Endpoint URL shown in the General information section.

| I want to next...                          | Go to                 |
| ------------------------------------------ | --------------------- |
| Learn about Policy Group to control access | [MCP Governance](../) |
| Review MCP Gateway architecture            | [MCP Gateway](./)     |
