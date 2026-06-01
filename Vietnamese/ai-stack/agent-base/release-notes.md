# Lịch sử cập nhật — GreenNode AgentBase

## Tháng 5, 2026

GreenNode AgentBase ra mắt **Phase 2** với các tính năng mới mở rộng khả năng quản trị, bảo mật và tích hợp cho AI Agent:

**Tính năng mới:**

* **Marketplace:** Browse và deploy AI agent từ thư viện template theo danh mục — AI Chat, Coding, Automation. Hỗ trợ filter, xem chi tiết và deploy 1 click.
  * Tìm hiểu thêm tại [Marketplace](marketplace/README.md).

* **Container Registry:** Kho lưu trữ container image riêng, được cấp phát tự động cho tổ chức. Hỗ trợ push image qua AgentBase Skills (khuyến nghị) hoặc Docker CLI thủ công; image dùng trực tiếp khi tạo Runtime.
  * Tìm hiểu thêm tại [Container Registry](container-registry/README.md).

* **Rate Limit:** Kiểm soát tần suất gọi API theo số request hoặc token trên từng model và API key, ngăn quá tải hệ thống và kiểm soát chi phí.
  * Tìm hiểu thêm tại [Rate Limit](protect-govern/rate-limit.md).

* **MCP Governance:** Kiểm soát tập trung kết nối giữa AI Agent và external service:
  * **MCP Gateway** — Proxy tập trung, tự động nhận diện protocol, áp dụng Policy và hỗ trợ Private mode qua VPC Peering.
  * **Policy Groups** — Bộ quy tắc Allow/Deny theo tool name, input pattern và output pattern.
  * Tìm hiểu thêm tại [MCP Governance](mcp-governance/README.md).

* **AI Coding:** Kết nối Claude Code CLI và các AI coding tool OpenAI-compatible (OpenAI SDK, LiteLLM, Cursor...) trực tiếp với GreenNode MaaS — thanh toán bằng credit-token nội bộ.
  * Tìm hiểu thêm tại [AI Coding](ai-coding/README.md).

* **Usage & Budget:** Dashboard theo dõi lượng tiêu thụ token và chi phí realtime theo agent, model, API key và khoảng thời gian; cài đặt ngân sách tháng với cảnh báo tự động khi đạt 80% và 100%.
  * Tìm hiểu thêm tại [Usage & Budget](usage-budget/README.md).

* **Mạng riêng tư (Private Networking):** VPC Peering cho Agent Runtime và MCP Gateway — cho phép agent kết nối đến internal service mà không cần expose ra internet.
  * Tìm hiểu thêm tại [Mạng riêng tư](private-networking.md).

***

## Tháng 4, 2026

GreenNode ra mắt **OpenClaw 1-Click** trên AgentBase, cho phép triển khai AI Agent cá nhân dựa trên OpenClaw ngay từ **Agent Marketplace** — không cần kiến thức kỹ thuật, không cần cài đặt thủ công, chỉ trong 40–60 giây.

**Tính năng mới:**

* **OpenClaw 1-Click:** Deploy OpenClaw instance trực tiếp từ Marketplace với cấu hình tối giản.
  * **Tự động kết nối GreenNode MaaS:** Tài khoản GreenNode được tự động cấp quyền truy cập model AI, không cần cấu hình API key thủ công. Model mặc định: **qwen3-5-27b**.
  * **BYOK — Bring Your Own Key:** Hỗ trợ mang API key từ provider bên ngoài (OpenAI, Anthropic, Gemini...).
  * **Tích hợp Channel:** Cấu hình kết nối Telegram và Zalo ngay trong bước deploy.
  * **My Agents:** Quản lý toàn bộ OpenClaw instance với filter theo trạng thái, stop, restart và xóa.
  * Tìm hiểu thêm tại [OpenClaw 1-Click](agent-runtime/openclaw/openclaw-1-click.md).

***

## Tháng 3, 2026

GreenNode AgentBase ra mắt **Phase 1** — nền tảng hạ tầng chuyên biệt dành cho AI Agent, giúp developer triển khai và vận hành AI Agent trên cloud mà không cần tự quản lý server, scaling hay credential.

**Tính năng mới:**

* **Agent Runtime:** Deploy agent dưới dạng container với autoscaling, versioning và zero-downtime deployment; hỗ trợ Custom Agent và OpenClaw 1-Click.
* **Access Control & Team Permissions:** Quản lý danh tính agent, tự động inject credentials vào container; phân quyền thành viên theo Role với Service Accounts.
* **Memory Service:** Lưu trữ lịch sử hội thoại (short-term) và trích xuất facts ngữ nghĩa (long-term).
* **GreenNode MaaS Integration:** Kết nối trực tiếp với LLM models qua API tương thích OpenAI.
* Tìm hiểu thêm tại [GreenNode AgentBase](README.md).

***
