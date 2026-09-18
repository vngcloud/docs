# Configure Remote MCP

**Remote MCP** là vServer MCP Server đã được host sẵn cho bạn: **một endpoint duy nhất**, không cần cài Python/`uv`, không cần clone repo, không cần `~/.greennode` trên máy. MCP client kết nối qua HTTP (**streamable-http**) và đăng nhập bằng **IAM user GreenNode** của chính nó.

Endpoint nằm sau **AgentBase Gateway** — gateway xử lý xác thực và chuyển tiếp identity của caller cho server, nên mọi lệnh gọi vServer chạy dưới account, project và permission của user đã đăng nhập. Nhiều user chia sẻ một endpoint nhưng mỗi người chỉ thấy resource của mình.

### Yêu cầu trước

* Một **MCP client** hỗ trợ remote MCP + OAuth: Claude Code, Claude Desktop / [claude.ai](http://claude.ai), Cursor, Visual Studio Code.
* Một **IAM user GreenNode** có quyền vServer (cùng account bạn dùng để đăng nhập [GreenNode Portal](https://console.greennode.ai)).

> Không cần API token, không cần `client_id` / `client_secret`. Client tự chạy OAuth login trên trình duyệt và tự refresh token — secret không bao giờ rơi vào file config.

### Remote MCP endpoint

\<!-- TODO: thay \<XX> bằng số deployment thực tế khi endpoint được provision. -->

| Service                         | Remote MCP Server URL                                                                            | Service key |
| ------------------------------- | ------------------------------------------------------------------------------------------------ | ----------- |
| **vServer — GreenNode Compute** | `https://gw-vserver-mcp-server-<XX>.agentbase-gateway.aiplatform.vngcloud.vn/vserver_mcp_server` | `vserver`   |

Endpoint này expose cùng bộ tool như local mode — xem MCP Tools.

### Xác thực

Endpoint là một **OAuth 2.1 resource server** đầy đủ theo spec MCP; client tự điều phối toàn bộ flow:

1. Client gọi endpoint không kèm token → nhận **401** kèm header `WWW-Authenticate` trỏ tới metadata của authorization server.
2. Client đọc metadata đó, tự đăng ký (Dynamic Client Registration), và mở trình duyệt tại trang login (authorization code + PKCE `S256`).
3. Sau khi đăng nhập, client giữ access token và **tự refresh** — không cần đăng nhập lại mỗi session.

Chỉ **Root / IAM user** mới đi qua được gateway này. Token **service-account** (`client_id` / `client_secret`, tức client-credentials) bị từ chối với `403 Access denied` — service-account chỉ dùng cho Configure Local MCP.

### Thêm vào MCP client

#### Claude Code

```bash
claude mcp add --transport http vserver \
  https://gw-vserver-mcp-server-<XX>.agentbase-gateway.aiplatform.vngcloud.vn/vserver_mcp_server

# Verify + đăng nhập
claude mcp list
```

Chạy `/mcp` trong Claude Code → chọn `vserver` → **Authenticate** để mở flow đăng nhập trên trình duyệt.

#### Claude Desktop / [claude.ai](http://claude.ai)

Settings → **Connectors** → **Add custom connector** → dán endpoint URL. Claude mở trang đăng nhập GreenNode ở lần dùng đầu tiên.

Remote MCP **không** dùng `command` / `args` / biến môi trường như stdio.

#### Cursor

Thêm một entry kiểu remote vào `mcp.json` — chỉ cần `url`, không cần header:

```json
{
  "mcpServers": {
    "vserver": {
      "url": "https://gw-vserver-mcp-server-<XX>.agentbase-gateway.aiplatform.vngcloud.vn/vserver_mcp_server"
    }
  }
}
```

Xem [Cursor — Model Context Protocol](https://docs.cursor.com/context/model-context-protocol).

#### Visual Studio Code

Thêm entry tương tự vào `.vscode/mcp.json`. Xem [Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers).

### Xử lý sự cố

**401 `iam_unauthenticated`:** Chưa đăng nhập, hoặc session hết hạn. Chạy lại flow authenticate của client (`/mcp` → `vserver` → Authenticate trong Claude Code).

**403 `Access denied: you are not authorized to access this gateway`:** Token hợp lệ nhưng principal không được cấp quyền trên gateway. Đăng nhập bằng **IAM user** của account được phép — token service-account (`client_id`/`client_secret`) không dùng được với remote endpoint.

**Client không mở trang đăng nhập:** Entry bị config sai kiểu (stdio thay vì remote), hoặc client không hỗ trợ OAuth cho remote MCP. Kiểm tra entry chỉ có `url` và không có `command` / `args`.

**Resource kỳ vọng bị thiếu:** Kiểm tra region (`HCM-3` / `HAN`) — mọi tool `list_*` đều echo lại region đã query, và mỗi region có project riêng. Nếu vẫn sai, xác nhận bạn đăng nhập đúng IAM user / account.

**Agent báo tool write không khả dụng:** Access level của hosted endpoint được cố định bởi người deploy (read-only / write); client không thể thêm flag. Nếu cần thao tác write mà endpoint không cho phép, dùng Configure Local MCP với `--allow-write`.
