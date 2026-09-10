# Configure Remote MCP

Remote MCP là **vMonitor MCP Server được host qua HTTP** (**streamable-http**): MCP client kết nối chỉ bằng một URL — không cần cài Python/`uv`, không cần clone repo, và không cần `~/.greennode` trên máy client.

Bạn tự host server (hoặc platform team của bạn host) — hoặc chạy trực tiếp, hoặc đặt sau **AgentBase Gateway**. Khi ở sau gateway, authentication được tập trung hóa: gateway xử lý phần đăng nhập và chuyển tiếp danh tính của caller tới server, nên mọi lời gọi vMonitor đều chạy dưới account, project và quyền của user đã đăng nhập. Nhiều user dùng chung một endpoint mà mỗi người vẫn chỉ thấy resource của chính mình.

### Host server

Hai cách, đều từ repo [`greennode-mcp`](https://github.com/GreenNodeHub/greennode-mcp):

**Cách 1 — chạy bằng uv (HTTP transport):**

```bash
uv run vmonitor-mcp-server --transport streamable-http --host 0.0.0.0 --port 8080
```

Mặc định bind `127.0.0.1:8000` — đặt `--host 0.0.0.0` (kèm port) khi client kết nối từ máy khác.

**Cách 2 — Docker:**

```bash
# Build (từ thư mục gốc repo)
docker build -f src/vmonitor-mcp-server/Dockerfile -t vmonitor-mcp-server .

# Run (streamable-http trên :8080); truyền credentials qua env hoặc mount ~/.greennode
docker run --rm -p 8080:8080 \
  -e GRN_CLIENT_ID=<id> -e GRN_CLIENT_SECRET=<secret> \
  vmonitor-mcp-server
```

Lưu ý chung cho cả hai cách:

* `GET /health` luôn không cần xác thực — dùng để kiểm tra liveness / readiness.
* **Access level đặt lúc server khởi động**: mặc định read-only (**110 tool**); thêm `--allow-write` để đăng ký đủ **213 tool**. Cân nhắc kỹ — các tool đặt hàng quota tiêu tốn tiền.
* HTTP transport có thể khởi động **hoàn toàn không có credentials** khi chạy sau AgentBase Gateway ở chế độ passthrough — khi đó mỗi request đều yêu cầu token của caller.

### Authentication (HTTP transport)

Danh tính được resolve **theo từng request**, không cần flag:

1. Request mang IAM bearer token trong `Authorization` (AgentBase Gateway chuyển tiếp token của caller) → **mọi lời gọi vMonitor chạy dưới danh tính caller đó**. Token user bị từ chối sẽ báo lỗi — không bao giờ tự động retry ngầm dưới service account.
2. Không có token, nhưng host có cấu hình service-account credentials (env var hoặc `~/.greennode`) → dùng service account dùng chung.
3. Không có gì → **401** + `WWW-Authenticate: Bearer`.

Lưu ý thêm:

* **stdio (local) luôn yêu cầu service-account credentials**; chỉ HTTP transport mới hỗ trợ chế độ passthrough không credentials.
* Server không tự verify token — các API của vMonitor mới là bên verify. Token hết hạn sẽ hiện lên dưới dạng `500 IAM_VALIDATION_ERROR`, được xem là auth failure và refresh một lần.
* `--auth-debug` (hoặc `GRN_MCP_AUTH_DEBUG=1`) bật diagnostic logging opt-in, đã redact, chỉ dành cho HTTP: log tóm tắt auth của inbound request và expose `GET /whoami` không cần xác thực. Nó không verify signature và không log full token — **không bật trong production**.

### Remote MCP endpoint

| Service                                        | Remote MCP Server URL             | Service key |
| ---------------------------------------------- | --------------------------------- | ----------- |
| **vMonitor — nền tảng observability GreenNode** | `<YOUR_VMONITOR_MCP_SERVER_URL>`  | `vmonitor`  |

Thay `<YOUR_VMONITOR_MCP_SERVER_URL>` bằng endpoint mà deployment của bạn expose — ví dụ `https://<your-host>:8080` nếu chạy trực tiếp, hoặc endpoint AgentBase Gateway của bạn (dạng `https://gw-vmonitor-mcp-server-<id>.agentbase-gateway.aiplatform.vngcloud.vn/vmonitor_mcp_server`) khi đặt sau gateway.

Endpoint này expose cùng bộ tool như local mode — xem vMonitor MCP Tools. Access level (read-only / write) do người deploy cố định.

### Add to MCP client

#### Claude Code

```bash
claude mcp add --transport http vmonitor <YOUR_VMONITOR_MCP_SERVER_URL>

# Verify + đăng nhập
claude mcp list
```

Khi endpoint nằm sau AgentBase Gateway, chạy `/mcp` trong Claude Code → chọn `vmonitor` → **Authenticate** để mở luồng đăng nhập trên browser (OAuth 2.1, client tự refresh token).

#### Claude Desktop / claude.ai

Settings → **Connectors** → **Add custom connector** → dán endpoint URL. Sau AgentBase Gateway, Claude sẽ mở trang đăng nhập GreenNode ở lần dùng đầu.

Remote MCP **không** dùng `command` / `args` / environment variable như stdio.

#### Cursor

Thêm entry kiểu remote vào `mcp.json` — chỉ cần `url`:

```json
{
  "mcpServers": {
    "vmonitor": {
      "url": "<YOUR_VMONITOR_MCP_SERVER_URL>"
    }
  }
}
```

Xem [Cursor — Model Context Protocol](https://docs.cursor.com/context/model-context-protocol).

#### Visual Studio Code

Thêm entry tương tự vào `.vscode/mcp.json`. Xem [Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers).

#### HTTP trực tiếp không qua gateway

Với deployment không có AgentBase Gateway, các client không tự chạy OAuth flow có thể gửi bearer token tường minh:

```json
{
  "mcpServers": {
    "vmonitor": {
      "type": "http",
      "url": "<YOUR_VMONITOR_MCP_SERVER_URL>",
      "headers": {
        "Authorization": "Bearer ${GREENNODE_MCP_TOKEN}"
      }
    }
  }
}
```

Token là một IAM bearer token — mọi lời gọi khi đó chạy dưới danh tính đó.

### Troubleshooting

**401 (unauthenticated):** Caller không mang token hợp lệ và host không có service-account credentials. Sau gateway, chạy lại luồng authenticate của client (`/mcp` → `vmonitor` → Authenticate trong Claude Code); với deployment trực tiếp, kiểm tra header `Authorization: Bearer`.

**403 `Access denied`:** Token hợp lệ nhưng principal không được cấp quyền trên gateway. Đăng nhập bằng **IAM user** thuộc account được authorize.

**500 `IAM_VALIDATION_ERROR`:** Token hết hạn — server tự refresh một lần; nếu lỗi vẫn còn thì đăng nhập lại.

**Agent báo tool không khả dụng:** Access level của endpoint host cố định lúc deploy (read-only / write) — client không thể thêm flag. Nếu cần thao tác write mà endpoint không cho phép, dùng Configure Local MCP.

**Server có đang chạy không?** `GET /health` trên endpoint — luôn mở, không cần token.
