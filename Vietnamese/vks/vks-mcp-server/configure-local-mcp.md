# Configure Local MCP

**Local MCP** chạy **VKS MCP Server** như một process ngay trên máy, kết nối MCP client với dịch vụ VKS qua **stdio**. Đây là cách phổ biến nhất: server xác thực bằng credentials trong `~/.greennode` (dùng chung với greennode-cli) kết nối tới dịch vụ VKS.

### Requirements

* **Python ≥ 3.11**.
* [`uv`](https://docs.astral.sh/uv/) — quản lý môi trường và chạy **Python**.
* Repo [`greennode-mcp`](https://github.com/vngcloud/greennode-mcp) clone sẵn trên máy (client trỏ `--directory` tới đây; `uv run` tự cài deps ở lần chạy đầu).
* Một **MCP client**: Claude Desktop, Claude Code, Cursor, hoặc VS Code (Copilot MCP).
* **GreenNode credentials** — cung cấp hai cách:
  * File `~/.greennode/credentials` + `~/.greennode/config`: cài greennode-cli theo [hướng dẫn GreenNode CLI](https://docs.greennode.ai/vn/vks/getting-started/su-dung-greennode-cli-de-quan-ly-vks) rồi chạy `grn configure`.
  * Environment variable `GRN_CLIENT_ID` / `GRN_CLIENT_SECRET` (+ `GRN_DEFAULT_REGION`) — không cần file, và luôn override file nếu có cả hai.

> ⚠️ **Security**: không commit `client_secret` vào Git. Server giữ token in-memory, không ghi ra disk, không log token/secret.

### Configuration

Credentials và region đọc từ `~/.greennode/credentials` + `~/.greennode/config` (thư mục pre-rename `~/.greenode` vẫn được đọc làm fallback nếu chỉ có nó). Environment variable override file (ưu tiên cao nhất):

| Variable             | Tác dụng                                                      |
| -------------------- | ------------------------------------------------------------- |
| `GRN_CLIENT_ID`      | Override `client_id`                                          |
| `GRN_CLIENT_SECRET`  | Override `client_secret`                                      |
| `GRN_PROFILE`        | Chọn profile (mặc định: `default`)                            |
| `GRN_DEFAULT_REGION` | Override region (`HCM-3` hoặc `HAN`)                          |
| `GRN_PROJECT_ID`     | Override `project_id` (auto-discover từ vServer nếu bỏ trống) |

### Add to MCP client

Với **stdio**, MCP client tự spawn server bằng `command` / `args` trong config — không cần chạy server thủ công. **Read-only** là mặc định; thêm flag vào `args` để mở rộng quyền:

| Flag                            | Tác dụng                                |
| ------------------------------- | --------------------------------------- |
| _(không flag)_                  | Read-only tools                         |
| `--allow-write`                 | Mở tool create / update / delete.       |
| `--allow-sensitive-data-access` | Đọc kubeconfig, Secret, pod log, event. |

#### Claude Desktop / Cursor

Thêm entry vào config `mcpServers`, trỏ `--directory` tới thư mục gốc `greennode-mcp`:

```json
{
  "mcpServers": {
    "vks": {
      "command": "uv",
      "args": [
        "run",
        "--directory", "/path/to/greennode-mcp",
        "vks-mcp-server",
        "--allow-write"
      ]
    }
  }
}
```

Bỏ `--allow-write` nếu chỉ cần read-only; thêm `--allow-sensitive-data-access` nếu cần đọc kubeconfig/Secret/log.

#### Claude Code

```bash
claude mcp add vks -- \
  uv run --directory /path/to/greennode-mcp vks-mcp-server --allow-write

# Kiểm tra
claude mcp list
```

#### Visual Studio Code (Copilot MCP)

Thêm entry tương tự vào `.vscode/mcp.json` hoặc `settings.json`, cùng `command` / `args` như phần Claude Desktop.

### Troubleshooting

**Authentication thất bại (401):** Kiểm tra `client_id` / `client_secret` trong `~/.greennode/credentials` (chạy `grn configure`). Gọi `get_access_token` để xác nhận lấy được IAM bearer token.

**Sai region / không thấy resource:** Kiểm tra region trong `~/.greennode/config` hoặc `GRN_DEFAULT_REGION` (`HCM-3` hay `HAN`). Các `list_*` tool echo lại region đã query.

**Agent báo "tool không khả dụng":** Server đang read-only. Thêm `--allow-write` (và/hoặc `--allow-sensitive-data-access`) rồi restart client.

**Không connect được:** Kiểm tra `--directory` trỏ đúng thư mục gốc repo, và `uv sync` đã chạy xong. Xem log client để biết lỗi khởi động.
