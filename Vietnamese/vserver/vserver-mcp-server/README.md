# vServer MCP Server

**vServer MCP Server** là một server [MCP (Model Context Protocol)](https://modelcontextprotocol.io) cung cấp cho các trợ lý AI (Claude, Cursor, Gemini, …) một bộ công cụ để quản lý **vServer — sản phẩm compute / IaaS của GreenNode**: máy ảo, ổ đĩa block storage, snapshot, image, networking (VPC, subnet, security group, network ACL, route table, peering, interconnect, virtual IP, floating IP, network interface, DHCP option set), SSH key và placement group.

MCP là một chuẩn mở để cung cấp context có cấu trúc cho LLM. Thay vì gõ lệnh `grn` ([GreenNode CLI](https://docs.greennode.ai/vserver/getting-started/manage-vserver-with-the-greennode-cli)) hay gọi API công khai trực tiếp, trợ lý AI sẽ tự chọn và gọi công cụ mà vServer MCP Server cung cấp — dựa trên một yêu cầu bằng ngôn ngữ tự nhiên.

Sau khi kết nối, bạn có thể yêu cầu trợ lý AI bằng tiếng bình thường để:

* **Quản lý máy ảo**: list, xem chi tiết, tạo, resize, bật/tắt, xóa server; chụp user image; đọc serial console.
* **Quản lý storage**: tạo, attach, resize, xóa volume; chuyển volume sang tier IOPS khác; xem volume history.
* **Quản lý networking**: VPC và subnet, security group và rule, network ACL, route table, VPC peering, interconnect, virtual IP, floating IP, elastic network interface, DHCP option set.
* **Quản lý snapshot**: điểm snapshot block-level cho server và volume, kèm policy; rollback hoặc xóa điểm.
* **Quản lý key, placement và tag**: SSH key, placement group (affinity / anti-affinity), và tag vocabulary.

Phạm vi rộng hơn bộ lệnh greennode-cli: snapshot, route table, network ACL, VPC peering, interconnect và virtual IP không có tương đương trong CLI.

**An toàn mặc định:** server chạy **read-only** — chỉ inspect, không thay đổi gì. Các thao tác mutating (create/update/delete/power) chỉ chạy khi được bật tường minh lúc khởi động server (xem Configure Local MCP).

### Bắt đầu

Bộ tài liệu này bao gồm:

| Trang                | Nội dung                                                                                                                    |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Configure Remote MCP | Dùng **endpoint được host sẵn** qua HTTP — không cần cài gì, đăng nhập bằng IAM user GreenNode ngay trên trình duyệt.       |
| Configure Local MCP  | Chạy server cục bộ qua **stdio** — phù hợp Claude Desktop, Cursor, Claude Code, VS Code. Setup, config client, và các flag. |
| MCP Tools            | Toàn bộ 183 công cụ theo handler, kèm tham số và access level (read / write / destructive).                                 |

#### Chọn mode nào?

* **Remote (hosted)** — đường nhanh nhất: trỏ MCP client vào một URL và đăng nhập bằng IAM user qua trình duyệt. Không cần Python/`uv`, không cần credential trên máy. Xem Configure Remote MCP.
* **Local (stdio)** — chạy server trên máy của bạn, xác thực bằng credential trong `~/.greennode`. Access level do bạn chọn qua flag `--allow-write`. Xem Configure Local MCP.

### Yêu cầu

* Một **MCP client**: Claude Desktop, Claude Code, Cursor, VS Code (Copilot MCP), hoặc bất kỳ client nào nói MCP.
* **Remote (hosted)**: một **IAM user GreenNode** có quyền vServer — client tự mở flow đăng nhập; không cần cài gì, không cần khai báo secret.
* **Local (stdio)**: **Python ≥ 3.11**, [`uv`](https://docs.astral.sh/uv/), và **credential GreenNode** (`client_id` / `client_secret` trong `~/.greennode/credentials` — dùng chung với greennode-cli; chạy `grn configure` một lần nếu chưa có).

### Region

vServer phục vụ hai region, khai báo dưới dạng `Literal["HCM-3", "HAN"]`:

| Region  | Vị trí          |
| ------- | --------------- |
| `HCM-3` | TP. Hồ Chí Minh |
| `HAN`   | Hà Nội          |

Mọi resource đều scope theo region và **mỗi region có một project riêng trên gateway của nó** — server tự resolve project id, nên các tool không bao giờ nhận tham số `project_id`. Zone id là chuỗi dễ đọc (`HCM03-1A` … `HCM03-BKK-01`), không phải UUID. Mọi tool `list_*` đều echo lại region đã query, nên kết quả từ hai region không bao giờ bị trộn lẫn.

### Tài nguyên

* **GreenNode CLI** — quản lý vServer từ dòng lệnh: [Manage vServer with the GreenNode CLI](https://docs.greennode.ai/vserver/getting-started/manage-vserver-with-the-greennode-cli)
* **GreenNode MCP trên GitHub** — [https://github.com/GreenNodeHub/greennode-mcp](https://github.com/GreenNodeHub/greennode-mcp)
* **Model Context Protocol** — đặc tả MCP: [modelcontextprotocol.io](https://modelcontextprotocol.io)
