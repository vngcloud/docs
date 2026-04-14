# FAQ

> Các câu hỏi thường gặp về GreenNode AgentBase.

---


## Tổng quan (Overview)

**H: Agent của tôi phải được viết bằng ngôn ngữ lập trình nào?**

Agent của bạn phải là một HTTP server chạy trong container lắng nghe trên cổng 8080. AgentBase SDK (`greennode-agentbase`) chỉ hỗ trợ Python. Hầu hết người dùng viết agent bằng Python sử dụng `GreenNodeAgentBaseApp` làm framework server.

---

**H: Tôi có thể chạy agent cục bộ trong quá trình phát triển không?**

Có. Đặt `GREENNODE_CLIENT_ID` và `GREENNODE_CLIENT_SECRET` làm biến môi trường (hoặc sử dụng `.greennode.json` trong thư mục gốc dự án), sau đó chạy agent trực tiếp. Đặt `GREENNODE_AGENT_IDENTITY` thành tên agent identity dùng cho phát triển để kích hoạt truy xuất credential.

```bash
export GREENNODE_CLIENT_ID="<your-client-id>"
export GREENNODE_CLIENT_SECRET="<your-client-secret>"
export GREENNODE_AGENT_IDENTITY="my-agent-dev"
python main.py
```

---

**H: Nhiều runtime có thể dùng chung một identity không?**

Có. Một identity có thể được liên kết với nhiều runtime. Tất cả runtime dùng chung một identity đều có quyền truy cập cùng các cấu hình xác thực. Nếu bạn cần credential khác nhau cho mỗi môi trường, hãy tạo các identity riêng biệt (ví dụ, `my-agent-dev`, `my-agent-prod`).

---

**H: Những framework nào được hỗ trợ chính thức?**

SDK hỗ trợ đầy đủ cho LangGraph qua `AgentBaseMemoryEvents` (từ `greennode-agent-bridge[langgraph]`). Đối với lớp HTTP server, sử dụng `GreenNodeAgentBaseApp`. Bất kỳ framework HTTP Python nào lắng nghe trên cổng 8080 và cung cấp `GET /health` trả về HTTP 200 đều có thể hoạt động.

---

## Bắt đầu

**H: Yêu cầu thiết lập tối thiểu để triển khai agent là gì?**

Ở mức tối thiểu bạn cần:

