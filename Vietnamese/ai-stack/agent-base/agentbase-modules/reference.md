# Tham Khảo

> Tài liệu tham khảo đầy đủ cho tất cả API endpoint của AgentBase, quy ước phân trang, biến môi trường, SDK import, và giới hạn nền tảng.

---


## URL Dịch Vụ

### Portal Console

| Dịch vụ                   | URL                                              |
| ------------------------- | ------------------------------------------------ |
| IAM Service Accounts      | https://iam.console.vngcloud.vn/service-accounts |
| IAM Policies              | https://iam.console.vngcloud.vn/policies         |
| Access Control (Identity) | https://aiplatform.console.vngcloud.vn/identity  |
| Runtime          | https://aiplatform.console.vngcloud.vn/runtime   |
| Memory          | https://aiplatform.console.vngcloud.vn/memory    |
| Container Registry (vCR)  | https://vcr.console.vngcloud.vn                  |
| AI Platform (AIP) Models  | https://aiplatform.console.vngcloud.vn/models    |

### API Base URL

| Dịch vụ                           | Base URL                                               |
| --------------------------------- | ------------------------------------------------------ |
| Access Control                    | `https://agentbase.api.vngcloud.vn/identity/api/v1`  |
| Runtime                           | `https://agentbase.api.vngcloud.vn/runtime`          |
| Memory                            | `https://agentbase.api.vngcloud.vn/memory`           |
| Container Registry (vCR)          | `https://vcr.api.vngcloud.vn`                        |
| AIP Management                    | `https://aiplatform-hcm.api.vngcloud.vn`             |
| LLM Inference (tương thích OpenAI) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| Registry Host (Docker)            | `vcr.vngcloud.vn`                                    |

---

## API Endpoint Theo Dịch Vụ

### Access Control (`https://agentbase.api.vngcloud.vn/identity/api/v1`)

**Agent Identity:**

| Phương thức     | Đường dẫn                                 | Mô tả                 |
| ---------- | ------------------------------------ | --------------------------- |
| `POST`   | `/agent-identities`                | Tạo identity             |
| `GET`    | `/agent-identities?page=0&size=20` | Liệt kê identity (bắt đầu từ 0) |
| `GET`    | `/agent-identities/{name}`         | Lấy identity                |
| `PUT`    | `/agent-identities/{name}`         | Cập nhật identity             |
| `DELETE` | `/agent-identities/{name}`         | Xóa identity             |

**Static API Key Provider:**

| Phương thức     | Đường dẫn                                                                             | Mô tả         |
| ---------- | -------------------------------------------------------------------------------- | ------------------- |
| `POST`   | `/outbound-auth/api-key-providers`                                             | Tạo provider     |
| `GET`    | `/outbound-auth/api-key-providers?page=0&size=20`                              | Liệt kê provider      |
| `GET`    | `/outbound-auth/api-key-providers/{name}`                                      | Lấy provider        |
| `PUT`    | `/outbound-auth/api-key-providers/{name}`                                      | Cập nhật (xoay vòng key) |
| `DELETE` | `/outbound-auth/api-key-providers/{name}`                                      | Xóa provider     |
| `GET`    | `/outbound-auth/api-key-providers/{name}/agent-identities/{agentName}/api-key` | Truy xuất key        |

**Delegated API Key Provider:**

| Phương thức     | Đường dẫn                                                                                       | Mô tả           |
| ---------- | ------------------------------------------------------------------------------------------ | --------------------- |
| `POST`   | `/outbound-auth/delegated-api-key-providers`                                             | Tạo provider       |
| `GET`    | `/outbound-auth/delegated-api-key-providers?page=0&size=20`                              | Liệt kê provider        |
| `GET`    | `/outbound-auth/delegated-api-key-providers/{name}`                                      | Lấy provider          |
| `DELETE` | `/outbound-auth/delegated-api-key-providers/{name}`                                      | Xóa provider       |
| `POST`   | `/outbound-auth/delegated-api-key-providers/{name}/agent-identities/{agentName}/api-key` | Yêu cầu delegated key |

**OAuth2 Provider:**

