# OpenClaw 1-Click

## Tổng quan

**OpenClaw 1-Click** là tính năng cho phép triển khai AI Agent cá nhân dựa trên OpenClaw ngay từ **Agent Marketplace** của GreenNode AgentBase — không cần kiến thức kỹ thuật, không cần cài đặt thủ công, chỉ trong **40–60 giây**.

### OpenClaw là gì?

[OpenClaw](https://open.claw.cloud/) là một open-source AI agent có khả năng tự động hoàn thành các tác vụ: duyệt web, quản lý file, chạy lệnh, viết code, và tích hợp messaging (Telegram, Zalo). Thay vì cài đặt OpenClaw trên máy tính cá nhân, GreenNode AgentBase cho phép bạn chạy OpenClaw trên cloud với đầy đủ tài nguyên và kết nối sẵn với GreenNode MaaS (Model-as-a-Service).

Để khởi tạo và quản lý OpenClaw instance, vui lòng tham khảo hướng dẫn [tại đây](trien-khai-openclaw-1-click.md).

### So sánh cài thủ công và 1-Click Deploy

| Tiêu chí | Tự cài OpenClaw (Local) | OpenClaw 1-Click (AgentBase) |
| --- | --- | --- |
| **Thời gian setup** | 30–60 phút | 40–60 giây |
| **Yêu cầu kỹ thuật** | Cần kiến thức DevOps | Không cần |
| **Cấu hình API key** | Thủ công | Tự động kết nối GreenNode MaaS |
| **Hạ tầng** | Máy tính cá nhân | Cloud (GreenNode AgentBase) |
| **Tích hợp messaging** | Tự cấu hình | Telegram, Zalo — cấu hình ngay khi deploy |
| **Quản lý instance** | Tự quản lý | Qua My Agents Dashboard |

### Khi nào nên sử dụng OpenClaw 1-Click?

* **Người dùng phổ thông**: Muốn dùng AI Agent ngay mà không cần cài đặt hay cấu hình kỹ thuật.
* **Developer**: Muốn có OpenClaw chạy trên cloud, kết nối sẵn LLM model mà không phải tự dựng infra.
* **Người dùng ngoài GreenNode**: Muốn dùng model từ provider khác (OpenAI, Anthropic, Gemini) — hỗ trợ BYOK.

***

## Kiến trúc OpenClaw 1-Click

Khi bạn nhấn Deploy, hệ thống AgentBase tự động thực hiện 4 bước provisioning:

| Bước | Task | Mô tả |
| --- | --- | --- |
| 1 | **OpenClaw Token** | Tạo Identity và token xác thực cho instance |
| 2 | **AI Service Account** | Tạo IAM Service Account kết nối GreenNode MaaS |
| 3 | **AI Service Token** | Lấy access token cho model AI đã chọn |
| 4 | **Cloud Computer** | Khởi động container OpenClaw trên AgentBase Runtime |

Sau khi hoàn tất, bạn nhận được **OpenClaw Gateway URL** để truy cập portal chat ngay lập tức.

***

## Hai nguồn AI hỗ trợ

### GreenNode MaaS (Mặc định)

Dành cho người dùng có tài khoản GreenNode. Hệ thống tự động tạo API key và kết nối với GreenNode Model-as-a-Service — bạn không cần copy/paste bất kỳ key nào.

### BYOK — Bring Your Own Key

Dành cho người muốn dùng model từ provider bên ngoài. Bạn tự cung cấp API key khi cấu hình.

| Provider hỗ trợ | Ví dụ model |
| --- | --- |
| OpenAI | gpt-4o, gpt-4.1 |
| Anthropic | claude-sonnet-4, claude-opus-4 |
| Gemini | gemini-2.0-flash |
| Custom | Tùy chỉnh endpoint |

***

## Tích hợp Channel

OpenClaw hỗ trợ kết nối với các nền tảng nhắn tin để bạn có thể chat với AI Agent ngay trên ứng dụng quen thuộc:

| Channel | Mô tả |
| --- | --- |
| **Telegram** | Kết nối qua Telegram Bot Token. Hỗ trợ mode Pairing và Allow List |
| **Zalo** | Kết nối qua Zalo |

Channel có thể được cấu hình ngay trong bước deploy hoặc sau đó tại **Settings → Config** trong OpenClaw Gateway.

***

## FAQ

### 1. Tôi không có tài khoản GreenNode, có dùng được không?

**Có.** Bạn chọn **BYOK** khi cấu hình và nhập API key từ provider bên ngoài (OpenAI, Anthropic, Gemini...).

### 2. Tôi có thể deploy nhiều OpenClaw instance không?

**Có.** Một user có thể deploy nhiều instance. Bạn quản lý tất cả từ **My Agents Dashboard**.

### 3. Instance của tôi tự dừng, tôi có mất dữ liệu không?

Dữ liệu của instance được giữ lại sau auto-shutdown. Bạn Restart từ My Agents Dashboard để tiếp tục sử dụng.

### 4. Tôi có thể tích hợp Telegram hoặc Zalo không?

**Có.** Bạn có thể cấu hình ngay trong bước deploy hoặc sau đó tại **Settings → Config** trong OpenClaw Gateway. Hiện hỗ trợ Telegram và Zalo.

Xem thêm giới hạn và lưu ý kỹ thuật tại [Giới hạn và Lưu ý](gioi-han-va-luu-y.md).
