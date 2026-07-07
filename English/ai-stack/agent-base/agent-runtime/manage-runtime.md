# Manage Runtime

> Guide to stopping, starting, updating, managing Endpoints, rolling back versions, and deleting an Agent Runtime.

***

## Prerequisites

* At least 1 Runtime already created
* Role Root or Admin

***

## Stop a Runtime

Stop a Runtime to save compute costs. Configuration, Endpoint, and logs are preserved.

**Step 1:** Open **Agent Runtime** → locate the Runtime to stop

**Step 2:** Click **Stop** → confirm

{% hint style="warning" %}
While the Runtime is in `STOPPED` state, all requests to its Endpoint will return an error until it is started again.
{% endhint %}

***

## Start a Runtime

**Step 1:** Open **Agent Runtime** → locate the `STOPPED` Runtime

**Step 2:** Click **Start** → Runtime transitions through `STARTING` → `ACTIVE`

***

## Update Runtime / Deploy a New Version

Each update creates a new immutable **Version**. The DEFAULT Endpoint automatically points to the latest version — the old version continues serving traffic until the deployment completes.

**Runtime topology with multiple versions:**

```
Runtime: my-order-agent
│
├── Versions
│   ├── Version 1  (image: my-agent:v1.0.0)
│   └── Version 2  (image: my-agent:v2.0.0)  ← latest
│
├── Endpoints
│   ├── DEFAULT  → https://<default-url>   (auto-tracks latest version)
│   └── canary   → https://<canary-url>    (pinned to Version 1)
│
└── Autoscaling: min=1, max=3, CPU threshold=50%
```

### Via Portal

**Step 1:** Open Runtime Detail → click **Edit**

**Step 2:** Change Image URL, Flavor, autoscaling, or environment variables → **Save**

### Via API

> Note: All fields (except `imageAuth`) are required in the PATCH body.

```bash
curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "description": "Production order agent v2",
    "imageUrl": "vcr.vngcloud.vn/<repo-backendName>/my-agent:v2.0.0",
    "imageAuth": {
      "enabled": true,
      "username": "<robot-backendName>",
      "password": "<robot-secret>"
    },
    "command": [],
    "args": [],
    "environmentVariables": {"LOG_LEVEL": "info"},
    "flavorId": "1x1-general",
    "autoscaling": {
      "minReplicas": 1,
      "maxReplicas": 3,
      "cpuUtilization": 50,
      "memoryUtilization": 50
    }
  }' | jq .
```

***

## Manage Endpoints

Each Runtime has one **DEFAULT** Endpoint created automatically. You can create additional Endpoints pinned to specific versions for canary or staging traffic.

### Via Portal

**View Endpoints:** Open Runtime Detail → **Endpoints** tab

![Runtime detail — Endpoints tab](<../../../../.gitbook/assets/1774594267224 (2).png>)

**Create a new Endpoint:**

1. **Endpoints** tab → click **Create Endpoint**
2. Enter **Name** and select **Version** → **Create**

**Change an Endpoint's version:**

1. **Endpoints** tab → click an endpoint → **Edit**
2. Select a new **Version** → **Save**

### Via API

**List Endpoints:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints?page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

Fields returned: `id`, `agentRuntimeId`, `name`, `version`, `url`, `status`, `createdAt`, `updatedAt`

**Create an Endpoint:**

```bash
curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "canary", "version": 2}' | jq .
```

**Update an Endpoint's version:**

```bash
curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID?version=3" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Delete an Endpoint:**

```bash
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID" \
  -H "Authorization: Bearer $TOKEN"
```

***

## View Versions and Rollback

Each update creates a new immutable Version. To roll back, point the DEFAULT Endpoint to an older version number.

### Via Portal

Open Runtime Detail → **Versions** tab

![Runtime detail — Versions tab](<../../../../.gitbook/assets/1774594455831 (2).png>)

### Via API

**List versions:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/versions?page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

Fields returned: `agentRuntimeId`, `version` (integer), `imageUrl`, `flavorId`, `autoscaling`, `createdAt`

**Rollback to an older version:**

```bash
ENDPOINT_ID=$(curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints?page=1&size=10" \
  -H "Authorization: Bearer $TOKEN" | jq -r '.listData[] | select(.name=="DEFAULT") | .id')

curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID?version=1" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

***

## Delete a Runtime

{% hint style="warning" %}
Deleting a Runtime is **irreversible**. All versions, Endpoints, and logs are permanently deleted.
{% endhint %}

### Via Portal

**Step 1:** Open **Agent Runtime** → locate the Runtime to delete

**Step 2:** Click **Delete** → review the warning → confirm

### Via API

```bash
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID" \
  -H "Authorization: Bearer $TOKEN"
```

***

## Reset Service Account

If IAM service account credentials are changed or revoked, use this to recover the Runtime:

```bash
curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/reset-service-account" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

{% hint style="warning" %}
This regenerates `GREENNODE_CLIENT_ID` and `GREENNODE_CLIENT_SECRET`. The Runtime restarts with new credentials.
{% endhint %}

***

## Next Steps

| I want to...          | Go to                                                                                                             |
| --------------------- | ----------------------------------------------------------------------------------------------------------------- |
| View logs and metrics | [Insight](logs-and-metrics.md)                                                                                    |
| Configure MCP Gateway | [MCP Governance](https://github.com/vngcloud/docs/blob/main/English/ai-stack/agent-base/mcp-governance/README.md) |
