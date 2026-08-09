# VKS MCP Server

## VKS MCP Server

**VKS MCP Server** là một [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server, cung cấp cho các AI assistant (Claude, Cursor, Gemini, …) một bộ tool để quản lý **VKS — GreenNode Kubernetes Service**: cluster, node group, và cả các Kubernetes resource _bên trong_ cluster.

MCP là một chuẩn standard để cung cấp structured context cho các LLM. Thay vì tự gõ lệnh `grn` ([GreenNode CLI](https://docs.greennode.ai/vn/vks/getting-started/su-dung-greennode-cli-de-quan-ly-vks)) hay gọi API public, AI assistant sẽ tự chọn và invoke các tool mà VKS MCP Server expose — dựa trên yêu cầu bằng ngôn ngữ tự nhiên của bạn.

Sau khi kết nối, bạn có thể yêu cầu AI assistant bằng ngôn ngữ tự nhiên để:

* **Quản lý cluster**: liệt kê, xem chi tiết, tạo, cập nhật, xóa cluster; xem events; lấy kubeconfig; bật auto-upgrade / auto-healing.
* **Quản lý node group**: tạo, cập nhật số node, autoscale, upgrade version, xóa node group.
* **Quản lý resources Kubernetes**: xem/sửa resource, apply YAML, xem log pod và events.

**An toàn theo mặc định:** server chạy ở chế độ **read-only** — chỉ xem, không đổi gì. Các thao tác thay đổi (create/update/delete) và đọc dữ liệu nhạy cảm (Secret, log, events) chỉ hoạt động khi bạn bật tường minh khi khởi động server (xem Configure Local MCP).

### Getting started

Bộ tài liệu này gồm các trang:

| Trang                | Nội dung                                                                                                                         |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Configure Remote MCP | Dùng **endpoint host sẵn** qua HTTP — không cần cài đặt gì, đăng nhập bằng GreenNode IAM user ngay trên browser.                 |
| Configure Local MCP  | Chạy server local qua **stdio** — phù hợp Claude Desktop, Cursor, Claude Code, VS Code. Cài đặt, config client, và các run flag. |
| MCP Tools            | Toàn bộ 41 tool theo từng handler, kèm parameter và access level (read / write / sensitive).                                     |

#### Chọn mode nào?

* **Remote (hosted)** — cách nhanh nhất: khai báo một URL trong MCP client rồi đăng nhập bằng IAM user qua browser. Không cần cài Python/`uv`, không cần credentials trên máy. Xem Configure Remote MCP.
* **Local (stdio)** — chạy server ngay trên máy, authenticate bằng credentials trong `~/.greennode`. Chọn được access level qua flag (`--allow-write`, `--allow-sensitive-data-access`). Xem Configure Local MCP.

### Requirements

* Một **MCP client**: Claude Desktop, Claude Code, Cursor, VS Code (Copilot MCP), hoặc bất kỳ client nào nói được MCP.
* **Remote (hosted)**: một **GreenNode IAM user** có quyền trên VKS — client tự mở luồng đăng nhập, không cần cài đặt hay khai báo secret.
* **Local (stdio)**: **Python ≥ 3.11**, [`uv`](https://docs.astral.sh/uv/), và **GreenNode credentials** (`client_id` / `client_secret` trong `~/.greennode/credentials` — dùng chung với greennode-cli, chạy `grn configure` một lần nếu chưa có).

### Region

VKS hiện phục vụ hai region, khai báo bằng `Literal["HCM-3", "HAN"]`:

| Region  | Location    |
| ------- | ----------- |
| `HCM-3` | Hồ Chí Minh |
| `HAN`   | Hà Nội      |

Các `list_*` tool luôn echo lại region vừa query, nên bạn không nhầm data giữa hai region.

### Resources

* **GreenNode CLI** — quản lý VKS bằng dòng lệnh: [Sử dụng GreenNode CLI để quản lý VKS](https://docs.greennode.ai/vn/vks/getting-started/su-dung-greennode-cli-de-quan-ly-vks)
* **GreenNode MCP Github** — [**https://github.com/GreenNodeHub/greennode-mcp**](https://github.com/GreenNodeHub/greennode-mcp)
* **Model Context Protocol** — đặc tả chuẩn MCP: [modelcontextprotocol.io](https://modelcontextprotocol.io)

