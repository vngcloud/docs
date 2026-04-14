# Access Control

> Access Control là nền tảng của AgentBase. Nó bao gồm hai vấn đề liên quan mật thiết: **Agent Identity** (đăng ký agent của bạn trên nền tảng) và **Auth & Secrets** (lưu trữ và tiêm credential mà agent của bạn cần để gọi các dịch vụ bên ngoài).

- **Portal:** https://aiplatform.console.vngcloud.vn/access-control
- **API Base URL:** `https://agentbase.api.vngcloud.vn/identity/api/v1`

---

## Khái niệm cơ bản

### Identity là gì?

Trong AgentBase, một **Identity** là một bản ghi được quản lý bởi nền tảng, có tên duy nhất, đại diện cho agent của bạn trong tổ chức. Hãy xem nó như "tài khoản" của agent — là nền tảng mà mọi thứ khác được xây dựng trên đó. Một identity phải tồn tại trước khi có thể tạo Runtime cho agent đó, và trước khi bất kỳ auth credential nào có thể được truy xuất.

**Một identity bao gồm:**

- Một **tên duy nhất** (trong phạm vi tổ chức)
- **Mô tả** và metadata tùy chọn
- Danh sách các **cấu hình auth liên kết** (các credential mà identity này có thể truy xuất)

**Quy tắc đặt tên Identity:**

- 3–50 ký tự
- Chỉ cho phép chữ cái, số, dấu gạch dưới `_`, và dấu gạch ngang `-` (`^[a-zA-Z0-9_-]+$`)
- Phải duy nhất trong tổ chức

### Identity và Runtime

Một Identity là lâu dài và không phụ thuộc vào môi trường. Một Runtime gắn với một container image và cấu hình tính toán cụ thể. Nhiều runtime (ví dụ, `staging` và `production`) có thể dùng chung một identity.

```
Identity: my-order-agent (persistent)
     │
     ├─── Runtime: my-order-agent-staging  (environment-specific)
     └─── Runtime: my-order-agent-prod     (environment-specific)
```

### Xác thực chiều đi (Outbound Authentication)

Khi agent của bạn gọi các dịch vụ bên ngoài (OpenAI, Google, Slack, API nội bộ), nó cần credential. Hệ thống Auth của AgentBase cho phép bạn lưu trữ các credential này tập trung và tự động cung cấp cho agent tại thời điểm chạy — mà không cần mã cứng (hardcode) chúng.

Hệ thống auth hỗ trợ ba loại credential:

- **Static API Key** — Một chuỗi cố định (như API key) liên kết với một identity. Sử dụng khi dịch vụ bên ngoài cấp API key có thời hạn sử dụng dài và bạn muốn quản lý tập trung.
- **Delegated API Key** — Một credential có phạm vi giới hạn và có thể có thời hạn ngắn, hữu ích cho các kịch bản nhiều người thuê (multi-tenant) khi các agent khác nhau cần nhận các key có phạm vi khác nhau.
- **OAuth2 Provider** — Dành cho các dịch vụ sử dụng OAuth2 (Google, Slack, và các dịch vụ khác). AgentBase lưu trữ client credential và refresh token, đồng thời tự động xử lý việc làm mới token.

| Loại Provider              | Trường hợp sử dụng                              | Lưu trữ                      |
| --------------------------- | ---------------------------------------------------- | ------------------------------ |
| **Static API Key**    | Key có thời hạn dài (OpenAI, AIP, v.v.)          | Mã hóa khi lưu trữ         |
| **Delegated API Key** | Key liên kết người dùng cuối                   | Theo người dùng, liên kết |
| **OAuth2**            | Dịch vụ bên thứ ba (Google, GitHub, Slack, v.v.) | Mã hóa, tự động làm mới |

**Mô hình bảo mật:** Credential được lưu trữ trong HashiCorp Vault.

---

## Agent Identity

### Portal

#### Tạo một Identity

1. Mở https://aiplatform.console.vngcloud.vn/access-control
2. Nhấn **"Create Identity"**
3. Điền thông tin:
   - **Name** (bắt buộc): ví dụ, `my-order-agent` — chữ thường, chữ cái số và dấu gạch ngang
   - **Description** (tùy chọn): ví dụ, `Handles order inquiries`
   - **Allowed Return URLs** (tùy chọn): Các URL callback OAuth2 cho identity này
4. Nhấn **Create**
5. Identity mới xuất hiện trong danh sách với trạng thái `ACTIVE`

#### Xem danh sách Identity

1. Mở https://aiplatform.console.vngcloud.vn/access-control
2. Tất cả các identity được hiển thị trong danh sách phân trang

