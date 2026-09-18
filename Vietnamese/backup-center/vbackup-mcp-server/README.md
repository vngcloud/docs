# vBackup MCP Server

**vBackup MCP Server** là một server [MCP (Model Context Protocol)](https://modelcontextprotocol.io) cung cấp cho các trợ lý AI (Claude, Cursor, Gemini, …) một bộ công cụ để quản lý **vBackup — dịch vụ backup theo lịch và theo policy của GreenNode** cho máy ảo vServer (kèm volume) và database vDB, các restore point do backup tạo ra, và history của các lần backup và restore.

MCP là một chuẩn mở để cung cấp context có cấu trúc cho LLM. Thay vì gọi API công khai trực tiếp, trợ lý AI sẽ tự chọn và gọi công cụ mà vBackup MCP Server cung cấp — dựa trên một yêu cầu bằng ngôn ngữ tự nhiên.

Sau khi kết nối, bạn có thể yêu cầu trợ lý AI bằng tiếng bình thường để:

* **Quản lý backup destination** ("Backup Location"): tạo vault hoặc vStorage container, set quota, bật soft delete, áp vault lock.
* **Quản lý backup policy**: định nghĩa schedule hourly/daily/weekly/monthly kèm retention, thăng một policy lên default, hoặc retire.
* **Bảo vệ instance vServer**: chọn policy và destination, chọn disk nào include, chạy backup ad-hoc, pause / resume schedule, download hoặc xóa restore point.
* **Bảo vệ database vDB** (chỉ deployment **cluster** của PostgreSQL và Redis): tạo backup database, attach policy, chạy backup ad-hoc, xóa restore point.
* **Xem coverage và history**: ai đang được bảo vệ, ai không, tại sao backup đêm qua fail, destination đang giữ bao nhiêu, và chart platform trend theo thời gian.

vBackup là sản phẩm khác với **snapshot** block-level của vServer — snapshot nằm trong vServer MCP Server. Backup là file-level, lưu vào vault destination, sống sót khi source server bị xóa, và tính phí theo quota vault.

**An toàn mặc định:** server chạy **read-only** — chỉ inspect, không thay đổi. Các thao tác mutating (create / update / delete destination, policy, backup server, backup database, restore point) chỉ chạy khi được bật tường minh lúc khởi động server (xem Configure Local MCP).

### Bắt đầu

Bộ tài liệu này bao gồm:

| Trang                | Nội dung                                                                                                                    |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Configure Remote MCP | Dùng **endpoint được host sẵn** qua HTTP — không cần cài gì, đăng nhập bằng IAM user GreenNode ngay trên trình duyệt.       |
| Configure Local MCP  | Chạy server cục bộ qua **stdio** — phù hợp Claude Desktop, Cursor, Claude Code, VS Code. Setup, config client, và các flag. |
| MCP Tools            | Toàn bộ 68 công cụ theo handler, kèm tham số và access level (read / write / destructive).                                  |

#### Chọn mode nào?

* **Remote (hosted)** — đường nhanh nhất: trỏ MCP client vào một URL và đăng nhập bằng IAM user qua trình duyệt. Không cần Python/`uv`, không cần credential trên máy. Xem Configure Remote MCP.
* **Local (stdio)** — chạy server trên máy của bạn, xác thực bằng credential trong `~/.greennode`. Access level do bạn chọn qua flag `--allow-write`. Xem Configure Local MCP.

### Yêu cầu

* Một **MCP client**: Claude Desktop, Claude Code, Cursor, VS Code (Copilot MCP), hoặc bất kỳ client nào nói MCP.
* **Remote (hosted)**: một **IAM user GreenNode** có quyền vBackup — client tự mở flow đăng nhập; không cần cài gì, không cần khai báo secret.
* **Local (stdio)**: **Python ≥ 3.11**, [`uv`](https://docs.astral.sh/uv/), và **credential GreenNode** (`client_id` / `client_secret` trong `~/.greennode/credentials` — dùng chung với greennode-cli).

### Region

vBackup phục vụ hai region, khai báo dưới dạng `Literal["HCM-3", "HAN"]`:

| Region  | Vị trí          |
| ------- | --------------- |
| `HCM-3` | TP. Hồ Chí Minh |
| `HAN`   | Hà Nội          |

Mọi tool đều nhận tham số `region`, và mọi output `list_*` echo lại region đã query. Hai gateway thấy resource khác nhau — nếu không thấy ở một region, thử region kia. Một backup destination sống đúng trong một region; dashboard vMonitor là bề mặt duy nhất trả cho cả hai region trong một call.

### Tài nguyên

* **vServer MCP Server** — cho snapshot block-level (sản phẩm khác trên cùng gateway): vServer MCP Server
* **GreenNode MCP trên GitHub** — [https://github.com/GreenNodeHub/greennode-mcp](https://github.com/GreenNodeHub/greennode-mcp)
* **Model Context Protocol** — đặc tả MCP: [modelcontextprotocol.io](https://modelcontextprotocol.io)
