# Dịch Vụ Hỗ Trợ

> Chương này trình bày các dịch vụ và công cụ hỗ trợ quy trình làm việc với agent của bạn — lưu trữ container image (vCR), truy cập mô hình LLM (AIP), Python SDK, và các phương pháp bảo mật tốt nhất. Đây không phải là các module chính của AgentBase, nhưng bạn sẽ cần chúng để xây dựng và triển khai agent.

---


## Container Registry (vCR)

- **Portal:** https://vcr.console.greennode.ai
- **API Base URL:** `https://vcr.api.vngcloud.vn`
- **Registry Host:** `vcr.vngcloud.vn`

> **Lưu ý:** Phân trang của vCR bắt đầu từ **1** (`page=1` là trang đầu tiên). Đường dẫn image sử dụng `backendName` của repository (không phải tên hiển thị): `vcr.vngcloud.vn/{backendName}/{imageName}:{tag}`

---

### Tạo Repository

#### Portal (GUI)

1. Mở https://vcr.console.greennode.ai → **"Create Repository"**
2. Điền thông tin:
   - **Repository Name**: ví dụ, `my-first-agent` (duy nhất, chữ thường, chữ cái, số và dấu gạch ngang)
   - **Access**: Private (khuyến nghị)
   - **Quota Limit**: ví dụ, `10` GB
3. Nhấn **Create**
4. Ghi lại **backendName** từ trang chi tiết repository — sử dụng tên này trong đường dẫn image

#### RESTful API

