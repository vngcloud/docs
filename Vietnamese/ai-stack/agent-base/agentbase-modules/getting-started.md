# Bắt Đầu

> Hoàn thành các điều kiện cần này trước khi sử dụng bất kỳ dịch vụ AgentBase nào. Sau khi hoàn tất, hãy theo lộ trình đọc tài liệu để bắt đầu xây dựng.

---


## Điều kiện cần (Prerequisites)

### Tạo tài khoản GreenNode

1. Truy cập https://console.vngcloud.vn và đăng ký hoặc đăng nhập.
2. Hoàn thành xác minh tài khoản.
3. Tạo hoặc tham gia một **Organization**. Tất cả tài nguyên AgentBase đều thuộc phạm vi một organization.

> **Lưu ý:** Nếu công ty của bạn đã có một GreenNode organization, hãy yêu cầu quản trị viên mời bạn trước khi tạo tài khoản riêng.

### Cài đặt các công cụ cần thiết

#### Python SDK

```bash
pip install greennode-agentbase
```

Đối với tích hợp LangGraph và LangChain:

```bash
pip install "greennode-agent-bridge[langgraph]"
```

#### curl và jq (cho các ví dụ RESTful API)

```bash
# macOS
brew install jq

# Ubuntu / Debian
apt-get install -y curl jq

# Windows — use WSL or Git Bash with jq from https://jqlang.github.io/jq/
```

### Thiết lập IAM Service Account

Tất cả các cuộc gọi AgentBase API (Portal, RESTful API và SDK) đều yêu cầu một GreenNode IAM bearer token được lấy từ Service Account. Thực hiện các bước sau một lần để tạo service account của bạn.

#### Portal (GUI)

**Bước 1: Di chuyển đến IAM Service Accounts**

1. Mở: https://iam.console.vngcloud.vn/service-accounts
2. Nếu được yêu cầu, đăng nhập bằng tài khoản GreenNode của bạn.

**Bước 2: Tạo Service Account mới**

1. Nhấn **"Create a Service Account"**.
2. Điền vào:
   - **Name**: ví dụ, `agentbase-dev`
   - **Description**: ví dụ, `Service account for AgentBase test`
3. Nhấn **"Next Step"**.

![1774518047320](image/02-getting-started/1774518047320.png)

**Bước 3: Gắn Policies**

1. Trong tab Permissions, nhấn **"Attach Policies"**.
2. Tìm và gắn từng policy sau:
   - `AgentBaseFullAccess` — truy cập các dịch vụ Identity, Runtime và Memory
   - `vcrFullAccess` — truy cập Container Registry (để push/pull image)
   - `AiPlatformFullAccess` — truy cập các LLM model và API key
3. Nhấn **"Create Service Account"**.

**Bước 4: Sao chép Client Secret (chỉ một lần duy nhất)**

> **Lưu ý:** Client Secret chỉ được hiển thị **một lần duy nhất** tại thời điểm tạo. Sao chép và lưu lại ngay lập tức — không thể truy xuất lại sau đó. Nếu bị mất, bạn phải reset nó (điều này sẽ vô hiệu hóa secret cũ).

1. Một cửa sổ popup xuất hiện với thông tin credential của bạn. Sao chép **Client Secret** và lưu trữ an toàn.
2. Nhấn **"Back to list"**.
3. Tìm service account mới của bạn, nhấn vào nó, di chuyển đến tab **"Security credentials"**.
4. Sao chép **Client ID**.

![1776141606586](image/getting-started/1776141606586.png)

### Cấu hình xác thực

Bây giờ bạn đã có **Client ID** và **Client Secret**, hãy cấu hình chúng để tất cả các cuộc gọi API và thao tác SDK có thể tự động xác thực.

#### Phương án A — Biến môi trường

```bash
export GREENNODE_CLIENT_ID="your-client-id"
export GREENNODE_CLIENT_SECRET="your-client-secret"
```

#### Phương án B — Tệp cấu hình

Tạo tệp `.greennode.json` trong thư mục gốc của dự án:

```json
{
  "client_id": "your-client-id",
  "client_secret": "your-client-secret"
}
```

> **Lưu ý:** Không commit `.greennode.json` vào hệ thống quản lý phiên bản. Thêm nó vào `.gitignore`.

#### Lấy IAM Token (`$TOKEN`)

Tất cả các ví dụ RESTful API trong hướng dẫn này sử dụng `$TOKEN`. Lấy token bằng lệnh:

```bash
TOKEN=$(curl -s -X POST "https://iam.api.vngcloud.vn/accounts-api/v2/auth/token" \
  -u "$GREENNODE_CLIENT_ID:$GREENNODE_CLIENT_SECRET" \
  -d "grant_type=client_credentials" \
  -H "Content-Type: application/x-www-form-urlencoded" | jq -r '.access_token')
```

Sau đó sử dụng trong các cuộc gọi API:

```bash
curl -s -X GET "https://agentbase.api.vngcloud.vn/..." \
  -H "Authorization: Bearer $TOKEN"
```

**Thời hạn token:** Token có thời hạn ngắn. Nếu bạn nhận được phản hồi `401 Unauthorized`, chạy lại lệnh trên để lấy token mới.

> **Lưu ý (người dùng SDK):** Python SDK tự động quản lý token — chỉ cần đảm bảo credential của bạn được cấu hình qua biến môi trường hoặc `.greennode.json`. Không cần lấy token thủ công.

---

## Tiếp theo là gì?

Sau khi hoàn thành các điều kiện cần, hãy theo các chương theo thứ tự để thực hiện lần triển khai đầu tiên, hoặc chuyển đến một chủ đề cụ thể:

| Tôi muốn...                           | Đi đến                                                                                                          |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| Đăng ký agent trên nền tảng      | [Access Control](./access-control/README.md#agent-identity)                                  |
| Lưu trữ API key cho các dịch vụ bên ngoài   | [Access Control — Auth &amp; Secrets](./access-control/README.md#auth--secrets)             |
| Push một Docker image                    | [Supporting Services — Container Registry](./supporting-services.md#container-registry-vcr) |
| Deploy và chạy agent của tôi                | [Runtime](./runtime/README.md)                                                                  |
| Thêm Memory hội thoại                | [Memory](./memory/README.md)                                                                    |
| Giám sát và debug                      | [Insight](./insight/README.md)                                                                  |
| Lấy LLM API key (tương thích OpenAI) | [Supporting Services — AI Platform](./supporting-services.md#ai-platform-aip--llm-access)   |
| Sử dụng Python SDK                     | [Supporting Services — SDK &amp; Integration](./supporting-services.md#sdk--integration)    |

> **Lần đầu?** Bắt đầu với [Access Control](./access-control/README.md) → [Supporting Services (vCR)](./supporting-services.md#container-registry-vcr) → [Runtime](./runtime/README.md) để đi từ con số không đến một agent đang chạy.

---

## Chi phí (Charging & Fees)

> Thông tin chi tiết về thanh toán sẽ được cập nhật trong phiên bản sau.

---