| Phương thức     | Đường dẫn                                                                               | Mô tả     |
| ---------- | ---------------------------------------------------------------------------------- | --------------- |
| `POST`   | `/outbound-auth/oauth2-providers`                                                | Tạo provider |
| `GET`    | `/outbound-auth/oauth2-providers?page=0&size=20`                                 | Liệt kê provider  |
| `GET`    | `/outbound-auth/oauth2-providers/{name}`                                         | Lấy provider    |
| `PUT`    | `/outbound-auth/oauth2-providers/{name}`                                         | Cập nhật provider |
| `DELETE` | `/outbound-auth/oauth2-providers/{name}`                                         | Xóa provider |
| `POST`   | `/outbound-auth/oauth2-providers/{name}/agent-identities/{agentName}/tokens/m2m` | Lấy M2M token   |
| `POST`   | `/outbound-auth/oauth2-providers/{name}/agent-identities/{agentName}/tokens/3lo` | Lấy 3LO token   |

---

### Runtime (`https://agentbase.api.vngcloud.vn/runtime`)

**Agent Runtime:**

| Phương thức     | Đường dẫn                                           | Mô tả                          |
| ---------- | ---------------------------------------------- | ------------------------------------ |
| `POST`   | `/agent-runtimes`                            | Tạo runtime                       |
| `GET`    | `/agent-runtimes?page=1&size=20`             | Liệt kê runtime (bắt đầu từ 1)            |
| `GET`    | `/agent-runtimes/{id}`                       | Lấy runtime                          |
| `PATCH`  | `/agent-runtimes/{id}`                       | Cập nhật runtime (tạo phiên bản mới) |
| `DELETE` | `/agent-runtimes/{id}`                       | Xóa runtime                       |
| `PATCH`  | `/agent-runtimes/{id}/reset-service-account` | Đặt lại credential IAM                |

**Endpoint:**

| Phương thức     | Đường dẫn                                                      | Mô tả             |
| ---------- | --------------------------------------------------------- | ----------------------- |
| `GET`    | `/agent-runtimes/{id}/endpoints?page=1&size=20`         | Liệt kê endpoint          |
| `POST`   | `/agent-runtimes/{id}/endpoints`                        | Tạo endpoint         |
| `PATCH`  | `/agent-runtimes/{id}/endpoints/{endpointId}?version=N` | Cập nhật phiên bản endpoint |
| `DELETE` | `/agent-runtimes/{id}/endpoints/{endpointId}`           | Xóa endpoint         |

**Phiên bản:**

| Phương thức  | Đường dẫn                                             | Mô tả   |
| ------- | ------------------------------------------------ | ------------- |
| `GET` | `/agent-runtimes/{id}/versions?page=1&size=20` | Liệt kê phiên bản |

**Flavor:**

| Phương thức  | Đường dẫn         | Mô tả          |
| ------- | ------------ | -------------------- |
| `GET` | `/flavors` | Liệt kê flavor tính toán |

**Insight (Log & Metric):**

| Phương thức   | Đường dẫn                                                    | Mô tả         |
| -------- | ------------------------------------------------------- | ------------------- |
| `POST` | `/agent-runtimes/{id}/logs`                           | Lấy log runtime    |
| `POST` | `/agent-runtimes/{id}/endpoints/{endpointId}/logs`    | Lấy log endpoint   |
| `GET`  | `/agent-runtimes/{id}/endpoints/{endpointId}/metrics` | Lấy metric CPU/RAM |

---

### Memory (`https://agentbase.api.vngcloud.vn/memory`)

**Memory:**

| Phương thức     | Đường dẫn                                           | Mô tả               |
| ---------- | ---------------------------------------------- | ------------------------- |
| `POST`   | `/memories`                                  | Tạo memory             |
| `GET`    | `/memories?page=1&size=10`                   | Liệt kê memory (bắt đầu từ 1) |
| `GET`    | `/memories/{id}`                             | Lấy memory                |
| `DELETE` | `/memories/{id}`                             | Xóa memory             |
| `GET`    | `/memories/{id}/long-term-memory-strategies` | Liệt kê chiến lược           |

**Event:**

| Phương thức   | Đường dẫn                                                                           | Mô tả  |
| -------- | ------------------------------------------------------------------------------ | ------------ |
| `POST` | `/memories/{id}/actors/{actorId}/sessions/{sessionId}/events`                | Tạo event |
| `GET`  | `/memories/{id}/actors/{actorId}/sessions/{sessionId}/events?page=1&size=20` | Liệt kê event  |
| `GET`  | `/memories/{id}/actors?page=1&size=10`                                       | Liệt kê actor  |

**Memory Record:**

