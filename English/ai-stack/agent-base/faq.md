# FAQ

> Frequently asked questions about GreenNode AgentBase.

---


## General

**Q: What programming language must my agent be written in?**

Your agent must be a containerized HTTP server listening on port 8080. The AgentBase SDK (`greennode-agentbase`) is Python-only. Most users write agents in Python using `GreenNodeAgentBaseApp` as the server framework.

---

**Q: Can I run my agent locally during development?**

Yes. Set `GREENNODE_CLIENT_ID` and `GREENNODE_CLIENT_SECRET` as environment variables (or use `.greennode.json` in your project root), then run the agent directly. Set `GREENNODE_AGENT_IDENTITY` to your dev agent identity name to enable credential retrieval.

```bash
export GREENNODE_CLIENT_ID="<your-client-id>"
export GREENNODE_CLIENT_SECRET="<your-client-secret>"
export GREENNODE_AGENT_IDENTITY="my-agent-dev"
python main.py
```

---

**Q: Can multiple runtimes share one identity?**

Yes. A single identity can be associated with multiple runtimes. All runtimes sharing an identity have access to the same auth configurations. If you need different credentials per environment, create separate identities (e.g., `my-agent-dev`, `my-agent-prod`).

---

**Q: What frameworks are officially supported?**

The SDK has first-class support for LangGraph via `AgentBaseMemoryEvents` (from `greennode-agent-bridge[langgraph]`). For the HTTP server layer, use `GreenNodeAgentBaseApp`. Any Python HTTP framework that listens on port 8080 and exposes `GET /health` returning HTTP 200 will work.

---

## Getting Started

**Q: What is the minimum setup required to deploy an agent?**

At minimum you need:

