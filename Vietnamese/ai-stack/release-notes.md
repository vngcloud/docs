# Lịch sử cập nhật — GreenNode AI Stack

Tổng hợp các bản cập nhật của toàn bộ sản phẩm trong GreenNode AI Stack — GreenNode AgentBase, Model as a Service, AI Gateway, AI Platform, AI Coding và GenAI Studio.

***

## Tháng 8, 2026

**GreenNode MaaS — Cập nhật danh mục model & bảng giá**

Để mang lại trải nghiệm tốt hơn, GreenNode cập nhật danh mục model trên MaaS, gồm hai nhóm:

* **Model do GreenNode trực tiếp self-host.**
* **Model third-party từ đối tác đã ký kết hợp đồng chính thức.**

**Mốc thời gian chuyển đổi**

| Sự kiện                                                                            | Thời điểm      |
| ------------------------------------------------------------------------------------ | -------------- |
| Dừng cung cấp các model hiện tại & công bố danh mục model mới trên portal            | 03/08/2026     |
| Gia hạn tự động 30 ngày — tiếp tục dùng model hiện tại đến hết                       | 02/09/2026     |
| Sau thời điểm này, request đến model cũ sẽ trả về lỗi và không thực hiện được        | Từ 03/09/2026  |

**Quý khách cần làm gì**

* Đối chiếu **model đang sử dụng** với [danh mục model mới](model-as-a-service/cac-model-duoc-cung-cap.md). Nếu model hiện tại vẫn còn trong danh mục, **không cần thay đổi**. Chỉ khi model không còn trong danh mục, mới cần tham khảo [bảng giá](model-as-a-service/bang-gia-model.md) và chọn model thay thế phù hợp.
* **Kiểm tra kỹ thuật khi chuyển đổi** (nếu cần thay thế model): model thay thế có thể khác về model ID/endpoint cũng như đặc điểm output. Vui lòng kiểm thử trước và điều chỉnh cấu hình, prompt cho phù hợp để tránh gián đoạn.
* Nếu cần **thêm thời gian chuyển đổi** ngoài mốc 02/09/2026, hoặc có nhu cầu đặc biệt về một model cụ thể, vui lòng liên hệ đội ngũ GreenNode để được tư vấn.

**Lợi ích sau chuyển đổi**

* **Minh bạch nguồn model:** trên portal hiển thị rõ model nào thuộc GreenNode self-host và model nào là third-party.
* **Chi phí tối ưu hơn:** nhiều model trong danh mục mới có giá tốt hơn trước — xem chi tiết tại [Bảng giá Model](model-as-a-service/bang-gia-model.md).
* **Danh mục đầy đủ & liên tục mở rộng:** đáp ứng đa số model open-source và closed-source top tier (Claude, GPT,…).