| Phương thức   | Đường dẫn                                                                                                  | Mô tả           |
| -------- | ----------------------------------------------------------------------------------------------------- | --------------------- |
| `GET`  | `/memories/{id}/memory-records?namespace=<encoded>&limit=100`                                       | Duyệt record        |
| `POST` | `/memories/{id}/memory-records:search?namespace=<encoded>`                                          | Tìm kiếm ngữ nghĩa       |
| `POST` | `/memories/{id}/memory-records:generate-from-session?actorId=&sessionId=&longTermMemoryStrategyId=` | Tạo từ phiên |

---

### Container Registry (`https://vcr.api.vngcloud.vn`)

| Phương thức     | Đường dẫn                                                       | Mô tả                       |
| ---------- | ---------------------------------------------------------- | --------------------------------- |
| `GET`    | `/v1/repository?page=1&size=50`                          | Liệt kê repository                 |
| `POST`   | `/v1/repository`                                         | Tạo repository                 |
| `GET`    | `/v1/repository/{repoId}`                                | Lấy repository                    |
| `DELETE` | `/v1/repository/{repoId}`                                | Xóa repository (phải trống) |
| `GET`    | `/v1/user?page=1&size=50`                                | Liệt kê robot account               |
| `POST`   | `/v1/user`                                               | Tạo robot account              |
| `GET`    | `/v1/user/permissions`                                   | Liệt kê quyền có sẵn        |
| `DELETE` | `/v1/user/{repoUserId}`                                  | Xóa robot account              |
| `GET`    | `/v1/repository/{repoId}/images?name=&page=1&size=10`    | Liệt kê image                       |
| `DELETE` | `/v1/repository/{repoId}/images/delete?imageName={name}` | Xóa image                      |

---

### AI Platform (`https://aiplatform-hcm.api.vngcloud.vn`)

| Phương thức     | Đường dẫn                            | Mô tả                          |
| ---------- | ------------------------------- | ------------------------------------ |
| `GET`    | `/v1/api-keys?page=1&size=20` | Liệt kê API key                        |
| `POST`   | `/v1/api-keys`                | Tạo API key (bất đồng bộ)               |
| `GET`    | `/v1/api-keys/{name}`         | Lấy API key (kiểm tra cho đến khi ACTIVE)        |
| `PUT`    | `/v1/api-keys/{name}`         | Cập nhật API key                       |
| `DELETE` | `/v1/api-keys/{name}`         | Xóa API key (bất đồng bộ, kiểm tra cho đến khi 404) |
| `GET`    | `/v1/models?page=1&size=20`   | Liệt kê mô hình                          |
| `GET`    | `/v1/models/detail/{uuid}`    | Lấy chi tiết mô hình                     |

**LLM Inference (tương thích OpenAI):**

| Phương thức   | Đường dẫn                     | Mô tả     |
| -------- | ------------------------ | --------------- |
| `POST` | `/v1/chat/completions` | Chat completion |
| `POST` | `/v1/completions`      | Text completion |
| `POST` | `/v1/embeddings`       | Embedding      |

Base URL cho inference: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1`

---

## Phân trang (Pagination Reference)

> **Quan trọng:** Quy ước phân trang khác nhau giữa các dịch vụ. Sử dụng sai chỉ số trang sẽ gây ra kết quả trống không mong muốn hoặc lỗi 400.

| Dịch vụ        | Trang đầu tiên | Key mục     | Key đếm          | Key trang       |
| -------------- | ---------- | ------------- | ------------------ | --------------- |
| Access Control | `page=0` | `.content`  | `.totalElements` | `.totalPages` |
| Runtime        | `page=1` | `.listData` | `.totalItem`     | `.totalPage`  |
| Memory         | `page=1` | `.listData` | `.totalItem`     | `.totalPage`  |
| vCR            | `page=1` | `.listData` | `.totalItem`     | `.totalPage`  |
| AIP            | `page=1` | `.listData` | `.totalItem`     | `.totalPage`  |

---

## Cấu trúc phản hồi (Response Shape Reference)

**Access Control (kiểu Spring):**

```json
{
  "content": [...],
  "totalElements": 5,
  "totalPages": 1,
  "size": 20,
  "number": 0
}
```

**Runtime / Memory / vCR / AIP (kiểu GreenNode):**

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

## Xác thực (Authentication)

Tất cả lệnh gọi API đều yêu cầu một GreenNode IAM bearer token:

```bash
Authorization: Bearer <token>
```

**Lấy token:** Xem [Cấu hình Xác thực](getting-started.md#configure-authentication) để biết chi tiết thiết lập đầy đủ. Tham khảo nhanh:

```bash
TOKEN=$(curl -s -X POST "https://iam.api.vngcloud.vn/accounts-api/v2/auth/token" \
  -u "$GREENNODE_CLIENT_ID:$GREENNODE_CLIENT_SECRET" \
  -d "grant_type=client_credentials" \
  -H "Content-Type: application/x-www-form-urlencoded" | jq -r '.access_token')
