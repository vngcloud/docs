# Configure Local MCP

**Local MCP** chạy **vBackup MCP Server** như một process trên máy của bạn, kết nối MCP client tới vBackup qua **stdio**. Server xác thực bằng credential trong `~/.greennode` (dùng chung với greennode-cli) để gọi vBackup API.

Chọn local khi bạn cần tự đặt access level qua flag `--allow-write` hoặc chạy dưới credential service-account. Nếu chỉ muốn dùng ngay không cài đặt gì, xem Configure Remote MCP.

### Yêu cầu

* **Python ≥ 3.11**.
* [`uv`](https://docs.astral.sh/uv/) — quản lý môi trường và chạy Python.
* Repo [`greennode-mcp`](https://github.com/GreenNodeHub/greennode-mcp) đã clone cục bộ (client trỏ `--directory` vào đó; `uv run` cài dependency ở lần chạy đầu).
* Một **MCP client**: Claude Desktop, Claude Code, Cursor, hoặc VS Code (Copilot MCP).
* **Credential GreenNode** — hai cách cung cấp:
  * File `~/.greennode/credentials` + `~/.greennode/config`: cài greennode-cli và chạy `grn configure`.
  * Biến môi trường `GRN_CLIENT_ID` / `GRN_CLIENT_SECRET` (+ `GRN_DEFAULT_REGION`) — không cần file, và luôn override file khi cả hai cùng tồn tại.

> ⚠️ **Bảo mật**: không bao giờ commit `client_secret` vào Git. Server giữ token trong memory — không ghi ra disk, không log.

### Cấu hình

Credential và region được đọc từ `~/.greennode/credentials` + `~/.greennode/config` (thư mục `~/.greenode` trước khi đổi tên vẫn được dùng làm fallback khi chỉ nó tồn tại). Biến môi trường override file (ưu tiên cao nhất):

| Variable             | Tác dụng                             |
| -------------------- | ------------------------------------ |
| `GRN_CLIENT_ID`      | Override `client_id`                 |
| `GRN_CLIENT_SECRET`  | Override `client_secret`             |
| `GRN_PROFILE`        | Chọn profile (mặc định: `default`)   |
| `GRN_DEFAULT_REGION` | Override region (`HCM-3` hoặc `HAN`) |
| `GRN_PROJECT_ID`     | Override `project_id`                |

### Thêm vào MCP client

Với **stdio**, MCP client tự spawn server từ `command` / `args` trong config — không cần khởi động server bằng tay. **Read-only** là mặc định; thêm `--allow-write` vào `args` để mở rộng access:

| Flag            | Tác dụng                                                                                                                                                                                                    |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _(không flag)_  | Read-only: chỉ tool list / get / discovery — **41 công cụ**.                                                                                                                                                |
| `--allow-write` | Đăng ký toàn bộ tool create / update / delete → **68 công cụ**. Tool destructive (xóa destination, policy, backup server, backup database, restore point) thêm annotation `destructiveHint` để client warn. |

### Claude Desktop / Cursor

Thêm một entry dưới `mcpServers`, trỏ `--directory` vào root repo `greennode-mcp`:

```json
{
  "mcpServers": {
    "vbackup": {
      "command": "uv",
      "args": [
        "run",
        "--directory", "/path/to/greennode-mcp",
        "vbackup-mcp-server",
        "--allow-write"
      ]
    }
  }
}
```

Bỏ `--allow-write` nếu read-only là đủ.

### Claude Code

```bash
claude mcp add vbackup -- \
  uv run --directory /path/to/greennode-mcp vbackup-mcp-server --allow-write

# Verify
claude mcp list
```

### Visual Studio Code (Copilot MCP)

Thêm entry tương tự vào `.vscode/mcp.json` hoặc `settings.json`, với cùng `command` / `args` như mục Claude Desktop.

### Xử lý sự cố

**Xác thực thất bại (401):** Kiểm tra `client_id` / `client_secret` trong `~/.greennode/credentials` (chạy `grn configure`). Gọi `get_access_token` để xác nhận có lấy được IAM bearer token.

**Sai region / resource thiếu:** Kiểm tra region trong `~/.greennode/config` hoặc `GRN_DEFAULT_REGION` (`HCM-3` hoặc `HAN`). Mọi tool `list_*` echo lại region đã query. Hai gateway thấy resource khác nhau — gateway HAN trả cả backend HAN lẫn HCM, còn HCM chỉ trả của nó, nên resource không thấy có thể chỉ nằm ở region kia.

**"Không có gì được bảo vệ" là nói dối về phía vDB:** `list_databases` trả mọi vDB instance account đang có và báo eligibility từng instance trong `ineligible_reason` — PostgreSQL single-node không eligible cho backup và trả về kèm lý do, không bị omit im lặng. Chỉ deployment cluster mới backup được.

**Agent báo tool write không khả dụng:** Server đang chạy read-only. Thêm `--allow-write`, rồi restart client.

**`list_*_history` trả list rỗng hoặc ngắn:** `list_backup_history` và `list_database_backup_history` áp silent window **180 ngày** mặc định phía API. Response rỗng không bao giờ là bằng chứng backup không chạy — truyền `from_date` (epoch milliseconds hoặc ISO-8601) để truy xuất xa hơn.

**Edit destination bị từ chối với `Cannot edit vault lock`:** Lock là permanent. Xảy ra khi vault lock tạo với `changeDuration=0`, hoặc change window của lock đã hết. DTO cấm giá trị 0 khi tạo lock mới; lock permanent đang tồn tại không thể edit hoặc disable qua tool.

**Xóa vDB backup cứ fail:** Hai 409 chặn delete. `Your resource is being processed.` là wait — retry sau khi point upload xong. `Your resource is being managed by Vault.` không phải — chỉ thành công khi retention vault-lock hết hạn hoặc lock được gỡ.

**Không kết nối được:** Xác nhận `--directory` trỏ vào root repo và `uv sync` đã chạy xong. Kiểm tra client log xem có lỗi startup.