{% hint style="info" %}
Cần hỗ trợ trong quá trình chuyển đổi? Liên hệ qua email [support@greennode.ai](mailto:support@greennode.ai), hotline **19001549**, hoặc [Trung tâm hỗ trợ](https://helpdesk.greennode.ai/portal/vi/home).
{% endhint %}

* Xem danh mục model mới tại [Các Model được cung cấp](model-as-a-service/cac-model-duoc-cung-cap.md).
* Xem bảng giá chi tiết tại [Bảng giá Model](model-as-a-service/bang-gia-model.md).

***

## Tháng 5, 2026

**GreenNode AgentBase — Phase 2**

GreenNode AgentBase ra mắt **Phase 2** với các tính năng mới mở rộng khả năng quản trị, bảo mật và tích hợp cho AI Agent:

**Tính năng mới:**

* **Marketplace:** Browse và deploy AI agent từ thư viện template theo danh mục — AI Chat, Coding, Automation. Hỗ trợ filter, xem chi tiết và deploy 1 click.
  * Tìm hiểu thêm tại [Marketplace](agent-base/marketplace/README.md).

* **Container Registry:** Kho lưu trữ container image riêng, được cấp phát tự động cho tổ chức. Hỗ trợ push image qua AgentBase Skills (khuyến nghị) hoặc Docker CLI thủ công; image dùng trực tiếp khi tạo Runtime.
  * Tìm hiểu thêm tại [Container Registry](agent-base/container-registry/README.md).

* **Rate Limit:** Kiểm soát tần suất gọi API theo số request hoặc token trên từng model và API key, ngăn quá tải hệ thống và kiểm soát chi phí.
  * Tìm hiểu thêm tại [Rate Limit](agent-base/protect-govern/rate-limit.md).

* **MCP Governance:** Kiểm soát tập trung kết nối giữa AI Agent và external service:
  * **MCP Gateway** — Proxy tập trung, tự động nhận diện protocol, áp dụng Policy và hỗ trợ Private mode qua VPC Peering.
  * **Policy Groups** — Bộ quy tắc Allow/Deny theo tool name, input pattern và output pattern.
  * Tìm hiểu thêm tại [MCP Governance](agent-base/mcp-governance/README.md).

* **AI Coding:** Kết nối Claude Code CLI và các AI coding tool OpenAI-compatible (OpenAI SDK, LiteLLM, Cursor...) trực tiếp với GreenNode MaaS — thanh toán bằng credit-token nội bộ.
  * Tìm hiểu thêm tại [AI Coding](ai-coding/README.md).

* **Usage & Budget:** Dashboard theo dõi lượng tiêu thụ token và chi phí realtime theo agent, model, API key và khoảng thời gian; cài đặt ngân sách tháng với cảnh báo tự động khi đạt 80% và 100%.
  * Tìm hiểu thêm tại [Usage & Budget](usage-budget/README.md).

* **Mạng riêng tư (Private Networking):** VPC Peering cho Agent Runtime và MCP Gateway — cho phép agent kết nối đến internal service mà không cần expose ra internet.
  * Tìm hiểu thêm tại [Mạng riêng tư](agent-base/private-networking.md).

***

## Tháng 4, 2026

**GreenNode AgentBase — OpenClaw 1-Click**

GreenNode ra mắt **OpenClaw 1-Click** trên AgentBase, cho phép triển khai AI Agent cá nhân dựa trên OpenClaw ngay từ **Agent Marketplace** — không cần kiến thức kỹ thuật, không cần cài đặt thủ công, chỉ trong 40–60 giây.

**Tính năng mới:**

* **OpenClaw 1-Click:** Deploy OpenClaw instance trực tiếp từ Marketplace với cấu hình tối giản.
  * **Tự động kết nối GreenNode MaaS:** Tài khoản GreenNode được tự động cấp quyền truy cập model AI, không cần cấu hình API key thủ công. Model mặc định: **qwen3-5-27b**.
  * **BYOK — Bring Your Own Key:** Hỗ trợ mang API key từ provider bên ngoài (OpenAI, Anthropic, Gemini...).
  * **Tích hợp Channel:** Cấu hình kết nối Telegram và Zalo ngay trong bước deploy.
  * **My Agents:** Quản lý toàn bộ OpenClaw instance với filter theo trạng thái, stop, restart và xóa.
  * Tìm hiểu thêm tại [OpenClaw 1-Click](agent-base/agent-runtime/openclaw/openclaw-1-click.md).

***

## Tháng 3, 2026

**GreenNode AgentBase — Phase 1**

GreenNode AgentBase ra mắt **Phase 1** — nền tảng hạ tầng chuyên biệt dành cho AI Agent, giúp developer triển khai và vận hành AI Agent trên cloud mà không cần tự quản lý server, scaling hay credential.

**Tính năng mới:**

* **Agent Runtime:** Deploy agent dưới dạng container với autoscaling, versioning và zero-downtime deployment; hỗ trợ Custom Agent và OpenClaw 1-Click.
* **Access Control & Team Permissions:** Quản lý danh tính agent, tự động inject credentials vào container; phân quyền thành viên theo Role với Service Accounts.
* **Memory Service:** Lưu trữ lịch sử hội thoại (short-term) và trích xuất facts ngữ nghĩa (long-term).
* **GreenNode MaaS Integration:** Kết nối trực tiếp với LLM models qua API tương thích OpenAI.
* Tìm hiểu thêm tại [GreenNode AgentBase](agent-base/README.md).
