# Reference

> Complete reference for all AgentBase API endpoints, pagination conventions, environment variables, SDK imports, and platform limits.

---


## Service URLs

### Portal Consoles

| Service                   | URL                                              |
| ------------------------- | ------------------------------------------------ |
| IAM Service Accounts      | https://iam.console.vngcloud.vn/service-accounts |
| IAM Policies              | https://iam.console.vngcloud.vn/policies         |
| Access Control (Identity) | https://aiplatform.console.vngcloud.vn/identity  |
| Runtime          | https://aiplatform.console.vngcloud.vn/runtime   |
| Memory          | https://aiplatform.console.vngcloud.vn/memory    |
| Container Registry (vCR)  | https://vcr.console.vngcloud.vn                  |
| AI Platform (AIP) Models  | https://aiplatform.console.vngcloud.vn/models    |

### API Base URLs

| Service                           | Base URL                                               |
| --------------------------------- | ------------------------------------------------------ |
| Access Control                    | `https://agentbase.api.vngcloud.vn/identity/api/v1`  |
| Runtime                           | `https://agentbase.api.vngcloud.vn/runtime`          |
| Memory                            | `https://agentbase.api.vngcloud.vn/memory`           |
| Container Registry (vCR)          | `https://vcr.api.vngcloud.vn`                        |
| AIP Management                    | `https://aiplatform-hcm.api.vngcloud.vn`             |
| LLM Inference (OpenAI-compatible) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| Registry Host (Docker)            | `vcr.vngcloud.vn`                                    |

---

## API Endpoints by Service

### Access Control (`https://agentbase.api.vngcloud.vn/identity/api/v1`)

**Agent Identities:**

| Method     | Path                                 | Description                 |
| ---------- | ------------------------------------ | --------------------------- |
| `POST`   | `/agent-identities`                | Create identity             |
| `GET`    | `/agent-identities?page=0&size=20` | List identities (0-indexed) |
| `GET`    | `/agent-identities/{name}`         | Get identity                |
| `PUT`    | `/agent-identities/{name}`         | Update identity             |
| `DELETE` | `/agent-identities/{name}`         | Delete identity             |

**Static API Key Providers:**

| Method     | Path                                                                             | Description         |
| ---------- | -------------------------------------------------------------------------------- | ------------------- |
| `POST`   | `/outbound-auth/api-key-providers`                                             | Create provider     |
| `GET`    | `/outbound-auth/api-key-providers?page=0&size=20`                              | List providers      |
| `GET`    | `/outbound-auth/api-key-providers/{name}`                                      | Get provider        |
| `PUT`    | `/outbound-auth/api-key-providers/{name}`                                      | Update (rotate key) |
| `DELETE` | `/outbound-auth/api-key-providers/{name}`                                      | Delete provider     |
| `GET`    | `/outbound-auth/api-key-providers/{name}/agent-identities/{agentName}/api-key` | Retrieve key        |

**Delegated API Key Providers:**

| Method     | Path                                                                                       | Description           |
| ---------- | ------------------------------------------------------------------------------------------ | --------------------- |
| `POST`   | `/outbound-auth/delegated-api-key-providers`                                             | Create provider       |
| `GET`    | `/outbound-auth/delegated-api-key-providers?page=0&size=20`                              | List providers        |
| `GET`    | `/outbound-auth/delegated-api-key-providers/{name}`                                      | Get provider          |
| `DELETE` | `/outbound-auth/delegated-api-key-providers/{name}`                                      | Delete provider       |
| `POST`   | `/outbound-auth/delegated-api-key-providers/{name}/agent-identities/{agentName}/api-key` | Request delegated key |

**OAuth2 Providers:**

| Method     | Path                                                                               | Description     |
| ---------- | ---------------------------------------------------------------------------------- | --------------- |
| `POST`   | `/outbound-auth/oauth2-providers`                                                | Create provider |
| `GET`    | `/outbound-auth/oauth2-providers?page=0&size=20`                                 | List providers  |
| `GET`    | `/outbound-auth/oauth2-providers/{name}`                                         | Get provider    |
| `PUT`    | `/outbound-auth/oauth2-providers/{name}`                                         | Update provider |
| `DELETE` | `/outbound-auth/oauth2-providers/{name}`                                         | Delete provider |
| `POST`   | `/outbound-auth/oauth2-providers/{name}/agent-identities/{agentName}/tokens/m2m` | Get M2M token   |
| `POST`   | `/outbound-auth/oauth2-providers/{name}/agent-identities/{agentName}/tokens/3lo` | Get 3LO token   |