> **�Điều kiện cần:** Tất cả các ví dụ API dưới đây sử dụng `$TOKEN` — một IAM bearer token. Xem [Cấu hình Xác thực](getting-started.md#configure-authentication) để biết cách lấy token.

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

**Phản hồi bao gồm `backendName`** — sử dụng tên này trong đường dẫn Docker image.

---

### Tạo Robot Account

Robot account là các tài khoản dịch vụ dùng để push/pull Docker.

#### Portal (GUI)

1. Trên trang chi tiết repository → **"Robot Accounts"** → **"Create Robot Account"**
2. Điền thông tin: **Name**, **Duration** (ngày), **Permissions** (push + pull)
3. Nhấn **Create**
4. **Sao chép Secret Key ngay lập tức** — chỉ hiển thị một lần
5. Tên đầy đủ (`backendName`) có định dạng: `{prefix}-{chosen-name}` (ví dụ, `109072-deploy-bot`)

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

**Phản hồi bao gồm `secretKey`** — lưu lại ngay lập tức, không thể truy xuất lại.

```bash
# Step 3: Get the full backendName (username for docker login)
curl -s "https://vcr.api.vngcloud.vn/v1/user?page=1&size=50" \
  -H "Authorization: Bearer $TOKEN" | jq '.listData[] | select(.name | endswith("deploy-bot")) | .backendName'
```

---

### Push & Pull Image

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

**Sử dụng trong Runtime (tạo runtime):**

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

### Quản Lý Image

**Liệt kê image:**

```bash
# name= parameter is required (even empty) — omitting it causes 500
curl -s "https://vcr.api.vngcloud.vn/v1/repository/$REPO_ID/images?name=&page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Xóa image:**

```bash
curl -s -X DELETE "https://vcr.api.vngcloud.vn/v1/repository/$REPO_ID/images/delete?imageName=my-agent" \
  -H "Authorization: Bearer $TOKEN"
```

**Xóa repository:**

> **Quan trọng:** Bạn PHẢI xóa tất cả image trước khi xóa repository.

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

### Các Lỗi API Đã Biết

| Vấn đề                                | Cách khắc phục                            |
| ------------------------------------- | ----------------------------------------- |
| `name=` là bắt buộc khi liệt kê image | Luôn thêm `?name=` kể cả khi để trống   |
| Phân trang bắt đầu từ 1              | Dùng `page=1` — `page=0` trả về 400  |
| Xóa repo thất bại nếu còn image      | Xóa tất cả image trước, sau đó xóa repo |

---

### Xử Lý Sự Cố

| Lỗi                  | Nguyên nhân                         | Cách sửa                                                    |
| ------------------- | ----------------------------------- | ------------------------------------------------------ |
| Docker push bị từ chối  | Robot account thiếu quyền push | Tạo lại với quyền push+pull rõ ràng          |
| Docker login thất bại  | Sai định dạng username               | Dùng `backendName` đầy đủ (ví dụ, `109072-deploy-bot`) |
| Xóa repo thất bại | Vẫn còn image                  | Xóa tất cả image trước                                |
| 400 khi liệt kê image   | Thiếu tham số `name=`             | Luôn thêm `?name=` kể cả khi để trống                |

---

## AI Platform (AIP) — Truy cập LLM

- **Portal:** https://aiplatform.console.greennode.ai/models
- **Management API:** `https://aiplatform-hcm.api.vngcloud.vn`
- **LLM Endpoint:** `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` (tương thích OpenAI)

> **Lưu ý:** AIP sử dụng phân trang bắt đầu từ **1** (`page=1`). Tên API key phải tuân theo mẫu `^[a-z0-9\-]{5,50}$`.

---

### Duyệt Mô Hình

#### Portal (GUI)

1. Mở https://aiplatform.console.greennode.ai/models
2. Duyệt các mô hình có sẵn — nhấn vào một mô hình để xem `path` (dùng làm tham số `model` trong các lệnh gọi API)

#### RESTful API

```bash
# List all enabled models
curl -s "https://aiplatform-hcm.api.vngcloud.vn/v1/models?page=1&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq '.listData[] | {name, path, modelStatus, provider: .provider.name}'
```

> **Quan trọng:** Sử dụng trường `path` (không phải `code`) làm tham số `model` khi gọi LLM endpoint.

---

### Tạo API Key

> **Lưu ý:** Việc tạo API key là **bất đồng bộ** — hãy kiểm tra định kỳ cho đến khi trạng thái là `ACTIVE`.

#### Portal (GUI)

1. Mở https://aiplatform.console.greennode.ai/models → **"API Keys"** → **"Create API Key"**
2. Nhập **Name** (5–50 ký tự chữ thường/số/gạch ngang) → **Create**
3. Đợi trạng thái `ACTIVE` → sao chép giá trị key

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

### Gọi Mô Hình LLM

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

### Xử Lý Sự Cố

| Lỗi                 | Nguyên nhân                      | Cách sửa                                                |
| ------------------ | -------------------------- | -------------------------------------------------- |
| 401 khi gọi LLM    | AIP key không hợp lệ hoặc hết hạn | Kiểm tra trạng thái key, tạo key mới nếu cần         |
| Không tìm thấy mô hình    | Sai tham số `model`  | Dùng trường `path` từ chi tiết mô hình, không phải `code` |
| Hết quota API key | Quá nhiều key              | Xóa key không dùng, sau đó tạo key mới             |

---

## SDK & Tích hợp

### Cài Đặt

```bash
# Main SDK
pip install greennode-agentbase

# LangGraph / LangChain bridge (for checkpointer and short-term memory)
pip install "greennode-agent-bridge[langgraph]"
```

---

### Thiết Lập Xác Thực

SDK đọc thông tin xác thực theo thứ tự ưu tiên sau:

1. **Biến môi trường** (ưu tiên cao nhất):

```bash
export GREENNODE_CLIENT_ID="<your-client-id>"
export GREENNODE_CLIENT_SECRET="<your-client-secret>"
export GREENNODE_AGENT_IDENTITY="<your-agent-identity-name>"   # optional for local dev
```

2. **`.greennode.json`** trong thư mục làm việc hiện tại (dự phòng):

```json
{
  "client_id": "<your-client-id>",
  "client_secret": "<your-client-secret>"
}
```

**Trên AgentBase Runtime:** `GREENNODE_CLIENT_ID`, `GREENNODE_CLIENT_SECRET`, và `GREENNODE_AGENT_IDENTITY` được **tự động inject** bởi runtime.

```python
from greennode_agentbase import IAMCredentials

creds = IAMCredentials()  # auto-loads from env vars or .greennode.json
```

---

### Xây Dựng Agent với `GreenNodeAgentBaseApp`

`GreenNodeAgentBaseApp` là web server tích hợp sẵn của SDK. Nó xử lý việc bind cổng, định tuyến health check, và phân phối request.

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

**Các trường của `RequestContext`:**

| Trường                 | Tương ứng với Header                       | Mô tả                                      |
| ---------------------- | ------------------------------------ | ------------------------------------------------ |
| `context.user_id`    | `X-GreenNode-AgentBase-User-Id`    | Định danh người dùng cuối (cho `actor_id` của Memory)    |
| `context.session_id` | `X-GreenNode-AgentBase-Session-Id` | Định danh phiên (cho `thread_id` của LangGraph) |

---

### Decorator Inject Credential

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

### Tích Hợp LangGraph (`AgentBaseMemoryEvents`)

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

> Để xem mẫu hoàn chỉnh (short-term + long-term memory trong một agent), xem [Memory mục 6.10](./memory/README.md#advanced-add-conversation-memory-to-a-langgraph-agent).

---

## Các Phương Pháp Bảo Mật Tốt Nhất

### Quyền IAM

Tất cả thao tác AgentBase đều yêu cầu một tài khoản dịch vụ GreenNode IAM. Xem [Bắt đầu](./getting-started.md#prerequisites) để biết các bước thiết lập.

**Các chính sách khuyến nghị:**

| Chính sách                   | Mô tả                                           | Người dùng thường gặp                |
| ------------------------ | ----------------------------------------------------- | --------------------------- |
| `AgentBaseFullAccess`  | Toàn quyền truy cập dịch vụ Identity, Runtime, và Memory | Nhà phát triển, đội nền tảng   |
| `vcrFullAccess`        | Toàn quyền truy cập Container Registry                     | Pipeline build, nhà phát triển |
| `AiPlatformFullAccess` | Truy cập mô hình LLM và API key trên AI Platform         | Nhà phát triển, agent          |

**Nguyên tắc đặc quyền tối thiểu:**

- Sử dụng tài khoản dịch vụ thay vì tài khoản cá nhân — không bao giờ dùng API key cá nhân trong CI/CD
- Tách riêng tài khoản dịch vụ cho mỗi môi trường (dev/prod)
- Xoay vòng key định kỳ
- Không bao giờ chia sẻ thông tin xác thực của tài khoản dịch vụ

**Credential được tự động inject trên Runtime (không cần thiết lập thủ công):**

| Biến                     | Mô tả                       |
| ---------------------------- | --------------------------------- |
| `GREENNODE_CLIENT_ID`      | Client ID tài khoản dịch vụ IAM     |
| `GREENNODE_CLIENT_SECRET`  | Client secret tài khoản dịch vụ IAM |
| `GREENNODE_AGENT_IDENTITY` | Tên agent identity               |

---

### Quản Lý Credential

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

**Vòng đời secret:**

```
1. OBTAIN   → Lấy API key từ dịch vụ bên ngoài (ví dụ, bảng điều khiển OpenAI)
2. REGISTER → Lưu trữ trong Access Control qua Portal, REST API, hoặc SDK (mã hóa khi lưu)
3. USE      → Agent truy xuất lúc runtime qua @requires_api_key (tự động inject)
4. ROTATE   → Cập nhật qua Portal hoặc REST API khi key hết hạn hoặc bị lộ
5. RETIRE   → Xóa provider khi tích hợp được gỡ bỏ
```

---

### Bảo Mật Máy Trạm Phát Triển

**Quy tắc gitignore cho các dự án AgentBase:**

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

**Hướng dẫn lưu trữ credential:**

| Loại Credential                     | Nơi lưu trữ                                      | KHÔNG lưu ở đây                     |
| ----------------------------------- | --------------------------------------------------- | ---------------------------- |
| IAM `client_id`/`client_secret` | Biến môi trường hoặc `.greennode.json`                     | Dockerfile, mã nguồn, git |
| LLM API key (AIP)                   | `.env` (dev cục bộ) hoặc Access Control (production) | Dockerfile, mã nguồn, git |
| Mật khẩu robot account vCR          | Biến môi trường `GREENNODE_VCR_PASSWORD` (CI)             | Mã nguồn, git             |
| API key bên ngoài (OpenAI, v.v.)    | AgentBase Access Control dưới dạng auth provider          | Bất kỳ đâu trong code hoặc config   |

**Pre-commit hook để ngăn commit chứa secret:**

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

### Xoay Vòng Credential

**Xoay vòng static API key (có hiệu lực từ request tiếp theo):**

```bash
TOKEN=$(bash .claude/skills/agentbase/scripts/get_token.sh)

curl -s -X PUT "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/api-key-providers/openai-key" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"apikey": "sk-proj-NEW-key-value"}' | jq .
```

**Đặt lại credential tài khoản dịch vụ IAM:**

1. Truy cập https://iam.console.greennode.ai/service-accounts
2. Nhấn vào tài khoản dịch vụ → tab **"Security credentials"** → **"Reset"**
3. Sao chép client secret mới (chỉ hiển thị một lần)
4. Cập nhật `GREENNODE_CLIENT_SECRET` trong môi trường của bạn

**Đặt lại tài khoản dịch vụ runtime (nếu credential runtime bị lộ):**

```bash
curl -s -X PATCH "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/reset-service-account" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

> **Lưu ý:** Thao tác này tạo lại credential cho runtime — container sẽ khởi động lại với credential mới.

---

