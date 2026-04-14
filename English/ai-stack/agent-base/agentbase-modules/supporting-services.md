# Supporting Services

> This chapter covers the services and tools that support your agent workflow — container image storage (vCR), LLM model access (AIP), the Python SDK, and security best practices. These are not core AgentBase modules, but you will need them to build and deploy agents.

---


## Container Registry (vCR)

- **Portal:** https://vcr.console.vngcloud.vn
- **API Base URL:** `https://vcr.api.vngcloud.vn`
- **Registry Host:** `vcr.vngcloud.vn`

> **Note:** vCR pagination is **1-indexed** (`page=1` is first page). Image paths use the repository's `backendName` (not the display name): `vcr.vngcloud.vn/{backendName}/{imageName}:{tag}`

---

### Create a Repository

#### Portal (GUI)

1. Open https://vcr.console.vngcloud.vn → **"Create Repository"**
2. Fill in:
   - **Repository Name**: e.g., `my-first-agent` (unique, lowercase, alphanumeric and hyphens)
   - **Access**: Private (recommended)
   - **Quota Limit**: e.g., `10` GB
3. Click **Create**
4. Note the **backendName** from the repository detail — use this in image paths

#### RESTful API

> **Prerequisite:** All API examples below use `$TOKEN` — an IAM bearer token. See [Configure Authentication](getting-started.md#configure-authentication) for how to obtain it.

```bash
TOKEN=$(bash .claude/skills/agentbase/scripts/get_token.sh)

# Create repository
curl -s -X POST "https://vcr.api.vngcloud.vn/v1/repository" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "repoName": "my-first-agent",
    "isPublic": false,
    "quotaLimit": 10
  }' | jq .
```

**Response includes `backendName`** — use this in Docker image paths.

---

### Create a Robot Account

Robot accounts are service accounts for Docker push/pull access.

#### Portal (GUI)

1. On the repository detail page → **"Robot Accounts"** → **"Create Robot Account"**
2. Fill in: **Name**, **Duration** (days), **Permissions** (push + pull)
3. Click **Create**
4. **Immediately copy the Secret Key** — shown only once
5. The full username (`backendName`) has format: `{prefix}-{chosen-name}` (e.g., `109072-deploy-bot`)

#### RESTful API

```bash
# Step 1: Get available permissions — note the UUIDs from the response
curl -s "https://vcr.api.vngcloud.vn/v1/user/permissions" \
  -H "Authorization: Bearer $TOKEN" | jq .
# Response contains objects with "uuid" and "name" fields (e.g., "Push repository", "Pull repository")

PULL_UUID="<uuid where name='Pull repository'>"
PUSH_UUID="<uuid where name='Push repository'>"
REPO_ID="<id from the repository creation response above>"

# Step 2: Create robot account
curl -s -X POST "https://vcr.api.vngcloud.vn/v1/user" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "deploy-bot",
    "description": "CI/CD deployment account",
    "duration": 365,
    "permissionRequestList": [
      {
        "repoId": "'"$REPO_ID"'",
        "policyIdList": ["'"$PULL_UUID"'", "'"$PUSH_UUID"'"]
      }
    ]
  }' | jq .
```

**Response includes `secretKey`** — save it immediately, cannot be retrieved again.

```bash
# Step 3: Get the full backendName (username for docker login)
curl -s "https://vcr.api.vngcloud.vn/v1/user?page=1&size=50" \
  -H "Authorization: Bearer $TOKEN" | jq '.listData[] | select(.name | endswith("deploy-bot")) | .backendName'
```

---

### Push & Pull Images

```bash
REGISTRY="vcr.vngcloud.vn"
REPO_BACKEND="<repo-backendName>"
ROBOT_USER="109072-deploy-bot"
ROBOT_PASS="<secret-key>"

# Login
docker login $REGISTRY -u $ROBOT_USER -p $ROBOT_PASS

# Build, tag, and push
docker build -t $REGISTRY/$REPO_BACKEND/my-agent:v1.0.0 .
docker push $REGISTRY/$REPO_BACKEND/my-agent:v1.0.0
```

**Use in Runtime (runtime creation):**

```json
{
  "imageUrl": "vcr.vngcloud.vn/<repo-backendName>/my-agent:v1.0.0",
  "imageAuth": {
    "enabled": true,
    "username": "109072-deploy-bot",
    "password": "<secret-key>"
  }
}
```

---

### Manage Images

**List images:**

```bash
# name= parameter is required (even empty) — omitting it causes 500
curl -s "https://vcr.api.vngcloud.vn/v1/repository/$REPO_ID/images?name=&page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Delete image:**

```bash
curl -s -X DELETE "https://vcr.api.vngcloud.vn/v1/repository/$REPO_ID/images/delete?imageName=my-agent" \
  -H "Authorization: Bearer $TOKEN"
```

**Delete repository:**

> **Important:** You MUST delete all images before deleting the repository.

```bash
# 1. List and delete all images first
curl -s "https://vcr.api.vngcloud.vn/v1/repository/$REPO_ID/images?name=&page=1&size=100" \
  -H "Authorization: Bearer $TOKEN" | jq '.listData[] | .name'

# 2. Delete each image
curl -s -X DELETE "https://vcr.api.vngcloud.vn/v1/repository/$REPO_ID/images/delete?imageName=<imageName>" \
  -H "Authorization: Bearer $TOKEN"

# 3. Delete repository
curl -s -X DELETE "https://vcr.api.vngcloud.vn/v1/repository/$REPO_ID" \
  -H "Authorization: Bearer $TOKEN"
```

---

### Known API Quirks

| Issue                                 | Workaround                                |
| ------------------------------------- | ----------------------------------------- |
| `name=` is required for list images | Always include `?name=` even if empty   |
| Pagination is 1-based                 | Use `page=1` — `page=0` returns 400  |
| Repo deletion fails if images exist   | Delete all images first, then delete repo |

---

### Troubleshooting

| Error               | Cause                               | Fix                                                    |
| ------------------- | ----------------------------------- | ------------------------------------------------------ |
| Docker push denied  | Robot account lacks push permission | Re-create with explicit push+pull permissions          |
| Docker login fails  | Wrong username format               | Use full `backendName` (e.g., `109072-deploy-bot`) |
| Repo deletion fails | Images still exist                  | Delete all images first                                |
| 400 on image list   | Missing `name=` param             | Always include `?name=` even if empty                |

---

## AI Platform (AIP) — LLM Access

- **Portal:** https://aiplatform.console.vngcloud.vn/models
- **Management API:** `https://aiplatform-hcm.api.vngcloud.vn`
- **LLM Endpoint:** `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` (OpenAI-compatible)

> **Note:** AIP uses **1-indexed** pagination (`page=1`). API key names must be `^[a-z0-9\-]{5,50}$`.

---

### Browse Models

#### Portal (GUI)

1. Open https://aiplatform.console.vngcloud.vn/models
2. Browse available models — click a model to see its `path` (used as the `model` parameter in API calls)

#### RESTful API

```bash
# List all enabled models
curl -s "https://aiplatform-hcm.api.vngcloud.vn/v1/models?page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq '.listData[] | {name, path, modelStatus, provider: .provider.name}'
```

> **Important:** Use the `path` field (not `code`) as the `model` parameter when calling the LLM endpoint.

---

### Create an API Key

> **Note:** API key creation is **async** — poll until status is `ACTIVE`.

#### Portal (GUI)

1. Open https://aiplatform.console.vngcloud.vn/models → **"API Keys"** → **"Create API Key"**
2. Enter a **Name** (5–50 lowercase chars/digits/hyphens) → **Create**
3. Wait for status `ACTIVE` → copy the key value

#### RESTful API

```bash
# Create key
curl -s -X POST "https://aiplatform-hcm.api.vngcloud.vn/v1/api-keys" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "my-agent-key"}' | jq .

# Poll until ACTIVE
while true; do
  STATUS=$(curl -s "https://aiplatform-hcm.api.vngcloud.vn/v1/api-keys/my-agent-key" \
    -H "Authorization: Bearer $TOKEN" | jq -r '.data.status')
  echo "Status: $STATUS"
  [ "$STATUS" = "ACTIVE" ] && break
  sleep 3
done

# Get the key value
AIP_KEY=$(curl -s "https://aiplatform-hcm.api.vngcloud.vn/v1/api-keys/my-agent-key" \
  -H "Authorization: Bearer $TOKEN" | jq -r '.data.key')
```

---

### Call LLM Models

**Python (OpenAI SDK):**

```python
from openai import OpenAI

client = OpenAI(
    api_key="<your-aip-api-key>",
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
)

response = client.chat.completions.create(
    model="<model-path-from-detail>",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Hello!"},
    ],
)
print(response.choices[0].message.content)
```

**curl:**

```bash
curl -s -X POST "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions" \
  -H "Authorization: Bearer $AIP_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "<model-path>",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Hello!"}
    ]
  }' | jq .
```

---

### Troubleshooting

| Error              | Cause                      | Fix                                                |
| ------------------ | -------------------------- | -------------------------------------------------- |
| 401 on LLM call    | Invalid or expired AIP key | Check key status, create new key if needed         |
| Model not found    | Wrong `model` parameter  | Use `path` field from model detail, not `code` |
| API key quota full | Too many keys              | Delete unused key, then create new one             |

---

## SDK & Integration

### Installation

```bash
# Main SDK
pip install greennode-agentbase

# LangGraph / LangChain bridge (for checkpointer and short-term memory)
pip install "greennode-agent-bridge[langgraph]"
```

---

### Authentication Setup

The SDK reads credentials in this priority order:

1. **Environment variables** (highest priority):

```bash
export GREENNODE_CLIENT_ID="<your-client-id>"
export GREENNODE_CLIENT_SECRET="<your-client-secret>"
export GREENNODE_AGENT_IDENTITY="<your-agent-identity-name>"   # optional for local dev
```

2. **`.greennode.json`** in the current working directory (fallback):

```json
{
  "client_id": "<your-client-id>",
  "client_secret": "<your-client-secret>"
}
```

**On AgentBase Runtime:** `GREENNODE_CLIENT_ID`, `GREENNODE_CLIENT_SECRET`, and `GREENNODE_AGENT_IDENTITY` are **automatically injected** by the runtime.

```python
from greennode_agentbase import IAMCredentials

creds = IAMCredentials()  # auto-loads from env vars or .greennode.json
```

---

### Building an Agent with `GreenNodeAgentBaseApp`

`GreenNodeAgentBaseApp` is the SDK's built-in web server. It handles port binding, health check routing, and request dispatch.

```python
import os
from greennode_agentbase import GreenNodeAgentBaseApp, RequestContext, PingStatus

app = GreenNodeAgentBaseApp()

@app.ping
def health() -> PingStatus:
    return PingStatus.HEALTHY

@app.entrypoint
def handler(payload: dict, context: RequestContext) -> dict:
    user_input = payload.get("input", "")
    return {"output": f"Echo: {user_input}"}

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=int(os.environ.get("PORT", "8080")))
```

**`RequestContext` fields:**

| Field                  | Maps to Header                       | Description                                      |
| ---------------------- | ------------------------------------ | ------------------------------------------------ |
| `context.user_id`    | `X-GreenNode-AgentBase-User-Id`    | End-user identifier (for Memory `actor_id`)    |
| `context.session_id` | `X-GreenNode-AgentBase-Session-Id` | Session identifier (for LangGraph `thread_id`) |

---

### Credential Injection Decorators

```python
from greennode_agentbase import requires_api_key, requires_access_token

# Static API key
@app.entrypoint
@requires_api_key(provider_name="openai-key")
def handler(payload: dict, context: RequestContext, openai_key: str) -> dict:
    from openai import OpenAI
    client = OpenAI(api_key=openai_key)
    ...

# OAuth2 access token
@app.entrypoint
@requires_access_token(provider_name="google-oauth")
def handler(payload: dict, context: RequestContext, google_token: str) -> dict:
    import httpx
    resp = httpx.get("https://api.google.com/...", headers={"Authorization": f"Bearer {google_token}"})
    ...
```

---

### Identity Client (`IdentityClient`)

```python
from greennode_agentbase import IdentityClient, IAMCredentials
from greennode_agentbase.identity import (
    CreateAgentIdentityRequest,
    CreateApikeyProviderRequest,
    CreateOauth2ProviderRequest,
    GetM2mTokenRequest,
)
import asyncio

client = IdentityClient(iam_credentials=IAMCredentials())

# Identity operations (0-indexed pagination)
identity = asyncio.run(client.create_agent_identity_async(
    request=CreateAgentIdentityRequest(name="my-agent", description="My agent")
))
result = asyncio.run(client.list_agent_identities_async(page=0, size=20))
identity = asyncio.run(client.get_agent_identity_async(name="my-agent"))
asyncio.run(client.delete_agent_identity_async(name="my-agent"))

# Auth provider operations
provider = asyncio.run(client.create_api_key_provider_async(
    request=CreateApikeyProviderRequest(name="openai-key", apikey="sk-proj-xxx")
))
result = asyncio.run(client.get_api_key_for_agent_identity_async(
    provider_name="openai-key",
    agent_identity_name="my-agent",
))
print(result.apikey)
```

---

### Memory Client (`MemoryClient`)

```python
from greennode_agentbase.memory import MemoryClient
from greennode_agentbase.memory.models import (
    MemoryCreateRequest,
    LongTermMemoryStrategy,
    MemoryRecordSearchRequest,
)
import asyncio

client = MemoryClient()

# Create memory
memory = asyncio.run(client.create_async(
    request=MemoryCreateRequest(
        name="my-memory",
        eventExpiryDuration=30,
        longTermMemoryStrategies=[
            LongTermMemoryStrategy(
                name="semantic-facts",
                type="SEMANTIC",
                namespaceTemplate="/strategies/{memoryStrategyId}/actors/{actorId}",
                enableAutomaticMemoryRecordGeneration=True,
            ),
        ],
    )
))

# List (1-indexed)
result = asyncio.run(client.list_async(page=1, size=10))

# Semantic search
results = asyncio.run(client.searchMemoryRecords_async(
    id="<memory-id>",
    namespace="/strategies/<strategy-id>/actors/<actor-id>",
    request=MemoryRecordSearchRequest(query="user preferences", limit=10, scoreThreshold=0.5),
))
for record in results:
    print(f"[{record.score:.2f}] {record.memory}")
```

---

### LangGraph Integration (`AgentBaseMemoryEvents`)

```python
from greennode_agent_bridge import AgentBaseMemoryEvents
from langgraph.prebuilt import create_react_agent

checkpointer = AgentBaseMemoryEvents(memory_id="<memory-id>")

agent = create_react_agent(llm, tools=[], checkpointer=checkpointer)

result = agent.invoke(
    {"messages": [("human", "Hello")]},
    config={"configurable": {"thread_id": context.session_id}},
)
```

> For the complete pattern (short-term + long-term memory in a single agent), see [Memory § 6.10](./memory/README.md#advanced-add-conversation-memory-to-a-langgraph-agent).

---

## Security Best Practices

### IAM Permissions

All AgentBase operations require a GreenNode IAM service account. See [Getting Started](./getting-started.md#prerequisites) for setup steps.

**Recommended policies:**

| Policy                   | Description                                           | Typical User                |
| ------------------------ | ----------------------------------------------------- | --------------------------- |
| `AgentBaseFullAccess`  | Full access to Identity, Runtime, and Memory services | Developers, platform team   |
| `vcrFullAccess`        | Full access to Container Registry                     | Build pipelines, developers |
| `AiPlatformFullAccess` | Access to AI Platform LLM models and API keys         | Developers, agents          |

**Principle of least privilege:**

- Use service accounts over personal accounts — never use personal API keys in CI/CD
- Separate service accounts per environment (dev/prod)
- Rotate keys regularly
- Never share service account credentials

**Auto-injected credentials on Runtime (no manual setup needed):**

| Variable                     | Description                       |
| ---------------------------- | --------------------------------- |
| `GREENNODE_CLIENT_ID`      | IAM service account client ID     |
| `GREENNODE_CLIENT_SECRET`  | IAM service account client secret |
| `GREENNODE_AGENT_IDENTITY` | Agent identity name               |

---

### Credential Management

```python
# WRONG: Hardcoded API key in source code
client = OpenAI(api_key="sk-proj-hardcoded-key")

# WRONG: API key in Dockerfile
# ENV OPENAI_API_KEY=sk-proj-xxxx

# CORRECT: Use @requires_api_key — key fetched from Access Control
@app.entrypoint
@requires_api_key(provider_name="openai-key")
def handler(payload: dict, context: RequestContext, openai_key: str) -> dict:
    client = OpenAI(api_key=openai_key, ...)
```

**Secrets lifecycle:**

```
1. OBTAIN   → Get API key from external service (e.g., OpenAI dashboard)
2. REGISTER → Store in Access Control via Portal, REST API, or SDK (encrypted at rest)
3. USE      → Agent retrieves at runtime via @requires_api_key (injected automatically)
4. ROTATE   → Update via Portal or REST API when key expires or is compromised
5. RETIRE   → Delete provider when integration is removed
```

---

### Developer Workstation Security

**Gitignore rules for AgentBase projects:**

```gitignore
# AgentBase local credentials
.greennode.json
.greennode_token_cache

# Environment files
.env
.env.local
*.env

# vCR credentials
.vcr-credentials.json

# Service account keys
*-sa-key.json
service-account*.json
```

**Credential storage guide:**

| Credential Type                     | Where to Store                                      | NOT Here                     |
| ----------------------------------- | --------------------------------------------------- | ---------------------------- |
| IAM `client_id`/`client_secret` | Env vars or `.greennode.json`                     | Dockerfile, source code, git |
| LLM API key (AIP)                   | `.env` (local dev) or Access Control (production) | Dockerfile, source code, git |
| vCR robot account password          | `GREENNODE_VCR_PASSWORD` env var (CI)             | Source code, git             |
| External API keys (OpenAI, etc.)    | AgentBase Access Control as auth providers          | Anywhere in code or config   |

**Pre-commit hook to prevent secret commits:**

```bash
pip install detect-secrets
detect-secrets scan > .secrets.baseline

cat > .pre-commit-config.yaml << 'EOF'
repos:
  - repo: https://github.com/Yelp/detect-secrets
    rev: v1.4.0
    hooks:
      - id: detect-secrets
        args: ['--baseline', '.secrets.baseline']
EOF

pre-commit install
```

---

### Credential Rotation

**Rotate a static API key (takes effect on next request):**

```bash
TOKEN=$(bash .claude/skills/agentbase/scripts/get_token.sh)

curl -s -X PUT "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/api-key-providers/openai-key" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"apikey": "sk-proj-NEW-key-value"}' | jq .
```

**Reset IAM service account credentials:**

1. Go to https://iam.console.vngcloud.vn/service-accounts
2. Click the service account → **"Security credentials"** tab → **"Reset"**
3. Copy the new client secret (shown only once)
4. Update `GREENNODE_CLIENT_SECRET` in your environment

**Reset runtime service account (if runtime credentials are compromised):**

```bash
curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/reset-service-account" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

> **Warning:** This regenerates credentials for the runtime — the container will restart with new credentials.

---