---

### Runtime (`https://agentbase.api.vngcloud.vn/runtime`)

**Agent Runtimes:**

| Method     | Path                                           | Description                          |
| ---------- | ---------------------------------------------- | ------------------------------------ |
| `POST`   | `/agent-runtimes`                            | Create runtime                       |
| `GET`    | `/agent-runtimes?page=1&size=20`             | List runtimes (1-indexed)            |
| `GET`    | `/agent-runtimes/{id}`                       | Get runtime                          |
| `PATCH`  | `/agent-runtimes/{id}`                       | Update runtime (creates new version) |
| `DELETE` | `/agent-runtimes/{id}`                       | Delete runtime                       |
| `PATCH`  | `/agent-runtimes/{id}/reset-service-account` | Reset IAM credentials                |

**Endpoints:**

| Method     | Path                                                      | Description             |
| ---------- | --------------------------------------------------------- | ----------------------- |
| `GET`    | `/agent-runtimes/{id}/endpoints?page=1&size=20`         | List endpoints          |
| `POST`   | `/agent-runtimes/{id}/endpoints`                        | Create endpoint         |
| `PATCH`  | `/agent-runtimes/{id}/endpoints/{endpointId}?version=N` | Update endpoint version |
| `DELETE` | `/agent-runtimes/{id}/endpoints/{endpointId}`           | Delete endpoint         |

**Versions:**

| Method  | Path                                             | Description   |
| ------- | ------------------------------------------------ | ------------- |
| `GET` | `/agent-runtimes/{id}/versions?page=1&size=20` | List versions |

**Flavors:**

| Method  | Path         | Description          |
| ------- | ------------ | -------------------- |
| `GET` | `/flavors` | List compute flavors |

**Insight (Logs & Metrics):**

| Method   | Path                                                    | Description         |
| -------- | ------------------------------------------------------- | ------------------- |
| `POST` | `/agent-runtimes/{id}/logs`                           | Get runtime logs    |
| `POST` | `/agent-runtimes/{id}/endpoints/{endpointId}/logs`    | Get endpoint logs   |
| `GET`  | `/agent-runtimes/{id}/endpoints/{endpointId}/metrics` | Get CPU/RAM metrics |

---

### Memory (`https://agentbase.api.vngcloud.vn/memory`)

**Memories:**

| Method     | Path                                           | Description               |
| ---------- | ---------------------------------------------- | ------------------------- |
| `POST`   | `/memories`                                  | Create memory             |
| `GET`    | `/memories?page=1&size=10`                   | List memories (1-indexed) |
| `GET`    | `/memories/{id}`                             | Get memory                |
| `DELETE` | `/memories/{id}`                             | Delete memory             |
| `GET`    | `/memories/{id}/long-term-memory-strategies` | List strategies           |

**Events:**

| Method   | Path                                                                           | Description  |
| -------- | ------------------------------------------------------------------------------ | ------------ |
| `POST` | `/memories/{id}/actors/{actorId}/sessions/{sessionId}/events`                | Create event |
| `GET`  | `/memories/{id}/actors/{actorId}/sessions/{sessionId}/events?page=1&size=20` | List events  |
| `GET`  | `/memories/{id}/actors?page=1&size=10`                                       | List actors  |

**Memory Records:**

| Method   | Path                                                                                                  | Description           |
| -------- | ----------------------------------------------------------------------------------------------------- | --------------------- |
| `GET`  | `/memories/{id}/memory-records?namespace=<encoded>&limit=100`                                       | Browse records        |
| `POST` | `/memories/{id}/memory-records:search?namespace=<encoded>`                                          | Semantic search       |
| `POST` | `/memories/{id}/memory-records:generate-from-session?actorId=&sessionId=&longTermMemoryStrategyId=` | Generate from session |