1. Một tài khoản dịch vụ GreenNode IAM
2. Một **Agent Identity** đã đăng ký ([Access Control](./access-control/README.md))
3. Một Docker image trong vCR ([Dịch Vụ Hỗ Trợ](./supporting-services.md#container-registry-vcr))
4. Một **Runtime** trỏ đến image đó ([Runtime](./runtime/README.md))

Bạn không cần Memory, cấu hình xác thực, hoặc tích hợp API bên ngoài để chạy một agent echo cơ bản.

---

**H: Tôi có thể sử dụng Docker image công khai thay vì vCR không?**

vCR được khuyến nghị cao — image trên vCR nằm trên cùng mạng nội bộ với các node runtime (pull nhanh, không tốn chi phí egress). Runtime cũng có thể pull từ registry bên ngoài nếu bạn cấu hình `imageAuth`, nhưng điều này tạo ra phụ thuộc bên ngoài trong môi trường production.

---

**H: Làm thế nào để triển khai phiên bản mới mà không bị gián đoạn?**

Mỗi lệnh `PATCH /agent-runtimes/{id}` tạo ra một phiên bản mới. Endpoint `DEFAULT` tự động cập nhật lên phiên bản mới nhất. Để triển khai an toàn với canary testing, hãy tạo một endpoint riêng gắn với phiên bản mới, kiểm tra, sau đó cập nhật endpoint `DEFAULT`. Xem [Runtime mục 5.12](./runtime/README.md#advanced-canary-deployment).

---

## Access Control

**H: Tôi có thể đổi tên identity sau khi tạo không?**

Không. Tên identity không thể thay đổi. Nếu bạn cần đổi tên, hãy tạo một identity mới với tên mong muốn, đăng ký lại tất cả cấu hình xác thực, cập nhật các runtime để sử dụng identity mới, sau đó xóa identity cũ.

---

**H: Điều gì xảy ra nếu tôi cố xóa một identity đang có runtime hoạt động?**

API sẽ từ chối yêu cầu xóa. Hãy dừng và xóa tất cả runtime liên quan trước, sau đó mới xóa identity.

---

**H: Làm thế nào để xác minh việc truy xuất credential hoạt động trước khi deploy?**

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

**H: Sự khác biệt giữa Runtime và Endpoint là gì?**

Một **Runtime** là môi trường tính toán (container, chính sách scale, flavor). Một **Endpoint** là URL HTTPS mà client gọi đến. Mỗi runtime tự động nhận một endpoint `DEFAULT`. Bạn có thể tạo thêm các endpoint gắn với phiên bản cụ thể cho việc triển khai canary.

---

**H: Các trạng thái runtime có thể có là gì?**

| Trạng thái        | Mô tả                                                   |
| ------------ | ------------------------------------------------------------- |
| `CREATING` | Runtime đang được tạo; các container đang khởi động             |
| `ACTIVE`   | Tất cả replica tối thiểu đều khỏe mạnh; endpoint đang phục vụ lưu lượng |
| `UPDATING` | Đang triển khai phiên bản mới                       |
| `ERROR`    | Một hoặc nhiều replica bắt buộc không thể khởi động (kiểm tra log)    |
| `DELETING` | Runtime đang được xóa                                      |

---

**H: Agent của tôi liên tục bị OOMKilled. Tôi nên làm gì?**

1. Kiểm tra mức sử dụng bộ nhớ hiện tại qua API metric:
   ```bash
   curl -s "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID/metrics" \
     -H "Authorization: Bearer $TOKEN" | jq '{cpu: .cpuCores, memory_mb: (.memoryBytes / 1048576 | floor)}'
   ```
2. Nâng cấp lên flavor lớn hơn qua `PATCH /agent-runtimes/{id}`
3. Tối ưu hóa sử dụng bộ nhớ: giảm độ dài lịch sử hội thoại, tránh tải bộ dữ liệu lớn vào bộ nhớ

---

**H: Làm thế nào để kích hoạt deploy từ CI pipeline?**

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

**H: Dữ liệu hội thoại của tôi có riêng tư cho tổ chức không?**

Có. Dữ liệu Memory (event và memory record) được cách ly theo tổ chức.

---

**H: Điều gì xảy ra với dữ liệu memory khi tôi xóa runtime?**

Dữ liệu memory KHÔNG bị xóa khi bạn xóa runtime. Dữ liệu vẫn tồn tại cho đến khi:

- Hết hạn (dựa trên `eventExpiryDuration`, phạm vi 1–365 ngày)
- Bạn xóa rõ ràng kho memory (`DELETE /memories/{id}`)

---

**H: Tìm kiếm ngữ nghĩa của tôi trả về không có kết quả. Tại sao?**

Các nguyên nhân phổ biến:

1. **Sai namespace** — Namespace dùng để lưu trữ và tìm kiếm phải giống hệt nhau.
2. **scoreThreshold quá cao** — Bắt đầu với `"scoreThreshold": 0.0` để xem tất cả kết quả, sau đó tăng dần.
3. **Record chưa được tạo** — Việc tạo record là bất đồng bộ. Đợi vài giây sau khi đăng event.
4. **Truy vấn quá khác biệt** — Tìm kiếm ngữ nghĩa tìm ý nghĩa tương đồng, không phải khớp chính xác.

```bash
# Debug: browse all records in the namespace
NAMESPACE_ENCODED=$(python3 -c 'import urllib.parse; print(urllib.parse.quote("/strategies/<strategy-id>/actors/<actor-id>"))')
curl -s "https://agentbase.api.vngcloud.vn/memory/memories/$MEMORY_ID/memory-records?namespace=$NAMESPACE_ENCODED&limit=100" \
  -H "Authorization: Bearer $TOKEN" | jq '.[] | .memory'
```

---

**H: Sự khác biệt giữa short-term và long-term memory là gì?**

|             | Short-Term                                       | Long-Term                                    |
| ----------- | ------------------------------------------------ | -------------------------------------------- |
| Lưu trữ     | Event (các lượt hội thoại) theo thứ tự             | Memory record (các sự kiện được trích xuất) dưới dạng vector  |
| Truy xuất   | Theo actor + session                               | Theo tìm kiếm tương đồng ngữ nghĩa                |
| Hết hạn      | Sau `eventExpiryDuration` ngày               | Vĩnh viễn cho đến khi bị xóa                      |
| Trường hợp sử dụng    | Lịch sử hội thoại, LangGraph checkpointing    | Sở thích người dùng, dữ kiện lâu dài           |
| Tích hợp | `AgentBaseMemoryEvents` LangGraph checkpointer | `MemoryClient.searchMemoryRecords_async()` |

---

## SDK & Tích hợp

**H: Tên chính xác của các biến môi trường cho SDK là gì?**

| Biến                     | Mô tả                                    |
| ---------------------------- | ---------------------------------------------- |
| `GREENNODE_CLIENT_ID`      | Client ID tài khoản dịch vụ IAM                  |
| `GREENNODE_CLIENT_SECRET`  | Client secret tài khoản dịch vụ IAM              |
| `GREENNODE_AGENT_IDENTITY` | Tên agent identity (để truy xuất credential) |

---

**H: Tôi có thể dùng `@requires_api_key` cho các hàm không phải entrypoint không?**

Không. Đối với các mẫu khác, sử dụng `IdentityClient.get_api_key_for_agent_identity_async()`:

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

## Xử lý sự cố (Troubleshooting)

**H: Runtime của tôi bị kẹt ở trạng thái `CREATING`. Tôi nên làm gì?**

1. Kiểm tra log runtime:
   ```bash
   curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/logs" \
     -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
     -d '{"from": 0, "limit": 100}' | jq -r '.logs[]'
   ```
2. Xác minh URL image đúng và tồn tại trong vCR
3. Xác minh credential `imageAuth` đúng cho registry private
4. Xác minh container cung cấp `GET /health` trả về HTTP 200 trên cổng 8080

---

**H: Tôi gặp lỗi 401 Unauthorized khi gọi API. Làm thế nào để sửa?**

IAM token có thời hạn ngắn. Hãy lấy lại token:

```bash
TOKEN=$(curl -s -X POST "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token" \
  -H "Content-Type: application/json" \
  -d '{"grantType": "client_credentials", "clientId": "'"$GREENNODE_CLIENT_ID"'", "clientSecret": "'"$GREENNODE_CLIENT_SECRET"'"}' \
  | jq -r '.data.accessToken')
```

---

**H: Agent của tôi trả về lỗi 500 nhưng log trông bình thường. Tôi nên kiểm tra gì?**

1. Kiểm tra log endpoint (không chỉ log runtime):
   ```bash
   curl -s -X POST "https://agentbase.api.vngcloud.vn/runtime/agent-runtimes/$RUNTIME_ID/endpoints/$ENDPOINT_ID/logs" \
     -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
     -d '{"from": 0, "limit": 200}' | jq -r '.logs[]' | grep -i "error\|traceback\|exception"
   ```
2. Xác minh header `context.user_id` và `context.session_id` có mặt nếu sử dụng Context
3. Xác minh health check `@app.ping` trả về `PingStatus.HEALTHY`

---

## Dọn dẹp / Xóa tài nguyên

**Mục tiêu:** Xóa tất cả tài nguyên AgentBase cho một dự án.

> **Lưu ý:** Thao tác này không thể hoàn tác. Runtime, dữ liệu memory, và cấu hình xác thực sẽ bị xóa vĩnh viễn.

### Thứ Tự Xóa

Xóa tài nguyên theo thứ tự sau để tránh lỗi phụ thuộc:

1. Xóa runtime
2. Xóa auth provider
3. Xóa agent identity
4. Xóa kho memory
5. Xóa image và repository vCR (tùy chọn)

---

### Bước 1: Xóa Runtime

#### Portal (GUI)

1. Mở https://aiplatform.console.vngcloud.vn/runtime → nhấn vào runtime → **"Delete"** → xác nhận

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

### Bước 2: Xóa Auth Provider

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

### Bước 3: Xóa Agent Identity

#### Portal (GUI)

1. Mở https://aiplatform.console.vngcloud.vn/identity → tìm identity → **"Delete"** → xác nhận

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

### Bước 4: Xóa Kho Memory

#### Portal (GUI)

1. Mở https://aiplatform.console.vngcloud.vn/memory → nhấn vào memory → **"Delete"** → xác nhận

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

### Bước 5: Xóa Repository vCR (Tùy chọn)

> **Quan trọng:** Bạn phải xóa tất cả image trước khi xóa repository.

#### Portal (GUI)

1. Mở https://vcr.console.vngcloud.vn → điều hướng đến repository → xóa tất cả image trước → xóa repository

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

### Xác Minh Dọn Dẹp

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

