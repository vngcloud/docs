# Connect a Connector

> This guide helps you connect a connector from the Catalog to your project — configure the Gateway, pick the right Authentication mode, and complete authentication.

---

## Prerequisites

- **Admin** or **Editor** access in the AgentBase product, or equivalent permission granted via **IAM Policy**.
- At least 1 **MCP Gateway** already created to attach the connector to.
- For **OAuth** or **API Key** modes: a matching Secret Provider already set up, or use the **Managed** secret AgentBase provides.

---

## Open the Connect modal

1. Click **Connect** on the card of the connector you want, in the Catalog.

The **Connect [Connector Name]** modal opens with 3 fixed sections:

- **GENERAL** — **Connector Name** (required), **Description** (optional)
- **CONFIGURATION** — **MCP Gateway** (required, select from a dropdown, or click **+** to create a new one), **MCP URL** (auto-generated from the selected Gateway, not editable)
- **AUTHENTICATION** — select an **Authentication mode**: **OAuth** / **API Key** / **Inbound forward** / **No authorization**

![The GENERAL, CONFIGURATION, and AUTHENTICATION sections of the Connect modal](../../../.gitbook/assets/mcp-connector/connect-mcp-detail-part1.png)

{% hint style="info" %}
Some Authentication modes may be disabled:
- Depending on the connector — some connectors only allow **OAuth** or **API Key**; **Inbound forward** and **No authorization** aren't supported on those.
- **Inbound forward** only works when the selected **MCP Gateway**'s **Inbound Auth** is not **No authorization** (i.e. IAM Permissions or JWT) — this mode forwards the same credential the agent used to authenticate inbound to the Gateway, reusing it as the outbound auth to the MCP server. If Inbound Auth = No authorization, there's no credential to forward, so this mode is disabled.
{% endhint %}

---

## Configure Authentication mode = OAuth

1. Select **OAuth** in the AUTHENTICATION section.
2. Select the **OAuth mode**: **2LO** (server-to-server) or **3LO** (requires user consent via the provider's consent screen) — depending on what the connector supports.
3. Select the **Secret source**: **Managed** (use a secret AgentBase already manages) or **Custom** (bring your own Client ID/Secret).
4. Select the matching **Secret Provider** in the dropdown.
5. Open **Advanced settings** and fill in:
   - **OAuth scopes** — pre-selected scopes for the connector; removable or you can type new ones, with at least 1 scope required; use **Copy** or **Reset** to copy/restore the default list.
   - **Return URL** — the OAuth callback URL, defaulting to your AgentBase domain.
   - **Parameters** (optional) — click **Add parameter** to add a custom **Header key** / **Header value prefix** pair (e.g. `Authorization` / `Bearer`).
6. Click **Connect** (or **Authorize** for OAuth 3LO) once everything is filled in.

![Secret source, Secret Provider, and Advanced settings in the Connect modal](../../../.gitbook/assets/mcp-connector/connect-mcp-detail-part2.png)

{% hint style="info" %}
**Secret source** ties directly into the [Access Control](../access-control/README.md) feature (Identity):
- **Managed** — quickly pick a Secret Provider GreenNode already created, with no need to set up your own OAuth App.
- **Custom** — if the provider you need isn't available as Managed (e.g. Slack), you must create the OAuth App yourself on the matching platform, then add it as an OAuth Provider in **Access Control** — only then does it appear in the Secret Provider dropdown when creating an MCP Gateway/Connector.
- Access Control also supports **OAuth public client** — only a Client ID is required, no Client Secret.
{% endhint %}

For **OAuth 3LO**, the system opens a new tab/popup to the provider's consent screen — review the requested scopes, then accept to complete the flow.

---

## Configure Authentication mode = API Key

1. Select **API Key** in the AUTHENTICATION section.
2. Select the **API Key mode**: **2LO** or **3LO**.
3. Paste the **API Key/Token** obtained from the external service, or select an already-configured **Secret Provider**.
4. For **3LO**, also fill in the **Return URL**.
5. Click **Connect**.

---

## Configure Authentication mode = Inbound forward / No authorization

1. Select **Inbound forward** or **No authorization** in the AUTHENTICATION section — **Inbound forward** only works when the selected **MCP Gateway**'s **Inbound Auth** is not **No authorization** (IAM Permissions or JWT), since this mode forwards that inbound credential as the outbound auth.
2. Click **Connect** — no additional credentials are needed.

---

## Result

The connector appears in the **Connected** tab with status **ACTIVE**, ready to be attached to an agent.

| I want to next... | Go to |
|---|---|
| View, edit, or disconnect the connector I just created | [Manage Connected Connectors](manage-connected-connectors.md) |
