# MCP Governance

MCP Governance giúp bạn kiểm soát toàn bộ traffic từ AI agent đến external services — xác thực, phân quyền và ghi log — mà không cần sửa code của agent.

---

## Tổng quan

Khi agent gọi **MCP Tool Servers** (web search, database, file system, v.v.) trực tiếp mà không có lớp kiểm soát trung gian, bạn không có cách nào biết agent nào đang gọi tool nào, không thể giới hạn quyền truy cập, và không có audit trail khi sự cố xảy ra.

MCP Governance cung cấp một **control plane tập trung** nằm giữa agent và external services, bao gồm hai thành phần chính:

| Thành phần | Chức năng |
|---|---|
| **MCP Gateway** | Proxy tập trung cho tất cả MCP tool calls — xác thực inbound từ agent, xác thực outbound đến MCP server, gắn Policy Group để kiểm soát quyền truy cập |
| **Policy Group** | Bộ rules operator-first xác định agent nào được gọi tool nào, trong điều kiện nào — attach vào MCP Gateway để enforce tự động |

---

## Phạm vi

- MCP Gateway CRUD (tạo / xem / sửa / xóa)
- Gắn Policy Group vào MCP Gateway

---

## Bắt đầu với MCP Governance

| Tôi muốn... | Đi đến |
|---|---|
| Hiểu MCP Gateway hoạt động như thế nào | [MCP Gateway](mcp-gateway/README.md) |
| Tạo MCP Gateway đầu tiên | [Quản lý MCP Gateway](mcp-gateway/quan-ly-mcp-gateway.md) |