---

### Container Registry (`https://vcr.api.vngcloud.vn`)

| Method     | Path                                                       | Description                       |
| ---------- | ---------------------------------------------------------- | --------------------------------- |
| `GET`    | `/v1/repository?page=1&size=50`                          | List repositories                 |
| `POST`   | `/v1/repository`                                         | Create repository                 |
| `GET`    | `/v1/repository/{repoId}`                                | Get repository                    |
| `DELETE` | `/v1/repository/{repoId}`                                | Delete repository (must be empty) |
| `GET`    | `/v1/user?page=1&size=50`                                | List robot accounts               |
| `POST`   | `/v1/user`                                               | Create robot account              |
| `GET`    | `/v1/user/permissions`                                   | List available permissions        |
| `DELETE` | `/v1/user/{repoUserId}`                                  | Delete robot account              |
| `GET`    | `/v1/repository/{repoId}/images?name=&page=1&size=10`    | List images                       |
| `DELETE` | `/v1/repository/{repoId}/images/delete?imageName={name}` | Delete image                      |

---

### AI Platform (`https://aiplatform-hcm.api.vngcloud.vn`)

| Method     | Path                            | Description                          |
| ---------- | ------------------------------- | ------------------------------------ |
| `GET`    | `/v1/api-keys?page=1&size=20` | List API keys                        |
| `POST`   | `/v1/api-keys`                | Create API key (async)               |
| `GET`    | `/v1/api-keys/{name}`         | Get API key (poll for ACTIVE)        |
| `PUT`    | `/v1/api-keys/{name}`         | Update API key                       |
| `DELETE` | `/v1/api-keys/{name}`         | Delete API key (async, poll for 404) |
| `GET`    | `/v1/models?page=1&size=20`   | List models                          |
| `GET`    | `/v1/models/detail/{uuid}`    | Get model detail                     |

**LLM Inference (OpenAI-compatible):**

| Method   | Path                     | Description     |
| -------- | ------------------------ | --------------- |
| `POST` | `/v1/chat/completions` | Chat completion |
| `POST` | `/v1/completions`      | Text completion |
| `POST` | `/v1/embeddings`       | Embeddings      |

Base URL for inference: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1`

---

## Pagination Reference

> **Critical:** Pagination conventions differ across services. Using the wrong page index causes unexpected empty results or 400 errors.

| Service        | First Page | Items Key     | Count Key          | Pages Key       |
| -------------- | ---------- | ------------- | ------------------ | --------------- |
| Access Control | `page=0` | `.content`  | `.totalElements` | `.totalPages` |
| Runtime        | `page=1` | `.listData` | `.totalItem`     | `.totalPage`  |
| Memory         | `page=1` | `.listData` | `.totalItem`     | `.totalPage`  |
| vCR            | `page=1` | `.listData` | `.totalItem`     | `.totalPage`  |
| AIP            | `page=1` | `.listData` | `.totalItem`     | `.totalPage`  |

---

## Response Shape Reference

**Access Control (Spring-style):**

```json
{
  "content": [...],
  "totalElements": 5,
  "totalPages": 1,
  "size": 20,
  "number": 0
}
```

**Runtime / Memory / vCR / AIP (GreenNode-style):**

```json
{
  "listData": [...],
  "page": 1,
  "pageSize": 20,
  "totalPage": 1,
  "totalItem": 5
}
```

---

## Authentication

All API calls require a GreenNode IAM bearer token:

```bash
Authorization: Bearer <token>
```

**Get token:** See [Configure Authentication](getting-started.md#configure-authentication) for full setup. Quick reference:

```bash
TOKEN=$(curl -s -X POST "https://iam.api.vngcloud.vn/accounts-api/v2/auth/token" \
  -u "$GREENNODE_CLIENT_ID:$GREENNODE_CLIENT_SECRET" \
  -d "grant_type=client_credentials" \
  -H "Content-Type: application/x-www-form-urlencoded" | jq -r '.access_token')
