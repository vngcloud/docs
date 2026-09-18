# Configure Local MCP

**Local MCP** chạy **vServer MCP Server** như một process trên máy của bạn, kết nối MCP client tới vServer qua **stdio**. Server xác thực bằng credential trong `~/.greennode` (dùng chung với greennode-cli) để gọi vServer API.

Chọn local khi bạn cần tự đặt access level qua flag `--allow-write` hoặc chạy dưới credential service-account. Nếu chỉ muốn dùng ngay không cài đặt gì, xem Configure Remote MCP.

### Yêu cầu

* **Python ≥ 3.11**.
* [`uv`](https://docs.astral.sh/uv/) — quản lý môi trường và chạy Python.
* Repo [`greennode-mcp`](https://github.com/GreenNodeHub/greennode-mcp) đã clone cục bộ (client trỏ `--directory` vào đó; `uv run` cài dependency ở lần chạy đầu).
* Một **MCP client**: Claude Desktop, Claude Code, Cursor, hoặc VS Code (Copilot MCP).
* **Credential GreenNode** — hai cách cung cấp:
  * File `~/.greennode/credentials` + `~/.greennode/config`: cài greennode-cli theo [hướng dẫn GreenNode CLI](https://docs.greennode.ai/vserver/getting-started/manage-vserver-with-the-greennode-cli), rồi chạy `grn configure`.
  * Biến môi trường `GRN_CLIENT_ID` / `GRN_CLIENT_SECRET` (+ `GRN_DEFAULT_REGION`) — không cần file, và luôn override file khi cả hai cùng tồn tại.

> ⚠️ **Bảo mật**: không bao giờ commit `client_secret` vào Git. Server giữ token trong memory — không ghi ra disk, không log.

### Cấu hình

Credential và region được đọc từ `~/.greennode/credentials` + `~/.greennode/config` (thư mục `~/.greenode` trước khi đổi tên vẫn được dùng làm fallback khi chỉ nó tồn tại). Biến môi trường override file (ưu tiên cao nhất):

| Variable             | Tác dụng                                                                          |
| -------------------- | --------------------------------------------------------------------------------- |
| `GRN_CLIENT_ID`      | Override `client_id`                                                              |
| `GRN_CLIENT_SECRET`  | Override `client_secret`                                                          |
| `GRN_PROFILE`        | Chọn profile (mặc định: `default`)                                                |
| `GRN_DEFAULT_REGION` | Override region (`HCM-3` hoặc `HAN`)                                              |
| `GRN_PROJECT_ID`     | Override `project_id` cho **region mặc định only** — các region khác auto-resolve |

### Thêm vào MCP client

Với **stdio**, MCP client tự spawn server từ `command` / `args` trong config — không cần khởi động server bằng tay. **Read-only** là mặc định; thêm `--allow-write` vào `args` để mở rộng access:

| Flag            | Tác dụng                                                                                                                                                                                                  |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _(không flag)_  | Read-only: chỉ tool list / get / discovery / dry-run — **84 công cụ**.                                                                                                                                    |
| `--allow-write` | Đăng ký toàn bộ tool create / update / delete / power → **183 công cụ**. Tool destructive (delete, rollback, resize gây mất data) thêm annotation `destructiveHint` để client có thể warn trước khi chạy. |

### Claude Desktop / Cursor

Thêm một entry dưới `mcpServers`, trỏ `--directory` vào root repo `greennode-mcp`:

```json
{
  "mcpServers": {
    "vserver": {
      "command": "uv",
      "args": [
        "run",
        "--directory", "/path/to/greennode-mcp",
        "vserver-mcp-server",
        "--allow-write"
      ]
    }
  }
}
```

Bỏ `--allow-write` nếu read-only là đủ.

### Claude Code

```bash
claude mcp add vserver -- \
  uv run --directory /path/to/greennode-mcp vserver-mcp-server --allow-write

# Verify
claude mcp list
```

### Visual Studio Code (Copilot MCP)

Thêm entry tương tự vào `.vscode/mcp.json` hoặc `settings.json`, với cùng `command` / `args` như mục Claude Desktop.

### Xử lý sự cố

**Xác thực thất bại (401):** Kiểm tra `client_id` / `client_secret` trong `~/.greennode/credentials` (chạy `grn configure`). Gọi `get_access_token` để xác nhận có lấy được IAM bearer token.

**Sai region / resource thiếu:** Kiểm tra region trong `~/.greennode/config` hoặc `GRN_DEFAULT_REGION` (`HCM-3` hoặc `HAN`). Mọi tool `list_*` đều echo lại region đã query, và mỗi region có project riêng — resource ở HAN không thấy từ HCM-3 và ngược lại.

**Agent báo tool không khả dụng:** Server đang chạy read-only. Thêm `--allow-write`, rồi restart client.

**`list_*` trả về ít hơn console:** Một số catalogue (`list_active_vpcs`, `list_elastic_ips`, `list_shared_server_snapshots`, `list_interconnect_circuit_types`, `get_volume_snapshot_policy`) bị gate theo IAM policy của caller và trả `403 IAM_PERMISSION_DENIED` khi thiếu grant. Docstring của tool có nêu fallback trong từng trường hợp.

**Không kết nối được:** Xác nhận `--directory` trỏ vào root repo và `uv sync` đã chạy xong. Kiểm tra client log xem có lỗi startup.
