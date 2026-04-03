# Deploy & Manage OpenClaw 1-Click

OpenClaw 1-Click lets you deploy a personal AI Agent on GreenNode AgentBase in 40–60 seconds, automatically connected to GreenNode MaaS with no manual configuration required.

For an overview of concepts, architecture, and deployment options, see [OpenClaw 1-Click](openclaw-1-click.md).

***

## Deploy an OpenClaw Instance

### Access the Agent Marketplace

You can access the Agent Marketplace in two ways:

* **Option 1**: Go to the GreenNode homepage at [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/). From the main dashboard, navigate to **AI Stack** and select **AgentBase** → **Agent Marketplace**.
* **Option 2**: Go directly to [https://aiplatform.console.vngcloud.vn/agent-marketplace](https://aiplatform.console.vngcloud.vn/agent-marketplace).

### Deploy an OpenClaw Instance

On the Agent Marketplace, find the **OpenClaw Featured Card** or click **"Deploy OpenClaw With 1 Click!"** on the Hero Banner. The deployment process goes through the following steps:

#### Step 1: Configure Your Deployment

The configuration screen has 3 sections:

**Section 1 — AI Source**

Select the AI source for your OpenClaw instance:

| Option | Description | Requirement |
| --- | --- | --- |
| **GreenNode MaaS** (default) | Automatically connects to GreenNode Model-as-a-Service | GreenNode account required |
| **BYOK — Bring Your Own Key** | Use an API key from an external provider | Valid API key required |

{% hint style="info" %}
**GreenNode MaaS:** The default model is **Qwen-3-27b**.
{% endhint %}

When selecting **BYOK**, provide the following additional details:

* **Provider**: Select your provider (OpenAI, Anthropic, Gemini, Custom).
* **API Key**: Enter your API key. The system will validate it before proceeding.
* **Model**: Select the model corresponding to your chosen provider.

{% hint style="warning" %}
**BYOK note:** If the API key is invalid or expired, the system will show an inline error and block submission. Double-check your key before submitting.
{% endhint %}

**Section 2 — Instance Configuration**

| Field | Description | Notes |
| --- | --- | --- |
| **OpenClaw Name** | Instance identifier | Auto-filled as `openclaw/{username}`, editable. Must not duplicate a currently Running instance name |
| **Flavor** | Compute resource configuration (vCPU × RAM) | Default: `2×4`. Options include `4×8`, `8×16`... |

**Section 3 — Channel Configuration (Optional)**

Connect OpenClaw to a messaging platform so you can chat right after deployment.

| Field | Description | Notes |
| --- | --- | --- |
| **Channel Provider** | Messaging platform | Supported: Telegram, Zalo |
| **Mode** | Connection mode | Pairing (default) or Allow List |
| **Bot Token** | Telegram Bot Token | Optional. Can be configured later at Settings → Config |

Once all fields are filled, click **"Start Setup"** to begin provisioning.

#### Step 2: Provisioning — Setting Up Your Workspace

The **"Setting Up Your Workspace"** screen displays a loading spinner while the system automatically runs 4 provisioning tasks:

| Task | Description |
| --- | --- |
| **OpenClaw Token** | Creates an Identity and authentication token for the instance |
| **AI Service Account** | Creates an IAM Service Account connected to MaaS |
| **AI Service Token** | Retrieves the access token for the selected AI model |
| **Cloud Computer** | Starts the OpenClaw container |

Once provisioning is complete, you are automatically redirected to the Deploy Success screen.

{% hint style="info" %}
**If provisioning fails:** The system displays an error state with a **Troubleshoot** link and a **Retry** button. Failed instances do not count against your quota.
{% endhint %}

#### Step 3: Deploy Success

Once provisioning is complete, the Deploy Success screen shows your instance details:

| Field | Description |
| --- | --- |
| **Instance Name** | The name of your created instance (e.g. `openclaw/username`) |
| **Status** | 🟢 Active |
| **AI Model** | The model and AI source in use |
| **OpenClaw Gateway URL** | Link to your OpenClaw Gateway Dashboard |
| **Created At** | Timestamp |

Click **"Open OpenClaw"** to access your OpenClaw Gateway Dashboard and start using it immediately.

***

## Manage OpenClaw Instances

### Access My Agents Dashboard

In the AgentBase interface, select **My Agents** from the navigation menu. This page displays all your OpenClaw instances in two sections:

| Section | Condition | Description |
| --- | --- | --- |
| **Running 🟢** | At least 1 instance is running | Instance cards with an "Open" button |
| **Stopped ⚪** | At least 1 instance is stopped | Instance cards with a "Restart" button |

Each instance card shows: instance name, status, AI model in use, version, and tags.

### Open an Instance

1. In My Agents Dashboard, find the instance in the **Running** section.
2. Click **"Open"** on the instance card.
3. You are redirected straight to the OpenClaw Gateway Dashboard — no wizard or re-provisioning required.

### Stop an Instance

1. In My Agents Dashboard, find the instance in the **Running** section.
2. Click **"Stop"** on the instance card.
3. Confirm in the dialog that appears.

After stopping, the instance moves to the **Stopped** section and its URL is no longer accessible.

### Restart an Instance

1. In My Agents Dashboard, find the instance in the **Stopped** section.
2. Click **"Restart"** on the instance card.
3. The instance transitions through **Starting → Running**.

After restarting, the URL becomes accessible again and the card moves back to the **Running** section.

### Delete an Instance

1. In My Agents Dashboard, click **"Delete"** on the instance card (Running or Stopped).
2. A confirmation dialog appears, requiring you to type the **instance name**.
3. Enter the exact instance name and click **"Delete"** (red button) to confirm.

{% hint style="warning" %}
**Note when deleting:**

* Deletion is **permanent and cannot be undone**.
* All instance data will be **permanently deleted**.
{% endhint %}

### Auto-shutdown

If an instance receives no requests for **24 consecutive hours**, the system automatically stops it and sends an email notification. You can Restart at any time from My Agents Dashboard.
