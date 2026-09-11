# Configure Local MCP

**Local MCP** chạy **vMonitor MCP Server** như một process ngay trên máy của bạn, kết nối MCP client với vMonitor qua **stdio**. Server xác thực bằng credentials trong `~/.greennode` (dùng chung với greennode-cli) để gọi các API của vMonitor.

Chọn local khi bạn muốn tự đặt access level qua flag (`--allow-write`) hoặc chạy dưới service-account credentials. Nếu server đã được host sẵn qua HTTP, xem Configure Remote MCP.

### Requirements

* **Python ≥ 3.11**.
* [`uv`](https://docs.astral.sh/uv/) — quản lý môi trường và chạy **Python**.
* Repo [`greennode-mcp`](https://github.com/GreenNodeHub/greennode-mcp) clone sẵn trên máy (client trỏ `--directory` tới đây; `uv run` tự cài deps ở lần chạy đầu).
* Một **MCP client**: Claude Desktop, Claude Code, Cursor, hoặc VS Code (Copilot MCP).
* **GreenNode credentials** — cung cấp hai cách:
  * File `~/.greennode/credentials` + `~/.greennode/config`: cài greennode-cli rồi chạy `grn configure`. Chỉ cần `client_id` / `client_secret` của một service account từ GreenNode IAM Portal là đủ.
  * Environment variable `GRN_CLIENT_ID` / `GRN_CLIENT_SECRET` (+ `GRN_PROJECT_ID`) — không cần file, và luôn override file nếu có cả hai.

> ⚠️ **Security**: không commit `client_secret` vào Git. Server giữ token in-memory, không ghi ra disk, không log token/secret.

### Configuration

Credentials đọc từ `~/.greennode/credentials` + `~/.greennode/config` (định dạng INI, dùng chung với greennode-cli). Environment variable override file (ưu tiên cao nhất):

| Variable            | Tác dụng                                |
| ------------------- | --------------------------------------- |
| `GRN_CLIENT_ID`     | Override `client_id`                    |
| `GRN_CLIENT_SECRET` | Override `client_secret`                |
| `GRN_PROFILE`       | Chọn profile (mặc định: `default`)      |
| `GRN_PROJECT_ID`    | Override `project_id`                   |

vMonitor là dịch vụ **global** — server này không có setting region: `GRN_DEFAULT_REGION` bị bỏ qua ngay cả khi bạn đặt.

### Add to MCP client

Với **stdio**, MCP client tự spawn server bằng `command` / `args` trong config — không cần chạy server thủ công. **Read-only** là mặc định; thêm flag vào `args` để mở rộng quyền:

| Flag            | Tác dụng                                                                                                             |
| --------------- | -------------------------------------------------------------------------------------------------------------------- |
| _(không flag)_  | Read-only: chỉ các tool read / query / guide — **110 tool**.                                                          |
| `--allow-write` | Đăng ký toàn bộ tool create / update / delete → **213 tool**, gồm cả các tool đặt hàng quota (tốn tiền).              |

#### Claude Desktop / Cursor

Thêm entry vào config `mcpServers`, trỏ `--directory` tới thư mục gốc `greennode-mcp`:

```json
{
  "mcpServers": {
    "vmonitor": {
      "command": "uv",
      "args": [
        "run",
        "--directory", "/path/to/greennode-mcp",
        "vmonitor-mcp-server",
        "--allow-write"
      ]
    }
  }
}
```

Bỏ `--allow-write` nếu read-only là đủ cho nhu cầu của bạn.

#### Claude Code

```bash
claude mcp add vmonitor -- \
  uv run --directory /path/to/greennode-mcp vmonitor-mcp-server --allow-write

# Verify
claude mcp list
```

#### Visual Studio Code (Copilot MCP)

Thêm entry tương tự vào `.vscode/mcp.json` hoặc `settings.json`, với cùng `command` / `args` như mục Claude Desktop.

### Test server

Để thử các tool trước khi gắn vào client, chạy **MCP Inspector** từ thư mục gốc repo:

```bash
npx @modelcontextprotocol/inspector uv run vmonitor-mcp-server                 # read-only, 110 tool
npx @modelcontextprotocol/inspector uv run vmonitor-mcp-server --allow-write   # đủ 213 tool
```

Trên UI: Transport Type = `STDIO` → **Connect** → **Tools** → **List Tools**. Lệnh gọi thử tốt nhất là `list_dashboards` — nếu trả về dashboard của bạn thì authentication đã chạy đúng.

### Troubleshooting

**Authentication fails (401):** Kiểm tra `client_id` / `client_secret` trong `~/.greennode/credentials` (chạy `grn configure`), hoặc env var `GRN_CLIENT_ID` / `GRN_CLIENT_SECRET`. Gọi `list_dashboards` để xác nhận lấy được IAM token và vMonitor phản hồi.

**Sai project / thiếu resource:** Kiểm tra `GRN_PROJECT_ID` và `GRN_PROFILE`. vMonitor là global — không có region nào để kiểm tra lại trên server này.

**Agent báo tool không khả dụng:** Server đang chạy read-only. Thêm `--allow-write` rồi restart client — write tool không được đăng ký khi thiếu flag nên agent không nhìn thấy chúng.

**Không kết nối được:** Kiểm tra `--directory` trỏ đúng thư mục gốc repo và `uv sync` đã chạy xong. Xem log của client để tìm lỗi lúc khởi động.