1. A GreenNode IAM service account
2. A registered **Agent Identity** ([Access Control](./access-control/README.md))
3. A Docker image in vCR ([Supporting Services](./supporting-services.md#container-registry-vcr))
4. A **Runtime** pointing to that image ([Runtime](./runtime/README.md))

You do not need Memory, auth configs, or external API integrations to run a basic echo agent.

---

**Q: Can I use a public Docker image instead of vCR?**

vCR is strongly recommended — images on vCR are on the same private network as runtime nodes (fast pulls, no egress cost). The Runtime can also pull from external registries if you configure `imageAuth`, but this introduces an external dependency in production.

---

**Q: How do I deploy a new version without downtime?**

Every `PATCH /agent-runtimes/{id}` creates a new version. The `DEFAULT` endpoint automatically updates to the latest version. To safely roll out with canary testing, create a separate endpoint pinned to the new version, test it, then update the `DEFAULT` endpoint. See [Runtime § 5.12](./runtime/README.md#advanced-canary-deployment).

---

## Access Control

**Q: Can I change an identity's name after creation?**

No. The identity name is immutable. If you need to rename, create a new identity with the desired name, re-register all auth configs, update your runtimes to use the new identity, then delete the old identity.

---

**Q: What happens if I try to delete an identity with active runtimes?**

The API will reject the delete request. Stop and delete all associated runtimes first, then delete the identity.

---

**Q: How do I verify that credential retrieval works before deployment?**

```python
# test_credentials.py
from greennode_agentbase import IdentityClient, IAMCredentials
import asyncio

client = IdentityClient(iam_credentials=IAMCredentials())

# List auth providers
result = asyncio.run(client.list_api_key_providers_async(page=0, size=20))
print(f"API key providers: {[p.name for p in result.content]}")

# Retrieve a specific key
key_result = asyncio.run(client.get_api_key_for_agent_identity_async(
    provider_name="openai-key",
    agent_identity_name="my-agent-dev",
))
print(f"Key retrieved: {'yes' if key_result.apikey else 'no'}")
```

---

## Runtime

**Q: What is the difference between a Runtime and an Endpoint?**

A **Runtime** is the compute environment (containers, scaling policy, flavor). An **Endpoint** is the HTTPS URL clients call. Every runtime automatically gets a `DEFAULT` endpoint. You can create additional endpoints pinned to specific versions for canary deployments.

---

**Q: What are the possible runtime states?**

| State        | Description                                                   |
| ------------ | ------------------------------------------------------------- |
| `CREATING` | Runtime is being created; containers are starting             |
| `ACTIVE`   | All minimum replicas are healthy; endpoint is serving traffic |
| `UPDATING` | A new version deployment is in progress                       |
| `ERROR`    | One or more required replicas could not start (check logs)    |
| `DELETING` | Runtime is being deleted                                      |

---

**Q: My agent keeps getting OOMKilled. What should I do?**

1. Check current memory usage via the metrics API:
   ```bash
   curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID/metrics" \
     -H "Authorization: Bearer $TOKEN" | jq '{cpu: .cpuCores, memory_mb: (.memoryBytes / 1048576 | floor)}'
   ```
2. Update to a larger flavor via `PATCH /agent-runtimes/{id}`
3. Optimize memory usage: reduce conversation history length, avoid loading large datasets in memory

---

**Q: How do I trigger a deployment from a CI pipeline?**

```bash
TOKEN=$(curl -s -X POST "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token" \
  -H "Content-Type: application/json" \
  -d "{\"grantType\": \"client_credentials\", \"clientId\": \"$GREENNODE_CLIENT_ID\", \"clientSecret\": \"$GREENNODE_CLIENT_SECRET\"}" \
  | jq -r '.data.accessToken')

curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d "{
    \"description\": \"\",
    \"imageUrl\": \"vcr.vngcloud.vn/my-repo/my-agent:${GIT_SHA}\",
    \"command\": [],
    \"args\": [],
    \"environmentVariables\": {},
    \"flavorId\": \"1x1-general\",
    \"autoscaling\": {\"minReplicas\": 1, \"maxReplicas\": 2, \"cpuUtilization\": 50, \"memoryUtilization\": 50}
  }"
```

---

## Memory

**Q: Is my conversation data private to my organization?**

Yes. Memory data (events and memory records) is isolated per organization.

---

**Q: What happens to memory data when I delete a runtime?**

Memory data is NOT deleted when you delete a runtime. It persists until:

- It expires (based on `eventExpiryDuration`, range 1–365 days)
- You explicitly delete the memory store (`DELETE /memories/{id}`)

---

**Q: My semantic search returns zero results. Why?**

Common causes:

1. **Namespace mismatch** — The namespace used for storing and searching must be identical.
2. **scoreThreshold too high** — Start with `"scoreThreshold": 0.0` to see all results, then increase.
3. **Records not yet generated** — Record generation is asynchronous. Wait a few seconds after posting events.
4. **Query is too different** — Semantic search finds similar meaning, not exact matches.

```bash
# Debug: browse all records in the namespace
NAMESPACE_ENCODED=$(python3 -c 'import urllib.parse; print(urllib.parse.quote("/strategies/<strategy-id>/actors/<actor-id>"))')
curl -s "https://agentbase.api.vngcloud.vn/memory/memories/$MEMORY_ID/memory-records?namespace=$NAMESPACE_ENCODED&limit=100" \
  -H "Authorization: Bearer $TOKEN" | jq '.[] | .memory'
```

---

**Q: What is the difference between short-term and long-term memory?**

|             | Short-Term                                       | Long-Term                                    |
| ----------- | ------------------------------------------------ | -------------------------------------------- |
| Storage     | Events (conversation turns) in order             | Memory records (extracted facts) as vectors  |
| Retrieval   | By actor + session                               | By semantic similarity search                |
| Expiry      | After `eventExpiryDuration` days               | Permanent until deleted                      |
| Use case    | Conversation history, LangGraph checkpointing    | User preferences, persistent facts           |
| Integration | `AgentBaseMemoryEvents` LangGraph checkpointer | `MemoryClient.searchMemoryRecords_async()` |

---

## SDK & Integration

**Q: What are the correct environment variable names for the SDK?**

| Variable                     | Description                                    |
| ---------------------------- | ---------------------------------------------- |
| `GREENNODE_CLIENT_ID`      | IAM service account client ID                  |
| `GREENNODE_CLIENT_SECRET`  | IAM service account client secret              |
| `GREENNODE_AGENT_IDENTITY` | Agent identity name (for credential retrieval) |

---

**Q: Can I use `@requires_api_key` for non-entrypoint functions?**

No. For other patterns, use `IdentityClient.get_api_key_for_agent_identity_async()`:

```python
from greennode_agentbase import IdentityClient, IAMCredentials
import asyncio, os

client = IdentityClient(iam_credentials=IAMCredentials())
result = asyncio.run(client.get_api_key_for_agent_identity_async(
    provider_name="openai-key",
    agent_identity_name=os.environ["GREENNODE_AGENT_IDENTITY"],
))
api_key = result.apikey
```

---

## Troubleshooting

**Q: My runtime is stuck in `CREATING` state. What do I do?**

1. Check runtime logs:
   ```bash
   curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/logs" \
     -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
     -d '{"from": 0, "limit": 100}' | jq -r '.logs[]'
   ```
2. Verify the image URL is correct and exists in vCR
3. Verify `imageAuth` credentials are correct for private registries
4. Verify the container exposes `GET /health` returning HTTP 200 on port 8080

---

**Q: I get 401 Unauthorized on API calls. How do I fix it?**

IAM tokens are short-lived. Re-obtain the token:

```bash
TOKEN=$(curl -s -X POST "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token" \
  -H "Content-Type: application/json" \
  -d '{"grantType": "client_credentials", "clientId": "'"$GREENNODE_CLIENT_ID"'", "clientSecret": "'"$GREENNODE_CLIENT_SECRET"'"}' \
  | jq -r '.data.accessToken')
```

---

**Q: My agent returns 500 errors but logs look normal. What should I check?**

1. Check endpoint logs (not just runtime logs):
   ```bash
   curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID/logs" \
     -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
     -d '{"from": 0, "limit": 200}' | jq -r '.logs[]' | grep -i "error\|traceback\|exception"
   ```
2. Verify `context.user_id` and `context.session_id` headers are present if using Context
3. Verify the `@app.ping` health check returns `PingStatus.HEALTHY`

---

## Teardown / Clean Up Resources

**Goal:** Remove all AgentBase resources for a project.

> **Warning:** This is irreversible. Runtimes, memory data, and auth configurations will be permanently deleted.

### Delete Order

Delete resources in this order to avoid dependency errors:

1. Delete runtime(s)
2. Delete auth providers
3. Delete agent identity
4. Delete memory store(s)
5. Delete vCR images and repository (optional)

---

### Step 1: Delete Runtime(s)

#### Portal (GUI)

1. Open https://aiplatform.console.vngcloud.vn/runtime → click the runtime → **"Delete"** → confirm

#### RESTful API

```bash
TOKEN=$(bash .claude/skills/agentbase/scripts/get_token.sh)
RUNTIME_ID="<your-runtime-id>"

# List runtimes to get IDs
curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes?page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq '.listData[] | {id, name, status}'

# Delete runtime
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID" \
  -H "Authorization: Bearer $TOKEN"
```

---

### Step 2: Delete Auth Providers

#### RESTful API

```bash
# List and delete API key providers
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/api-key-providers?page=0&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq '.content[] | {name}'

curl -s -X DELETE "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/api-key-providers/<provider-name>" \
  -H "Authorization: Bearer $TOKEN"

# List and delete OAuth2 providers
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/oauth2-providers?page=0&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq '.content[] | {name}'

curl -s -X DELETE "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/oauth2-providers/<provider-name>" \
  -H "Authorization: Bearer $TOKEN"
```

#### SDK

```python
from greennode_agentbase import IdentityClient, IAMCredentials
import asyncio

client = IdentityClient(iam_credentials=IAMCredentials())
asyncio.run(client.delete_api_key_provider_async(name="aip-key"))
asyncio.run(client.delete_oauth2_provider_async(name="google-oauth"))
```

---

### Step 3: Delete Agent Identity

#### Portal (GUI)

1. Open https://aiplatform.console.vngcloud.vn/identity → find the identity → **"Delete"** → confirm

#### RESTful API

```bash
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/identity/api/v1/agent-identities/<identity-name>" \
  -H "Authorization: Bearer $TOKEN"
```

#### SDK

```python
asyncio.run(client.delete_agent_identity_async(name="my-agent"))
```

---

### Step 4: Delete Memory Store(s)

#### Portal (GUI)

1. Open https://aiplatform.console.vngcloud.vn/memory → click the memory → **"Delete"** → confirm

#### RESTful API

```bash
MEMORY_ID="<your-memory-id>"

# List memories
curl -s "https://agentbase.api.vngcloud.vn/memory/memories?page=1&size=10" \
  -H "Authorization: Bearer $TOKEN" | jq '.listData[] | {id, name}'

# Delete memory
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/memory/memories/$MEMORY_ID" \
  -H "Authorization: Bearer $TOKEN"
```

#### SDK

```python
from greennode_agentbase.memory import MemoryClient
import asyncio

memory_client = MemoryClient()
asyncio.run(memory_client.delete_async(id="<memory-id>"))
```

---

### Step 5: Delete vCR Repository (Optional)

> **Important:** You must delete all images before deleting the repository.

#### Portal (GUI)

1. Open https://vcr.console.vngcloud.vn → navigate to the repository → delete all images first → delete the repository

#### RESTful API

```bash
REPO_ID="<your-repo-id>"

# List all images
curl -s "https://vcr.api.vngcloud.vn/v1/repository/$REPO_ID/images?name=&page=1&size=100" \
  -H "Authorization: Bearer $TOKEN" | jq '.listData[] | .name'

# Delete each image
curl -s -X DELETE "https://vcr.api.vngcloud.vn/v1/repository/$REPO_ID/images/delete?imageName=<image-name>" \
  -H "Authorization: Bearer $TOKEN"

# After all images are deleted, delete the repository
curl -s -X DELETE "https://vcr.api.vngcloud.vn/v1/repository/$REPO_ID" \
  -H "Authorization: Bearer $TOKEN"
```

---

### Verify Teardown

```bash
# No identities remaining
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/agent-identities?page=0&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq '.totalElements'

# No runtimes remaining
curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes?page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq '.totalItem'

# No memories remaining
curl -s "https://agentbase.api.vngcloud.vn/memory/memories?page=1&size=10" \
  -H "Authorization: Bearer $TOKEN" | jq '.totalItem'
```

---

