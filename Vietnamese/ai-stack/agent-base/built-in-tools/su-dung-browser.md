# Sử dụng Browser

> Hướng dẫn kết nối agent của bạn với **Browser** — điều khiển Chrome thật trong microVM riêng cho từng session: automation qua CDP, xem trực tiếp màn hình (live view) và xem lại bản ghi (recording), tích hợp qua MCP.

---

## Điều kiện cần

- Tài khoản GreenNode và đã hoàn thành [Bắt đầu với AgentBase](../getting-started.md)
- Account đã được bật whitelist sử dụng Built-in Tools — xem [Built-in Tools](README.md) nếu chưa được bật
- Agent của bạn hỗ trợ MCP client (Claude Code, Cursor, hoặc MCP SDK)
- Nếu agent tự viết automation: dùng client **Chrome DevTools Protocol (CDP)** — Playwright, Puppeteer hoặc client CDP bất kỳ

---

## Kết nối qua MCP

**Bước 1:** Lấy endpoint MCP của Browser:

```
https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/browser
```

**Bước 2:** Thêm vào cấu hình MCP client của bạn. Ví dụ với Claude Code:

```bash
claude mcp add --transport http browser \
  https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/browser
```

Hoặc với Cursor / VS Code — chỉ cần `url`:

```json
{
  "mcpServers": {
    "browser": {
      "url": "https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/browser"
    }
  }
}
```

**Bước 3:** Đăng nhập lần đầu — client tự chạy flow đăng nhập (**Dynamic Client Registration**) và mở URL login của GreenNode Portal trên trình duyệt; access token được giữ và **tự refresh** sau đó. Token từ **Root user, IAM user hoặc Service Account** đều dùng được.

---

## Mô hình hoạt động

Mỗi **session** là một trình duyệt Chrome thật chạy trong một microVM riêng. Có 3 luồng riêng biệt:

```
Agent ──── automation stream (CDP, cổng 9222) ────┐
Người xem ── live view (noVNC, cổng 6080) ────────┤── Chrome trong microVM
Ghi hình ── recording (lưu khi xoá session) ──────┘
```

- **Automation stream** — agent điều khiển Chrome: relay kết nối CDP của client vào cổng debug của Chrome trong VM. Playwright / Puppeteer dùng được như localhost.
- **Live view** — người xem màn hình Chrome trực tiếp qua noVNC, nhúng trong portal bằng iframe.
- **Recording** — bản ghi phiên được lưu lại khi session kết thúc.

Browser dùng cùng khuôn với [Code Interpreter](su-dung-code-interpreter.md): tạo tài nguyên, chờ `ACTIVE`, tạo session (một VM mỗi session), xoá khi hết dùng.

---

## Điều khiển Chrome bằng automation stream

**Bước 1:** Tạo Browser và session (giống Code Interpreter: tạo → chờ `ACTIVE` → tạo session).

**Bước 2:** Bật automation stream cho session (tool/API `PUT .../sessions/{sessionId}/streams`). Luồng này bật/tắt được cho từng session.

**Bước 3:** Trỏ client CDP (Playwright, Puppeteer) vào địa chỉ automation stream của session. Service relay kết nối của bạn tới Chrome trong VM và tự viết lại địa chỉ debugger để trỏ ngược về chính nó.

---

## Xem trực tiếp (live view)

Màn hình Chrome được phục vụ qua noVNC và nhúng trong portal bằng iframe. Vì iframe và WebSocket không thể gắn header xác thực, live view dùng **URL đã ký** (kiểu presigned URL):

1. Portal ký URL live view cho session (ticket hiệu lực **5 phút**).
2. URL được đặt vào `iframe src` — ticket đi theo đường dẫn WebSocket và bị cắt bỏ trước khi vào VM.
3. Kết nối đã thiết lập thì không xác thực lại; mỗi kết nối giữ tối đa **1 giờ**. Hết hạn thì portal ký URL mới và tải lại iframe.

---

## Ghi hình (recording)

File ghi hình nằm bên trong VM nên sẽ mất khi VM bị xoá. Vì thế, **khi bạn xoá session**, service đọc file ghi hình ra ngay trước khi huỷ VM rồi lưu lên object storage. Sau đó lấy bản ghi bằng `GET .../sessions/{sessionId}/recording`.

{% hint style="warning" %}
Recording là **best effort**: nếu không đọc/lưu được file, việc xoá session vẫn tiếp tục và không có bản ghi. Bản ghi lớn hơn 64 MiB (giá trị cấu hình mặc định) không được lưu.
{% endhint %}

---

## API chính

| Đường dẫn dưới `/v1/browsers` | Mục đích |
|---|---|
| `POST`, `GET`, `GET /{id}`, `DELETE /{id}` | Tạo, liệt kê, xem, xoá Browser |
| `POST/GET/DELETE /{id}/sessions[/{sessionId}]` | Quản lý session — mỗi session một Chrome trong một VM |
| `PUT /{id}/sessions/{sessionId}/streams` | Bật/tắt automation stream |
| `/{id}/sessions/{sessionId}/automation-stream[/*]` | Relay CDP, mọi method |
| `POST .../live-view-stream-sign` và `GET .../live-view-stream[/*]` | Ký URL xem trực tiếp, và luồng xem |
| `GET .../recording` | Lấy bản ghi đã lưu |

---

## Xoá

1. Xoá session — service lưu recording lại (nếu bật), huỷ VM và toàn bộ trạng thái.
2. Xoá Browser khi hết cần — trả lại quota.

---

## Kết quả

Agent của bạn điều khiển được Chrome thật (CDP), bạn xem được màn hình trực tiếp trong portal và tải lại bản ghi phiên sau khi kết thúc.

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Cho agent chạy Python / shell | [Sử dụng Code Interpreter](su-dung-code-interpreter.md) |
| Xem toàn bộ giới hạn và mô hình bảo mật | [Sandbox: bảo mật và giới hạn](sandbox-bao-mat-va-gioi-han.md) |
