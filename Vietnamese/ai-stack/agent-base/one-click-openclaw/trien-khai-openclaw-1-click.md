# Triển khai và Quản lý OpenClaw 1-Click

OpenClaw 1-Click cho phép triển khai AI Agent cá nhân trên GreenNode AgentBase trong 40–60 giây, tự động kết nối GreenNode MaaS mà không cần cấu hình thủ công.

Để tìm hiểu thêm về khái niệm, kiến trúc và so sánh các tùy chọn deploy, vui lòng tham khảo tại [OpenClaw 1-Click](openclaw-1-click.md).

***

## Triển khai OpenClaw Instance

### Truy cập Agent Marketplace

Bạn truy cập Agent Marketplace theo 2 cách:

* **Cách 1**: Truy cập trang chủ GreenNode tại [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/). Tại giao diện chính, tìm đến **AI Stack** và chọn **AgentBase** → **Agent Marketplace**.
* **Cách 2**: Truy cập trực tiếp tại [https://aiplatform.console.vngcloud.vn/agent-marketplace](https://aiplatform.console.vngcloud.vn/agent-marketplace).

### Deploy OpenClaw Instance

Tại giao diện Agent Marketplace, tìm **OpenClaw Featured Card** hoặc click nút **"Deploy OpenClaw With 1 Click!"** trên Hero Banner. Quá trình deploy trải qua các bước:

#### Bước 1: Cấu hình Deploy

Màn hình cấu hình gồm 3 phần:

**Phần 1 — Nguồn AI (AI Source)**

Chọn nguồn AI cho OpenClaw instance:

| Tùy chọn | Mô tả | Yêu cầu |
| --- | --- | --- |
| **GreenNode MaaS** (mặc định) | Tự động kết nối GreenNode Model-as-a-Service | Cần tài khoản GreenNode |
| **BYOK — Nhập API Key của bạn** | Dùng API key từ provider bên ngoài | Cần API key hợp lệ |

{% hint style="info" %}
**GreenNode MaaS:** Model mặc định là **Qwen-3-27b**.
{% endhint %}

Khi chọn **BYOK**, bổ sung thêm các thông tin:

* **Provider**: Chọn nhà cung cấp (OpenAI, Anthropic, Gemini, Custom).
* **API Key**: Nhập API key. Hệ thống sẽ validate key trước khi cho phép tiếp tục.
* **Model**: Chọn model tương ứng với provider đã chọn.

{% hint style="warning" %}
**Lưu ý BYOK:** Nếu API key không hợp lệ hoặc hết hạn, hệ thống hiển thị lỗi inline và không cho phép tiếp tục. Hãy kiểm tra lại key trước khi submit.
{% endhint %}

**Phần 2 — Cấu hình Instance**

| Trường | Mô tả | Ghi chú |
| --- | --- | --- |
| **Tên OpenClaw** | Tên định danh instance | Auto-fill theo format `openclaw/{username}`, có thể đổi. Không được trùng tên instance đang Running |
| **Flavor** | Cấu hình tài nguyên (vCPU × RAM) | Mặc định: `2×4`. Có thể chọn `4×8`, `8×16`... |

**Phần 3 — Cấu hình Channel (Tùy chọn)**

Cho phép kết nối OpenClaw với Telegram để chat ngay sau khi deploy.

| Trường | Mô tả | Ghi chú |
| --- | --- | --- |
| **Channel Provider** | Nền tảng nhắn tin | Hiện hỗ trợ: Telegram, Zalo |
| **Mode** | Chế độ kết nối | Pairing (mặc định) hoặc Allow List |
| **Bot Token** | Telegram Bot Token | Không bắt buộc. Có thể cấu hình sau tại Settings → Config |

Sau khi điền đầy đủ thông tin, nhấn **"Bắt đầu thiết lập"** để bắt đầu provisioning.

#### Bước 2: Provisioning — Setting Up Your Workspace

Màn hình **"Setting Up Your Workspace"** hiển thị tiến độ provisioning theo 4 tasks:

| Task | Mô tả | Trạng thái |
| --- | --- | --- |
| **OpenClaw Token** | Tạo Identity và token xác thực cho instance | ◌ Đang xử lý / ✓ Hoàn thành / ✗ Lỗi |
| **AI Service Account** | Tạo IAM Service Account kết nối MaaS | ◌ Đang xử lý / ✓ Hoàn thành / ✗ Lỗi |
| **AI Service Token** | Lấy access token cho model AI đã chọn | ◌ Đang xử lý / ✓ Hoàn thành / ✗ Lỗi |
| **Cloud Computer** | Khởi động container OpenClaw | ◌ Đang xử lý / ✓ Hoàn thành / ✗ Lỗi |

Hệ thống tự động kiểm tra trạng thái mỗi 3 giây. Khi tất cả 4 tasks hoàn thành, bạn được tự động chuyển đến màn hình Deploy Success.

{% hint style="info" %}
**Nếu provisioning thất bại:** Hệ thống hiển thị trạng thái lỗi kèm link **Troubleshoot** và nút **Retry**. Instance lỗi không được tính vào quota của bạn.
{% endhint %}

#### Bước 3: Deploy Success

Sau khi provisioning hoàn tất, màn hình Deploy Success hiển thị thông tin instance:

| Thông tin | Mô tả |
| --- | --- |
| **Instance Name** | Tên instance đã tạo (ví dụ: `openclaw-nguyenvana-001`) |
| **Trạng thái** | 🟢 ONLINE |
| **AI Model** | Model và nguồn AI đang dùng |
| **OpenClaw Gateway URL** | Link truy cập OpenClaw Gateway Dashboard |
| **Thời gian tạo** | Timestamp |

Nhấn **"Mở OpenClaw"** để truy cập OpenClaw Gateway Dashboard và bắt đầu sử dụng ngay.

***

## Quản lý OpenClaw Instance

### Truy cập My Agents Dashboard

Tại giao diện AgentBase, chọn **My Agents** từ menu điều hướng. Trang này hiển thị tất cả OpenClaw instances của bạn theo 2 section:

| Section | Điều kiện | Mô tả |
| --- | --- | --- |
| **Running 🟢** | Có ít nhất 1 instance đang chạy | Hiển thị instance card với nút "Open" |
| **Stopped ⚪** | Có ít nhất 1 instance đã dừng | Hiển thị instance card với nút "Restart" |

Mỗi instance card hiển thị: tên instance, trạng thái, AI model đang dùng, phiên bản, và tags.

### Mở lại OpenClaw

1. Tại My Agents Dashboard, tìm instance muốn truy cập trong section **Running**.
2. Click **"Open"** trên instance card.
3. Hệ thống redirect thẳng vào OpenClaw Gateway Dashboard — không cần qua wizard hay provisioning lại.

### Dừng Instance (Stop)

1. Tại My Agents Dashboard, tìm instance trong section **Running**.
2. Click **"Stop"** trên instance card.
3. Xác nhận trong dialog hiện ra.

Sau khi Stop, instance chuyển sang section **Stopped** và URL của instance không còn accessible.

### Khởi động lại Instance (Restart)

1. Tại My Agents Dashboard, tìm instance trong section **Stopped**.
2. Click **"Restart"** trên instance card.
3. Instance chuyển qua trạng thái **Starting → Running**.

Sau khi Restart, URL hoạt động trở lại và card chuyển lên section **Running**.

### Xóa Instance (Delete)

1. Tại My Agents Dashboard, click **"Delete"** trên instance card (Running hoặc Stopped).
2. Hệ thống hiển thị dialog xác nhận yêu cầu nhập **tên instance**.
3. Nhập đúng tên instance và click **"Delete"** (màu đỏ) để hoàn tất.

{% hint style="warning" %}
**Lưu ý khi xóa:**

* Hành động xóa **không thể hoàn tác**.
* Toàn bộ dữ liệu trên persistent disk của instance sẽ bị **xóa vĩnh viễn**.
* Quota (1 instance/user) được trả về sau khi xóa, cho phép bạn deploy instance mới.
{% endhint %}

### Auto-shutdown

Nếu instance không nhận request trong **24 giờ liên tục**, hệ thống tự động dừng instance và gửi email thông báo. Bạn có thể Restart từ My Agents Dashboard bất cứ lúc nào.