```

**Token expiry:** Tokens are short-lived. On 401, re-obtain a fresh token.

---

## SDK Imports

```python
# Main AgentBase SDK
from greennode_agentbase import (
    GreenNodeAgentBaseApp,      # Web server for agent
    RequestContext,             # HTTP request metadata (user_id, session_id)
    PingStatus,                 # Health status enum (HEALTHY, HEALTHY_BUSY)
    IdentityClient,             # Access Control client
    MemoryClient,               # Memory service client
    IAMCredentials,             # IAM auth credentials
    requires_api_key,           # Decorator: inject static API key
    requires_access_token,      # Decorator: inject OAuth2 access token
)

# Access Control requests
from greennode_agentbase.identity import (
    CreateAgentIdentityRequest,
    UpdateAgentIdentityRequest,
    CreateApikeyProviderRequest,
    UpdateApikeyProviderRequest,
    CreateDelegatedApiKeyProviderRequest,
    CreateOauth2ProviderRequest,
    UpdateOauth2ProviderRequest,
    GetDelegatedApiKeyRequest,
    GetM2mTokenRequest,
    ThreeLoTokenRequest,
)

# Memory models
from greennode_agentbase.memory.models import (
    MemoryCreateRequest,
    LongTermMemoryStrategy,
    EventCreateRequest,
    ChatMessage,
    MemoryRecordSearchRequest,
)

# LangGraph bridge (short-term memory checkpointer)
from greennode_agent_bridge import AgentBaseMemoryEvents
```

---

## Auto-Injected Environment Variables

When an agent is deployed on AgentBase Runtime, these environment variables are automatically injected:

| Variable                     | Description                       | Used by                         |
| ---------------------------- | --------------------------------- | ------------------------------- |
| `GREENNODE_CLIENT_ID`      | IAM service account client ID     | SDK auto-auth                   |
| `GREENNODE_CLIENT_SECRET`  | IAM service account client secret | SDK auto-auth                   |
| `GREENNODE_AGENT_IDENTITY` | Agent identity name               | SDK auth + credential retrieval |

---

## Runtime Service Contract

Your agent container must meet these requirements:

| Requirement        | Value                                  |
| ------------------ | -------------------------------------- |
| Listen port        | `8080` (required)                    |
| Health check       | `GET /health` must return HTTP 200   |
| SDK server startup | `app.run(host="0.0.0.0", port=8080)` |

**Incoming request headers (when using Memory):**

| Header                               | Description                              |
| ------------------------------------ | ---------------------------------------- |
| `X-GreenNode-AgentBase-User-Id`    | End-user ID →`actor_id` for memory    |
| `X-GreenNode-AgentBase-Session-Id` | Session ID →`thread_id` for LangGraph |

---

## Platform Limits

### Access Control

| Limit                         | Value                |
| ----------------------------- | -------------------- |
| Identity name max length      | 50 chars             |
| Identity name pattern         | `^[a-zA-Z0-9_-]+$` |
| Auth provider name max length | 50 chars             |
| Auth provider name pattern    | `^[a-zA-Z0-9_-]+$` |

### Runtime

| Limit                              | Value   |
| ---------------------------------- | ------- |
| Min replicas                       | 1       |
| Max replicas                       | 10      |
| CPU utilization threshold range    | 25–75% |
| Memory utilization threshold range | 25–75% |
| Log offset max (`from`)          | 5000    |
| Log limit max (`limit`)          | 1000    |

### Memory

| Limit                                    | Value                 |
| ---------------------------------------- | --------------------- |
| Memory name max length                   | 50 chars              |
| Memory name pattern                      | `^[a-zA-Z0-9._-]*$` |
| Event expiry duration range              | 1–365 days           |
| Semantic search `limit` range          | 5–200                |
| Semantic search `scoreThreshold` range | 0.0–1.0              |

### Container Registry (vCR)

| Limit                                   | Value                        |
| --------------------------------------- | ---------------------------- |
| Pagination first page                   | `page=1` (0 returns 400)   |
| `name=` param required for image list | Yes, even if empty           |
| Repo deletion                           | Must delete all images first |

### AI Platform (AIP)

| Limit                | Value                      |
| -------------------- | -------------------------- |
| API key name pattern | `^[a-z0-9\-]{5,50}$`     |
| API key creation     | Async — poll until ACTIVE |
| API key deletion     | Async — poll until 404    |

---

