# vMonitor MCP Server

## vMonitor MCP Server

**vMonitor MCP Server** là một [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server, cung cấp cho các AI assistant (Claude, Cursor, Gemini, …) một bộ tool để quản lý **vMonitor Platform** — dịch vụ observability của GreenNode: dashboard, metric query, alarm, infrastructure host, log, notification, quota & usage, và synthetic uptime monitor.

MCP là một chuẩn mở để cung cấp structured context cho các LLM. Thay vì thao tác qua console vMonitor hay gọi trực tiếp năm API vMonitor khác nhau, AI assistant sẽ tự chọn và invoke các tool mà vMonitor MCP Server expose — dựa trên yêu cầu bằng ngôn ngữ tự nhiên của bạn.

Server bao phủ **toàn bộ năm API của vMonitor** (metric/dashboard, Log, notification, quota-usage, và synthetic/uptime) sau **một lớp xác thực IAM duy nhất** — request được tự động route tới đúng API.

Sau khi kết nối, bạn có thể yêu cầu AI assistant bằng ngôn ngữ tự nhiên để:

* **Quản lý dashboard & widget**: liệt kê, xem chi tiết, tạo, clone, cập nhật, xóa dashboard; thêm / di chuyển / resize widget; quản lý variable và saved view.
* **Query metric**: khám phá metric catalogue, chạy time-series query, đọc metric của một resource ngay từ default dashboard của nó.
* **Quản lý alarm**: tạo / cập nhật / xóa alarm metric, log và change-detection; xem lịch sử và trạng thái hiện tại.
* **Giám sát infrastructure host**: liệt kê host trên các sản phẩm GreenNode (vServer, vStorage, vDB, vLB, vBackup, …), xem metric snapshot hiện tại, tạm dừng / mở lại giám sát.
* **Làm việc với log**: search và export log; quản lý log project, pipeline, processor, archive, refill và resource log mapping.
* **Quản lý notification**: tạo channel đã xác thực OTP — Email, SMS, Slack, Webhook, Telegram, Teams.
* **Theo dõi quota & usage**: đọc mức sử dụng và giá, sau đó mua / resize quota (báo giá trước, đặt hàng sau).
* **Chạy synthetic test**: quản lý uptime monitor và probing location.

**An toàn theo mặc định:** server chạy ở chế độ **read-only** — chỉ xem, không đổi gì. Các thao tác thay đổi (create/update/delete) chỉ được đăng ký khi server khởi động với `--allow-write` (xem Configure Local MCP). Các tool đặt hàng quota tiêu tốn tiền — mọi đơn hàng đều có bước báo giá miễn phí trước đó.

### Getting started

Bộ tài liệu này gồm các trang:

| Trang                 | Nội dung                                                                                                                             |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Configure Remote MCP | **Tự host server qua HTTP** (uv hoặc Docker, ví dụ sau AgentBase Gateway) rồi kết nối MCP client chỉ bằng một URL.                    |
| Configure Local MCP  | Chạy server local qua **stdio** — phù hợp Claude Desktop, Cursor, Claude Code, VS Code. Cài đặt, config client, và các run flag.      |
| vMonitor MCP Tools   | Toàn bộ 213 tool theo từng nhóm tính năng, kèm access level (read / write / destructive), 11 feature-guide prompt và các workflow chính. |

#### Chọn mode nào?

* **Local (stdio)** — chạy server ngay trên máy, authenticate bằng credentials trong `~/.greennode`. Chọn được access level qua flag (`--allow-write`). Xem Configure Local MCP.
* **Remote (HTTP)** — tự host server (hoặc để platform team host) rồi kết nối chỉ với một URL — không cần cài đặt gì trên máy client. Xem Configure Remote MCP.

### Requirements

* Một **MCP client**: Claude Desktop, Claude Code, Cursor, VS Code (Copilot MCP), hoặc bất kỳ client nào nói được MCP.
* **Local (stdio)**: **Python ≥ 3.11**, [`uv`](https://docs.astral.sh/uv/), và **GreenNode credentials** — `client_id` / `client_secret` của một service account từ GreenNode IAM Portal, nằm trong `~/.greennode/credentials` (dùng chung với greennode-cli; chạy `grn configure` một lần nếu chưa có).
* **Remote (HTTP)**: máy host cần credentials (env var hoặc mount `~/.greennode`) — hoặc không cần gì cả khi mỗi caller tự mang token của họ phía sau AgentBase Gateway.

### Region

vMonitor là dịch vụ **global** — không có chọn region: `GRN_DEFAULT_REGION` bị bỏ qua, mọi tool đều nói chuyện với cùng các endpoint vMonitor. (Trong khi đó, các MCP server VKS / vServer là region-scoped.)

### Resources

* **GreenNode MCP trên GitHub** — [**https://github.com/GreenNodeHub/greennode-mcp**](https://github.com/GreenNodeHub/greennode-mcp) (source của server này: `src/vmonitor-mcp-server`)
* **Tài liệu vMonitor Platform** — xem mục vMonitor Platform trong bộ tài liệu này
* **Model Context Protocol** — đặc tả chuẩn MCP: [modelcontextprotocol.io](https://modelcontextprotocol.io)