#### Xem chi tiết Identity

1. Mở https://aiplatform.console.vngcloud.vn/access-control
2. Nhấn vào tên identity

#### Cập nhật một Identity

1. Mở https://aiplatform.console.vngcloud.vn/access-control
2. Nhấn vào tên identity → **"Edit"**
3. Cập nhật mô tả hoặc allowed return URLs → **Save**

#### Xóa một Identity

> **Lưu ý:** Xóa một identity là **không thể khôi phục**. Hãy dừng tất cả các runtime liên kết và xóa tất cả cấu hình auth trước khi xóa.

1. Mở https://aiplatform.console.vngcloud.vn/access-control
2. Tìm identity → **Delete** → xác nhận

---

### RESTful API

> **�Điều kiện cần:** Tất cả các ví dụ API dưới đây sử dụng `$TOKEN` — một IAM bearer token. Xem [Configure Authentication](../getting-started.md#214-configure-authentication) để biết cách lấy token.

#### Tạo một Identity

```bash
curl -s -X POST "https://agentbase.api.vngcloud.vn/identity/api/v1/agent-identities" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "my-order-agent",
    "description": "Handles order inquiries via Salesforce",
    "allowedReturnUrls": []
  }' | jq .
```

**Ví dụ phản hồi:**

```json
{
  "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "name": "my-order-agent",
  "description": "Handles order inquiries via Salesforce",
  "allowedReturnUrls": [],
  "createdAt": "2026-03-18T09:00:00Z",
  "updatedAt": "2026-03-18T09:00:00Z"
}
```

**Lỗi: 409 Conflict** — tên đã tồn tại. Chọn một tên khác hoặc sử dụng identity hiện có.

#### Xem danh sách Identity

```bash
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/agent-identities?page=0&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Cấu trúc phản hồi:**

```json
{
  "content": [...],
  "totalElements": 3,
  "totalPages": 1,
  "size": 20,
  "number": 0
}
```

#### Xem chi tiết Identity

```bash
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/agent-identities/my-order-agent" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

#### Cập nhật một Identity

Bạn có thể cập nhật mô tả và allowed return URLs. **Tên và ID là không thể thay đổi**.

```bash
curl -s -X PUT "https://agentbase.api.vngcloud.vn/identity/api/v1/agent-identities/my-order-agent" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "description": "Handles order + returns inquiries via Salesforce",
    "allowedReturnUrls": ["https://myapp.com/callback"]
  }' | jq .
```

#### Xóa một Identity

> **Lưu ý:** Xóa một identity là **không thể khôi phục**.

```bash
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/identity/api/v1/agent-identities/my-order-agent" \
  -H "Authorization: Bearer $TOKEN"
```

---

### SDK

#### Tạo một Identity

```python
from greennode_agentbase import IdentityClient, IAMCredentials
from greennode_agentbase.identity import CreateAgentIdentityRequest
import asyncio

client = IdentityClient(iam_credentials=IAMCredentials())

identity = asyncio.run(client.create_agent_identity_async(
    request=CreateAgentIdentityRequest(
        name="my-order-agent",
        description="Handles order inquiries via Salesforce",
        allowed_return_urls=[],
    )
))
print(f"Name: {identity.name}, ID: {identity.id}")
```

> **Lưu ý:** `IAMCredentials()` không có tham số sẽ tự động tải từ các biến môi trường `GREENNODE_CLIENT_ID` / `GREENNODE_CLIENT_SECRET` hoặc `.greennode.json`.

#### Xem danh sách Identity

```python
result = asyncio.run(client.list_agent_identities_async(page=0, size=20))
for identity in result.content:
    print(f"{identity.name} (id: {identity.id})")
print(f"Total: {result.total_elements}")
```

#### Xem chi tiết Identity

```python
identity = asyncio.run(client.get_agent_identity_async(name="my-order-agent"))
print(f"Name: {identity.name}, ID: {identity.id}")
```

#### Cập nhật một Identity

```python
from greennode_agentbase.identity import UpdateAgentIdentityRequest

identity = asyncio.run(client.update_agent_identity_async(
    name="my-order-agent",
    request=UpdateAgentIdentityRequest(
        description="Handles order + returns inquiries via Salesforce",
        allowed_return_urls=["https://myapp.com/callback"],
    )
))
```

#### Xóa một Identity

```python
asyncio.run(client.delete_agent_identity_async(name="my-order-agent"))
```

---

## Auth & Secrets

Một **agent identity** phải tồn tại trước khi tạo auth provider. Nếu bạn chưa tạo, xem [4.3 Agent Identity](#43-agent-identity) ở trên.

### Portal

#### Static API Key Provider

1. Mở https://aiplatform.console.vngcloud.vn/access-control → **"Auth Providers"**
2. Nhấn **"Create Provider"** → chọn **"Static API Key"**
3. Điền **Name** (ví dụ, `openai-key`) và **giá trị API Key**
4. Nhấn **Create**

#### Delegated API Key Provider

1. Mở https://aiplatform.console.vngcloud.vn/access-control → **Auth Providers**
2. Nhấn **"Create Provider"** → chọn **"Delegated API Key"**
3. Nhập **Name** (ví dụ, `user-openai-key`) → **Create**

#### OAuth2 Provider

1. Mở https://aiplatform.console.vngcloud.vn/access-control → **Auth Providers**
2. Nhấn **"Create Provider"** → chọn **"OAuth2"**
3. Điền: **Name**, **Client ID**, **Client Secret**, **Authorization URL**, **Token URL**
4. Nhấn **Create** — phản hồi bao gồm một **Callback URL** để đăng ký trong ứng dụng OAuth2 của bạn

![1774593811794](../image/04-access-control/1774593811794.png)

---

### RESTful API

#### Static API Key Provider

**Tạo:**

```bash
curl -s -X POST "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/api-key-providers" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "openai-key",
    "apikey": "sk-proj-xxxxxxxxxxxxxxxxxxxx"
  }' | jq .
```

**Xem danh sách:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/api-key-providers?page=0&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Xem chi tiết:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/api-key-providers/openai-key" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Cập nhật (xoay key):**

```bash
curl -s -X PUT "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/api-key-providers/openai-key" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"apikey": "sk-proj-new-key-value"}' | jq .
```

**Xóa:**

```bash
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/api-key-providers/openai-key" \
  -H "Authorization: Bearer $TOKEN"
```

> **Lưu ý:** Xóa một provider sẽ lập tức thu hồi quyền truy cập của tất cả các agent đang chạy sử dụng nó.

#### Delegated API Key Provider

**Tạo:**

```bash
curl -s -X POST "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/delegated-api-key-providers" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "user-openai-key"}' | jq .
```

**Xem danh sách:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/delegated-api-key-providers?page=0&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Xem chi tiết:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/delegated-api-key-providers/user-openai-key" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Xóa:**

```bash
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/delegated-api-key-providers/user-openai-key" \
  -H "Authorization: Bearer $TOKEN"
```

#### OAuth2 Provider

**Tạo:**

```bash
curl -s -X POST "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/oauth2-providers" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "google-oauth",
    "clientId": "812345678901-abcdefg.apps.googleusercontent.com",
    "clientSecret": "GOCSPX-xxxxxxxxxxxx",
    "authorizationUrl": "https://accounts.google.com/o/oauth2/v2/auth",
    "tokenUrl": "https://oauth2.googleapis.com/token"
  }' | jq .
```

**Phản hồi bao gồm `callbackUrl` — hãy đăng ký URL này trong ứng dụng OAuth2 của bạn.**

**Xem danh sách:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/oauth2-providers?page=0&size=20" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Xem chi tiết:**

```bash
curl -s "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/oauth2-providers/google-oauth" \
  -H "Authorization: Bearer $TOKEN" | jq .
```

**Cập nhật:**

```bash
curl -s -X PUT "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/oauth2-providers/google-oauth" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "clientId": "new-client-id.apps.googleusercontent.com",
    "clientSecret": "GOCSPX-new-secret",
    "authorizationUrl": "https://accounts.google.com/o/oauth2/v2/auth",
    "tokenUrl": "https://oauth2.googleapis.com/token"
  }' | jq .
```

**Xóa:**

```bash
curl -s -X DELETE "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/oauth2-providers/google-oauth" \
  -H "Authorization: Bearer $TOKEN"
```

**Lấy OAuth2 Token (M2M):**

```bash
curl -s -X POST "https://agentbase.api.vngcloud.vn/identity/api/v1/outbound-auth/oauth2-providers/google-oauth/agent-identities/my-order-agent/tokens/m2m" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{}' | jq .
```

---

### SDK

#### Static API Key Provider

```python
from greennode_agentbase.identity import CreateApikeyProviderRequest

provider = asyncio.run(client.create_api_key_provider_async(
    request=CreateApikeyProviderRequest(
        name="openai-key",
        apikey="sk-proj-xxxxxxxxxxxxxxxxxxxx"
    )
))
print(f"Created: {provider.name} (status: {provider.status})")
```

#### Delegated API Key Provider

```python
from greennode_agentbase.identity import CreateDelegatedApiKeyProviderRequest

provider = asyncio.run(client.create_delegated_api_key_provider_async(
    request=CreateDelegatedApiKeyProviderRequest(name="user-openai-key")
))
```

#### OAuth2 Provider

**Tạo:**

```python
from greennode_agentbase.identity import CreateOauth2ProviderRequest

provider = asyncio.run(client.create_oauth2_provider_async(
    request=CreateOauth2ProviderRequest(
        name="google-oauth",
        client_id="812345678901-abcdefg.apps.googleusercontent.com",
        client_secret="GOCSPX-xxxxxxxxxxxx",
        authorization_url="https://accounts.google.com/o/oauth2/v2/auth",
        token_url="https://oauth2.googleapis.com/token",
    )
))
print(f"Callback URL: {provider.callback_url}")
```

**Lấy OAuth2 Token (M2M):**

```python
from greennode_agentbase.identity import GetM2mTokenRequest

result = asyncio.run(client.get_m2m_token_async(
    provider_name="google-oauth",
    agent_identity_name="my-order-agent",
    request=GetM2mTokenRequest()
))
print(f"Access Token: {result.access_token}")
```

#### Truy xuất Credential tại thời điểm chạy

Khi agent của bạn được triển khai trên AgentBase Runtime, runtime tự động tiêm `GREENNODE_CLIENT_ID`, `GREENNODE_CLIENT_SECRET`, và `GREENNODE_AGENT_IDENTITY` dưới dạng biến môi trường. SDK sử dụng các biến này tự động.

**Tiêm static API key:**

```python
from greennode_agentbase import (
    GreenNodeAgentBaseApp, RequestContext, PingStatus,
    requires_api_key, requires_access_token,
)

app = GreenNodeAgentBaseApp()

@app.ping
def health() -> PingStatus:
    return PingStatus.HEALTHY

@app.entrypoint
@requires_api_key(provider_name="openai-key")
def handler(payload: dict, context: RequestContext, openai_key: str) -> dict:
    from openai import OpenAI
    client = OpenAI(api_key=openai_key)
    response = client.chat.completions.create(
        model="gpt-4o",
        messages=[{"role": "user", "content": payload.get("input", "")}]
    )
    return {"output": response.choices[0].message.content}
```

**Tiêm OAuth2 access token:**

```python
@app.entrypoint
@requires_access_token(provider_name="google-oauth")
def handler(payload: dict, context: RequestContext, google_token: str) -> dict:
    import httpx
    resp = httpx.get(
        "https://www.googleapis.com/calendar/v3/calendars/primary/events",
        headers={"Authorization": f"Bearer {google_token}"},
    )
    return {"events": resp.json().get("items", [])}
```

---

## Các mô hình phản hồi

Các trường **AgentIdentityResponse**:

| Trường                | Kiểu dữ liệu | Mô tả                                             |
| ----------------------- | --------------- | --------------------------------------------------- |
| `id`                  | string          | Định danh UUID duy nhất                          |
| `name`                | string          | Tên Identity (không thể thay đổi sau khi tạo) |
| `description`         | string          | Mô tả tùy chọn                                  |
| `allowed_return_urls` | list[string]    | Các URL callback OAuth2                            |
| `created_at`          | datetime        | Thời gian tạo                                     |
| `updated_at`          | datetime        | Thời gian cập nhật cuối                         |

---

## Xử lý sự cố

| Lỗi                                    | Nguyên nhân                               | Cách khắc phục                                                                             |
| --------------------------------------- | ------------------------------------------- | --------------------------------------------------------------------------------------------- |
| 401 Unauthorized                        | IAM token hết hạn hoặc không hợp lệ   | Lấy lại token với credential hợp lệ                                                      |
| 403 Forbidden                           | Service account thiếu quyền               | Gắn `AgentBaseFullAccess` tại https://iam.console.vngcloud.vn                             |
| 409 Conflict                            | Tên identity hoặc provider đã tồn tại | Chọn một tên khác                                                                         |
| Lỗi xác thực tên                    | Tên không khớp `^[a-zA-Z0-9_-]+$`      | Chỉ sử dụng chữ cái, số, dấu gạch dưới và dấu gạch ngang. 3–50 ký tự          |
| 404 Not Found                           | Tên provider không tồn tại              | Xác minh bằng thao tác `list`                                                            |
| Agent không thể truy xuất credential | Thiếu tên identity                        | Đảm bảo biến môi trường `GREENNODE_AGENT_IDENTITY` được thiết lập trong runtime |

---

*Trước đó: [Tổng quan](../README.md) | Tiếp theo: [Runtime](../runtime/README.md)*