```

**Hết hạn token:** Token có thời hạn ngắn. Khi gặp lỗi 401, hãy lấy token mới.

---

## SDK Import

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

## Biến môi trường tự động (Auto-Injected Environment Variables)

Khi agent được triển khai trên AgentBase Runtime, các biến môi trường sau được tự động inject:

| Biến                     | Mô tả                       | Được sử dụng bởi                         |
| ---------------------------- | --------------------------------- | ------------------------------- |
| `GREENNODE_CLIENT_ID`      | Client ID tài khoản dịch vụ IAM     | Tự động xác thực SDK                   |
| `GREENNODE_CLIENT_SECRET`  | Client secret tài khoản dịch vụ IAM | Tự động xác thực SDK                   |
| `GREENNODE_AGENT_IDENTITY` | Tên agent identity               | Xác thực SDK + truy xuất credential |

---

## Hợp đồng dịch vụ Runtime (Runtime Service Contract)

Container agent của bạn phải đáp ứng các yêu cầu sau:

| Yêu cầu        | Giá trị                                  |
| ------------------ | -------------------------------------- |
| Cổng lắng nghe        | `8080` (bắt buộc)                    |
| Health check       | `GET /health` phải trả về HTTP 200   |
| Khởi động SDK server | `app.run(host="0.0.0.0", port=8080)` |

**Header request đến (khi sử dụng Memory):**

| Header                               | Mô tả                              |
| ------------------------------------ | ---------------------------------------- |
| `X-GreenNode-AgentBase-User-Id`    | ID người dùng cuối → `actor_id` cho memory    |
| `X-GreenNode-AgentBase-Session-Id` | ID phiên → `thread_id` cho LangGraph |

---

## Giới hạn nền tảng (Platform Limits)

### Access Control

| Giới hạn                         | Giá trị                |
| ----------------------------- | -------------------- |
| Độ dài tối đa tên identity      | 50 ký tự             |
| Mẫu tên identity         | `^[a-zA-Z0-9_-]+$` |
| Độ dài tối đa tên auth provider | 50 ký tự             |
| Mẫu tên auth provider    | `^[a-zA-Z0-9_-]+$` |

### Runtime

| Giới hạn                              | Giá trị   |
| ---------------------------------- | ------- |
| Số replica tối thiểu                       | 1       |
| Số replica tối đa                       | 10      |
| Phạm vi ngưỡng sử dụng CPU    | 25–75% |
| Phạm vi ngưỡng sử dụng Memory | 25–75% |
| Offset log tối đa (`from`)          | 5000    |
| Giới hạn log tối đa (`limit`)          | 1000    |

### Memory

| Giới hạn                                    | Giá trị                 |
| ---------------------------------------- | --------------------- |
| Độ dài tối đa tên memory                   | 50 ký tự              |
| Mẫu tên memory                      | `^[a-zA-Z0-9._-]*$` |
| Phạm vi thời hạn hết hạn event              | 1–365 ngày           |
| Phạm vi `limit` tìm kiếm ngữ nghĩa          | 5–200                |
| Phạm vi `scoreThreshold` tìm kiếm ngữ nghĩa | 0.0–1.0              |

### Container Registry (vCR)

| Giới hạn                                   | Giá trị                        |
| --------------------------------------- | ---------------------------- |
| Trang đầu tiên phân trang                   | `page=1` (0 trả về 400)   |
| Tham số `name=` bắt buộc khi liệt kê image | Có, kể cả khi để trống           |
| Xóa repo                           | Phải xóa tất cả image trước |

### AI Platform (AIP)

| Giới hạn                | Giá trị                      |
| -------------------- | -------------------------- |
| Mẫu tên API key | `^[a-z0-9\-]{5,50}$`     |
| Tạo API key     | Bất đồng bộ — kiểm tra cho đến khi ACTIVE |
| Xóa API key     | Bất đồng bộ — kiểm tra cho đến khi 404    |

---

