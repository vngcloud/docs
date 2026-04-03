# GreenNode AgentBase — Tổng quan Sản phẩm

> **Nguồn** : Tổng hợp từ `greennode-agentbase-skills-main` — bộ tài liệu kỹ thuật & Skills của sản phẩm.
> **Cập nhật** : 2026-03-23

---

## 1. AgentBase là gì?

**GreenNode AgentBase** là nền tảng hạ tầng chuyên biệt dành cho AI Agent của GreenNode (VNG Cloud).

Thay vì tự dựng server, tự quản lý credential, tự lo memory và scaling, developer chỉ cần viết code agent — AgentBase lo toàn bộ phần còn lại: deploy, scaling, identity, memory, observability.

 **Mô hình** : Developer đóng gói agent vào Docker image → đẩy lên AgentBase Runtime → platform tự quản lý vòng đời container, inject credentials, xử lý memory và cung cấp endpoint công khai để gọi agent.

---

## 2. Kiến trúc Tổng thể

```
┌──────────────────────────────────────────────────────┐
│                  GreenNode AgentBase                 │
│                                                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │
│  │  Identity   │  │   Runtime   │  │   Memory    │  │
│  │  Service    │  │   Service   │  │   Service   │  │
│  └─────────────┘  └─────────────┘  └─────────────┘  │
│                                                      │
│  ┌─────────────┐  ┌─────────────┐                   │
│  │ AI Platform │  │  Container  │                   │
│  │  (AIP/MAAS) │  │  Registry   │                   │
│  │             │  │   (vCR)     │                   │
│  └─────────────┘  └─────────────┘                   │
└──────────────────────────────────────────────────────┘
```

---

## 3. Các thành phần chính (Platform Components)

### 3.1 Identity Service

