# Dùng MCP Server với AI Coding

> **MCP (Model Context Protocol)** cho phép agent AI Coding của bạn kết nối tới các công cụ và nguồn dữ liệu bên ngoài — ví dụ tra cứu web, đọc/ghi file, truy vấn database, hay thao tác với Jira, GitHub… Đây là cách "mở rộng khả năng" cho agent, **khác** với việc gắn model.

{% hint style="info" %}
Phân biệt cho dễ nhớ:
* **Gắn model (GLM 5.2)** = cho agent một **bộ não** để suy nghĩ → xem [Bắt đầu với AI Coding](bat-dau.md).
* **Gắn MCP server** = cho agent thêm **tay chân** để làm việc với hệ thống bên ngoài (chủ đề của trang này).

Hai việc độc lập nhau: bạn có thể dùng GLM 5.2 mà không cần MCP, và ngược lại.
{% endhint %}

---

## 1. MCP server là gì

Một **MCP server** là một chương trình nhỏ cung cấp cho agent một bộ "công cụ" (tools). Khi bạn hỏi agent một việc cần dữ liệu ngoài, agent sẽ tự gọi công cụ tương ứng qua MCP server đó. Có 2 loại phổ biến:

| Loại | Chạy ở đâu | Ví dụ |
|------|-----------|-------|
| **Local (stdio)** | Ngay trên máy bạn | đọc file, chạy lệnh, truy cập DB nội bộ |
| **Remote (HTTP/SSE)** | Trên một server từ xa | connector doanh nghiệp (Jira, GitHub, tìm kiếm nội bộ) |

---

## 2. Điều kiện cần

* Đã gắn model GLM 5.2 cho agent theo [Bắt đầu với AI Coding](bat-dau.md).
* Thông tin của MCP server muốn thêm (lệnh chạy nếu là local; hoặc URL + token nếu là remote).

---

## 3. Thêm MCP server

### Trên Claude Desktop (giao diện)

1. Bật **Developer Mode** (giống khi cấu hình model): **Help → Troubleshooting → Enable Developer Mode**.
2. Vào **Developer → cấu hình MCP server (Local MCP)** và khai báo server: tên, lệnh chạy (local) hoặc URL (remote).
3. Khởi động lại app. Trong phiên làm việc, agent sẽ tự dùng công cụ từ MCP server khi cần.

### Trên Claude Code (dòng lệnh)

Thêm nhanh một MCP server bằng lệnh:

```bash
claude mcp add <tên-server> -- <lệnh-chạy-server>
```

Xem danh sách server đã thêm:

```bash
claude mcp list
```

---

## 4. Quản trị MCP trong GreenNode

Nếu bạn triển khai MCP ở quy mô tổ chức (kiểm soát server nào được phép, phân quyền theo tool, đặt qua gateway chung), hãy xem phần **MCP Governance** của AgentBase:

* [MCP Gateway](../agent-base/mcp-governance/mcp-gateway/README.md)
* [Policy Groups](../agent-base/mcp-governance/policy-groups/README.md)

---

## Cần hỗ trợ?

Nếu bạn làm theo mà vẫn chưa được, đừng ngại liên hệ bộ phận Hỗ trợ Khách hàng của GreenNode:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Trung tâm hỗ trợ: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Cảm ơn bạn đã sử dụng dịch vụ của GreenNode.
