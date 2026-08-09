# Configure Remote MCP



Remote MCP là VKS MCP Server đã được host sẵn: **một endpoint duy nhất**, không cần cài Python/`uv`, không cần clone repo, không cần `~/.greennode`. MCP client kết nối qua HTTP (**streamable-http**) và đăng nhập bằng chính **GreenNode IAM user** của mình.

### Prerequisites

* Một **MCP client** hỗ trợ remote MCP + OAuth: Claude Code, Claude Desktop / claude.ai, Cursor, Visual Studio Code.
* Một **GreenNode IAM user** có quyền trên VKS (chính là account đăng nhập [GreenNode Portal](https://vks.console.greennode.ai)).

> Không cần API token hay `client_id` / `client_secret`. Client tự chạy OAuth

### Remote MCP endpoint

| Service                                | Remote MCP Server URL                                                                  | Service key |
| -------------------------------------- | -------------------------------------------------------------------------------------- | ----------- |
| **VKS — GreenNode Kubernetes Service** | `https://gw-vks-mcp-server-81.agentbase-gateway.aiplatform.vngcloud.vn/vks_mcp_server` | `vks`       |

Endpoint này expose cùng bộ tool như chế độ local — xem MCP Tools.

### Authentication

Endpoint là một **OAuth 2.1 resource server** theo đúng spec MCP, client xử lý toàn bộ luồng:

1. Client gọi endpoint khi chưa có token → nhận **401** kèm `WWW-Authenticate` trỏ tới metadata của authorization server.
2. Client tự discover, tự đăng ký (Dynamic Client Registration), rồi mở browser tới trang đăng nhập (authorization code + PKCE `S256`).

Chỉ **Root/IAM User** mới qua được cổng này. Token của **service account** (`client_id` / `client_secret`, dạng client-credentials) sẽ bị từ chối với `403 Access denied` — service-account credentials chỉ dùng cho Configure Local MCP.

### Add to MCP client

#### Claude Code

```bash
claude mcp add --transport http vks \
  https://gw-vks-mcp-server-81.agentbase-gateway.aiplatform.vngcloud.vn/vks_mcp_server

# Kiểm tra + đăng nhập
claude mcp list
```

Chạy `/mcp` trong Claude Code → chọn `vks` → **Authenticate** để mở luồng đăng nhập browser.

#### Claude Desktop / claude.ai

Settings → **Connectors** → **Add custom connector** → dán URL endpoint. Claude tự mở trang đăng nhập GreenNode ở lần dùng đầu tiên.

Remote MCP **không** dùng `command` / `args` / environment variable như stdio.

#### Cursor

Thêm entry dạng remote vào `mcp.json` — chỉ cần `url`, không cần header:

```json
{
  "mcpServers": {
    "vks": {
      "url": "https://gw-vks-mcp-server-81.agentbase-gateway.aiplatform.vngcloud.vn/vks_mcp_server"
    }
  }
}
```

Xem [Cursor — Model Context Protocol](https://docs.cursor.com/context/model-context-protocol).

#### Visual Studio Code

Thêm entry tương tự vào `.vscode/mcp.json`. Xem [Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers).

### Troubleshooting

**401 `iam_unauthenticated`:** Chưa đăng nhập, hoặc session hết hạn. Chạy lại luồng authenticate của client (`/mcp` → `vks` → Authenticate với Claude Code).

**403 `Access denied: you are not authorized to access this gateway`:** Token hợp lệ nhưng principal không được cấp quyền vào gateway. Đăng nhập bằng **IAM user** của account đã được cấp quyền — service-account token (`client_id`/`client_secret`) không dùng được cho remote endpoint.

**Client không tự mở trang đăng nhập:** Client đang cấu hình sai dạng (stdio thay vì remote), hoặc không hỗ trợ OAuth cho remote MCP. Kiểm tra entry chỉ có `url`, không có `command` / `args`.

**Không thấy cluster quen thuộc:** Kiểm tra region (`HCM-3` / `HAN`) — các `list_*` tool echo lại region đã query. Nếu vẫn lệch, xác nhận đang đăng nhập đúng IAM user/account.

**Agent báo tool không khả dụng:** Access level của endpoint host sẵn do phía deploy quyết định (read-only / write / sensitive data), client không tự thêm flag được. Cần thao tác ghi mà endpoint không cho phép thì dùng Configure Local MCP.