* **Vai trò** : Quản lý danh tính agent và xác thực ra ngoài (outbound auth)
* **Base URL** : `https://agentbase.api.vngcloud.vn/identity/api/v1`
* **Console** : [https://aiplatform.console.vngcloud.vn/identity](https://aiplatform.console.vngcloud.vn/identity)
* **Chức năng** :
* Đăng ký `Agent Identity` — định danh của một agent trên platform
* Lưu trữ API Key tĩnh cho external services (OpenAI, Slack, Google…)
* Hỗ trợ Delegated API Key (end-user tự cung cấp key)
* Hỗ trợ OAuth2 Provider (M2M token và 3-legged OAuth2)
* **Ghi chú** : Khi deploy lên Runtime, Identity & credentials được **tự động inject** vào container, không cần cấu hình thủ công trong code.

### 3.2 Runtime Service

* **Vai trò** : Triển khai agent dạng container với autoscaling, versioning, zero-downtime deploy
* **Base URL** : `https://agentbase.api.vngcloud.vn/runtime`
* **Console** : [https://aiplatform.console.vngcloud.vn/runtime](https://aiplatform.console.vngcloud.vn/runtime)
* **Chức năng** :
* Deploy agent từ Docker image → sinh ra `Runtime` với endpoint công khai
* Quản lý phiên bản (versions), canary deployment, rollback
* Autoscaling theo CPU/RAM threshold
* Tự động tạo `DEFAULT` endpoint khi tạo runtime
* **Yêu cầu container** (Runtime Service Contract):
  * Listen trên port `8080`
  * Expose `GET /health` → HTTP 200
  * Nhận request tại `POST /invocations`
  * Các env var quan trọng được  **tự động inject** : `GREENNODE_CLIENT_ID`, `GREENNODE_CLIENT_SECRET`, `GREENNODE_AGENT_IDENTITY`, `GREENNODE_ENDPOINT_URL`

### 3.3 Memory Service

* **Vai trò** : Lưu trữ lịch sử hội thoại (short-term) và trích xuất facts ngữ nghĩa (long-term)
* **Base URL** : `https://agentbase.api.vngcloud.vn/memory`
* **Console** : [https://aiplatform.console.vngcloud.vn/memory](https://aiplatform.console.vngcloud.vn/memory)
* **Hai loại memory** :

| Loại                                | Mô tả                                                | Thời hạn                                                 |
| ------------------------------------ | ------------------------------------------------------ | ---------------------------------------------------------- |
| **Short-term (Events)**        | Lịch sử hội thoại theo session                     | Hết hạn sau N ngày (cấu hình `eventExpiryDuration`) |
| **Long-term (Memory Records)** | Facts ngữ nghĩa được trích xuất từ hội thoại | Permanent                                                  |

* **Long-Term Memory Strategy (LTMS)** :
* `SEMANTIC` — Trích xuất fact chung
* `USER_PREFERENCE` — Học sở thích người dùng
* `CUSTOM` — Tùy chỉnh prompt trích xuất
* **SDK tích hợp** : `AgentBaseMemoryEvents` (LangChain/LangGraph checkpointer), `MemoryClient` (tool-based)

### 3.4 AI Platform — AIP (MAAS)

* **Vai trò** : Cung cấp LLM models và API keys với endpoint tương thích OpenAI
* **LLM Endpoint** : `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1`
* **Tương thích** : OpenAI SDK, LangChain, bất kỳ OpenAI-compatible client nào
* **Chức năng** :
* Tạo/quản lý API Keys để truy cập LLM
* Browse, enable/disable các LLM model
* Kiểm tra rate limit

### 3.5 Container Registry (vCR)

* **Vai trò** : Docker image registry riêng của GreenNode
* **Image path** : `vcr.vngcloud.vn/{repoBackendName}/{imageName}:{tag}`
* **Chức năng** :
* Quản lý repositories, robot accounts, permissions
* Tích hợp trực tiếp với Runtime Service khi deploy

---

## 4. Authentication & IAM

AgentBase dùng **IAM Service Account** làm cơ chế xác thực chính.

```
IAM Service Account
  ├── client_id     (luôn hiển thị)
  └── client_secret (chỉ hiển thị 1 lần khi tạo)
```

**Policies cần thiết** (gắn vào Service Account):

* `AgentBaseFullAccess` — truy cập Identity, Runtime, Memory
* `vcrFullAccess` — push/pull Docker image
* `AiPlatformFullAccess` — quản lý LLM models & API keys

 **Cách lưu credentials** :

1. Environment variables: `GREENNODE_CLIENT_ID`, `GREENNODE_CLIENT_SECRET`
2. File `.greennode.json` trong project directory (fallback)

 **Khi deploy lên Runtime** : Runtime tự động inject credentials vào container → agent code không cần cấu hình thủ công.

---

## 5. Developer Tooling — Skills

AgentBase cung cấp bộ **AI Skills** (dùng với Claude Code, Cursor, OpenAI Codex) để thao tác toàn bộ vòng đời agent qua natural language hoặc slash commands:

| # | Skill                   | Mục đích                                                                                          |
| - | ----------------------- | ---------------------------------------------------------------------------------------------------- |
| 1 | `/agentbase-wizard`   | **Guided wizard 9 bước**từ zero đến deployed agent — điểm khởi đầu cho người mới |
| 2 | `/agentbase`          | Platform reference, giải thích kiến trúc, IAM setup                                              |
| 3 | `/agentbase-manage`   | Quản lý Identity, Outbound Auth (API key, OAuth2), Memory                                          |
| 4 | `/aip`                | Tạo API key & browse LLM models trên AI Platform                                                   |
| 5 | `/agentbase-deploy`   | Deploy pipeline (build → push → create runtime → verify), quản lý runtime, vCR registry         |
| 6 | `/agentbase-monitor`  | Xem logs, metrics (CPU/RAM), dashboard tổng hợp                                                    |
| 7 | `/agentbase-teardown` | Xóa toàn bộ resources của một project (có dry-run)                                             |

 **Hỗ trợ tool** :

| Feature              | Claude Code              | Cursor (v2.4+)       | OpenAI Codex         |
| -------------------- | ------------------------ | -------------------- | -------------------- |
| Auto API calls       | Có                      | Không               | Giới hạn           |
| Full deploy pipeline | Có                      | Không               | Không               |
| Monitoring/Logs      | Có                      | Không               | Không               |
| **Best for**   | **Full lifecycle** | **Viết code** | **Viết code** |

> **Recommended workflow** : Viết code trong  **Cursor** , deploy & monitor bằng  **Claude Code** .

---

## 6. Vòng đời Agent (9 bước của Wizard)

```
Step 1: Check Prerequisites     → IAM credentials
Step 2: Scaffold Project        → Tạo cấu trúc project (Basic / LangChain / LangGraph)
Step 3: Set Up Memory           → Tạo Memory container (optional)
Step 4: Identity & External Auth → Đăng ký identity, lưu API keys external (optional)
Step 5: Customize Agent Code    → Viết/chỉnh logic agent
Step 6: Configure Environment   → Scan env vars, cấu hình LLM key, MEMORY_ID…
Step 7: Local Testing           → validate → local → docker → preflight
Step 8: Deploy                  → Build image → Push vCR → Create runtime → Verify
Step 9: Verify & Next Steps     → Health check, endpoint URL, hướng dẫn tiếp theo
```

---

## 7. Python SDK

### Package chính: `greennode-agentbase`

```python
from greennode_agentbase import (
    GreenNodeAgentBaseApp,   # Web server cho agent (FastAPI-style)
    RequestContext,          # HTTP request metadata (session_id, user_id...)
    PingStatus,              # Health status: HEALTHY / HEALTHY_BUSY
    IdentityClient,          # Gọi Identity Service API
    MemoryClient,            # Gọi Memory Service API
    IAMCredentials,          # Auth credentials wrapper
    requires_api_key,        # Decorator: tự inject API key từ Identity
    requires_access_token,   # Decorator: tự inject OAuth2 token
)
```

### Package bridge: `greennode-agent-bridge[langgraph]`

```python
from greennode_agent_bridge import (
    AgentBaseMemoryEvents,   # LangGraph CheckpointSaver (short-term memory)
)
```

 **Ví dụ skeleton agent (LangChain)** :

```python
from greennode_agentbase import GreenNodeAgentBaseApp, PingStatus, RequestContext
import os

app = GreenNodeAgentBaseApp()

@app.ping
async def health() -> PingStatus:
    return PingStatus.HEALTHY

@app.invoke
async def handle(payload: dict, context: RequestContext) -> dict:
    # Logic agent ở đây
    return {"response": "Hello!"}

if __name__ == "__main__":
    app.run()  # Tự bind port 8080
```

---

## 8. Frameworks hỗ trợ

AgentBase scaffold sẵn template cho 4 frameworks:

| Framework                    | Mô tả                                          |
| ---------------------------- | ------------------------------------------------ |
| **Basic**              | Thuần Python, tự viết logic                   |
| **LangChain**          | Recommended — dùng LangChain agents/chains     |
| **LangChain + Memory** | LangChain + AgentBase Memory (short + long term) |
| **LangGraph**          | Advanced — state machine graph                  |
| **LangGraph + Memory** | LangGraph + AgentBase CheckpointSaver            |

---

## 9. Ví dụ use-case

### Tạo chatbot từ đầu (quick path)

```bash
/agentbase-wizard init my-chatbot --langgraph   # Scaffold project
/aip api-keys create my-chatbot-key             # Lấy LLM API key
/agentbase-manage memory create                 # Tạo memory store
/agentbase-wizard test local                    # Test local
/agentbase-deploy deploy                        # Deploy lên cloud
/agentbase-monitor runtime-logs <id>            # Xem logs
```

### Debug agent đang chạy

```bash
/agentbase-monitor runtime-logs <runtime-id>
/agentbase-monitor endpoint-logs <runtime-id> <endpoint-id>
/agentbase-monitor metrics <runtime-id>
```

### Rollback version

```bash
# Xem danh sách versions
bash runtime.sh versions $RUNTIME_ID

# Update runtime về image cũ (tạo version mới, DEFAULT endpoint tự cập nhật)
bash runtime.sh update $RUNTIME_ID --image "<old-image-url>" --flavor "<flavor>"
```

---

## 10. Một số điểm kỹ thuật cần lưu ý

| Vấn đề                                  | Chi tiết                                                                             |
| ------------------------------------------ | ------------------------------------------------------------------------------------- |
| **Pagination không đồng nhất**   | Identity Service:`page`0-indexed; Runtime/Memory/vCR:`page`1-indexed              |
| **Response shape khác nhau**        | Identity:`.content`/`.totalElements`; Runtime/Memory:`.listData`/`.totalItem` |
| **Port bắt buộc**                  | Container PHẢI listen port `8080`                                                  |
| **Health endpoint bắt buộc**       | `GET /health`phải trả về HTTP 200                                                |
| **DEFAULT endpoint**                 | Không thể update trực tiếp — phải update runtime để tạo version mới         |
| **vCR "all permissions" bị lỗi**   | Chỉ dùng specific permissions (`pull`+`push`), không dùng "all"               |
| **Re-attach robot account bị lỗi** | Backend bug — dùng `PUT /v1/user/{id}/permission`thay thế                        |
| **Xóa repo cần rỗng trước**     | Phải xóa hết images trước khi xóa repository                                    |
| **Không commit `.env`**           | Chỉ commit `.env.example`                                                          |
| **Secret trong chat**                | KHÔNG paste secret vào chat — dùng env var hoặc file                             |

---

## 11. Console URLs tổng hợp

| Service              | URL                                                                                               |
| -------------------- | ------------------------------------------------------------------------------------------------- |
| AI Platform Console  | [https://aiplatform.console.vngcloud.vn](https://aiplatform.console.vngcloud.vn)                     |
| Identity             | [https://aiplatform.console.vngcloud.vn/identity](https://aiplatform.console.vngcloud.vn/identity)   |
| Runtime              | [https://aiplatform.console.vngcloud.vn/runtime](https://aiplatform.console.vngcloud.vn/runtime)     |
| Memory               | [https://aiplatform.console.vngcloud.vn/memory](https://aiplatform.console.vngcloud.vn/memory)       |
| LLM Models           | [https://aiplatform.console.vngcloud.vn/models](https://aiplatform.console.vngcloud.vn/models)       |
| IAM Service Accounts | [https://iam.console.vngcloud.vn/service-accounts](https://iam.console.vngcloud.vn/service-accounts) |
| IAM Policies         | [https://iam.console.vngcloud.vn/policies](https://iam.console.vngcloud.vn/policies)                 |

---

## 12. Positioning tóm tắt

> GreenNode AgentBase = **"Vercel/Railway dành riêng cho AI Agent"**
>
> Developer chỉ cần viết business logic của agent (LangChain/LangGraph/thuần Python), đóng gói Docker, rồi giao cho AgentBase lo toàn bộ infra: deploy, scaling, identity, memory, observability — tích hợp sẵn với LLM MAAS của VNG Cloud (OpenAI-compatible).
>
