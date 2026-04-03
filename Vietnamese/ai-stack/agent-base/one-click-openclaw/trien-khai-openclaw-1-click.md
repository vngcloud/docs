# Triển khai và Quản lý OpenClaw

OpenClaw 1-Click cho phép triển khai AI Agent cá nhân trên GreenNode Agentbase trong 40–60 giây, tự động kết nối GreenNode MaaS mà không cần cấu hình thủ công.

Để tìm hiểu thêm về khái niệm, kiến trúc và so sánh các tùy chọn deploy, vui lòng tham khảo tại [OpenClaw 1-Click](openclaw-1-click.md).

***

## Triển khai OpenClaw Instance

### Truy cập Agent Marketplace

Bạn truy cập Agent Marketplace theo 2 cách:

* **Cách 1**: Truy cập trang chủ GreenNode tại [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/). Tại giao diện chính, tìm đến **AI Stack** và chọn **Agentbase** → **Agent Marketplace**.
* **Cách 2**: Truy cập trực tiếp tại [https://aiplatform.console.vngcloud.vn/agent-marketplace](https://aiplatform.console.vngcloud.vn/agent-marketplace).

<figure><img src="../../../.gitbook/assets/Screenshot 2026-04-03 154428.png" alt=""><figcaption></figcaption></figure>

### Deploy OpenClaw Instance

Tại giao diện Agent Marketplace, tìm **OpenClaw Featured Card** hoặc click nút **"Deploy OpenClaw With 1 Click!"** trên Hero Banner. Quá trình deploy trải qua các bước:

#### Bước 1: Cấu hình Deploy

<figure><img src="../../../.gitbook/assets/Screenshot 2026-04-03 154505.png" alt=""><figcaption></figcaption></figure>

Màn hình cấu hình gồm 3 phần:

**Phần 1 — Nguồn AI (AI Source)**

Chọn nguồn AI cho OpenClaw instance:

| Tùy chọn                        | Mô tả                                        | Yêu cầu                 |
| ------------------------------- | -------------------------------------------- | ----------------------- |
| **GreenNode MaaS** (mặc định)   | Tự động kết nối GreenNode Model-as-a-Service | Cần tài khoản GreenNode |
| **BYOK — Nhập API Key của bạn** | Dùng API key từ provider bên ngoài           | Cần API key hợp lệ      |

{% hint style="info" %}
**GreenNode MaaS:** Model mặc định là **qwen3-5-27b**.
{% endhint %}

Khi chọn **BYOK**, bổ sung thêm các thông tin:

* **Provider**: Chọn nhà cung cấp (OpenAI, Anthropic, Gemini, Custom).
* **API Key**: Nhập API key. Hệ thống sẽ validate key trước khi cho phép tiếp tục.
* **Model**: Chọn model tương ứng với provider đã chọn.

{% hint style="warning" %}
**Lưu ý BYOK:** Nếu API key không hợp lệ hoặc hết hạn, hệ thống hiển thị lỗi inline và không cho phép tiếp tục. Hãy kiểm tra lại key trước khi submit.
{% endhint %}

**Phần 2 — Cấu hình Instance**

| Trường           | Mô tả                            | Ghi chú                                                                     |
| ---------------- | -------------------------------- | --------------------------------------------------------------------------- |
| **Tên OpenClaw** | Tên định danh instance           | Auto-fill theo format `openclaw/{username}`, không thể thay đổi sau khi tạo |
| **Flavor**       | Cấu hình tài nguyên (vCPU × RAM) | Mặc định: `2×4`. Có thể chọn `4×8`, `8×16`...                               |

**Phần 3 — Cấu hình Channel (Tùy chọn)**

Cho phép kết nối OpenClaw với Telegram để chat ngay sau khi deploy.

| Trường               | Mô tả                     | Ghi chú                                                   |
| -------------------- | ------------------------- | --------------------------------------------------------- |
| **Channel Provider** | Nền tảng nhắn tin         | Hiện hỗ trợ: Telegram, Zalo                               |
| **Mode**             | Chế độ kết nối            | Pairing (mặc định) hoặc Allow List                        |
| **Bot Token**        | Bot Token kết nối channel | Không bắt buộc. Có thể cấu hình sau tại Settings → Config |

Sau khi điền đầy đủ thông tin, nhấn **"Bắt đầu thiết lập"** để bắt đầu provisioning.

#### Bước 2: Provisioning — Setting Up Your Workspace

Màn hình **"Setting Up Your Workspace"** hiển thị icon xoay trong khi hệ thống tự động chuẩn bị môi trường. Sau khi hoàn tất, bạn nhận được **Gateway Token** và **URL trang web admin OpenClaw** để đăng nhập và sử dụng ngay.

{% hint style="info" %}
**Nếu provisioning thất bại:** Hệ thống hiển thị thông báo lỗi kèm nút **Retry**.
{% endhint %}

#### Bước 3: Deploy Success

<figure><img src="../../../.gitbook/assets/Screenshot 2026-04-03 140457.png" alt=""><figcaption></figcaption></figure>

Sau khi provisioning hoàn tất, màn hình Deploy Success hiển thị thông tin instance:

| Thông tin                | Mô tả                                            |
| ------------------------ | ------------------------------------------------ |
| **Instance Name**        | Tên instance đã tạo (ví dụ: `openclaw/username`) |
| **Trạng thái**           | 🟢 Active                                        |
| **Gateway Token**        | Token đăng nhập vào trang web admin OpenClaw     |
| **OpenClaw Gateway URL** | Link truy cập trang web admin OpenClaw           |
| **Thời gian tạo**        | Timestamp                                        |

Nhấn **"Mở OpenClaw"** để truy cập OpenClaw Gateway Dashboard và bắt đầu sử dụng ngay.

***

## Quản lý OpenClaw Instance

### Truy cập My Agents Dashboard

Tại giao diện Agentbase, chọn **My Agents** từ menu điều hướng. Trang này hiển thị danh sách tất cả OpenClaw instances của bạn. Bạn có thể lọc theo trạng thái để xem các instance đang **Active** hoặc đã **Stopped**.

Mỗi instance trong danh sách hiển thị: tên instance, trạng thái, phiên bản, và tags.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-04-03 154608.png" alt=""><figcaption></figcaption></figure>

### Mở lại OpenClaw

1. Tại My Agents, tìm instance muốn truy cập.
2. Click **"Open"** trên instance.
3. Hệ thống redirect thẳng vào trang web admin OpenClaw — không cần qua wizard hay provisioning lại.

### Dừng Instance (Stop)

1. Tại My Agents, tìm instance muốn dừng.
2. Click **"Stop"** trên instance.
3. Xác nhận trong dialog hiện ra.

Sau khi Stop, trạng thái instance chuyển sang **Stopped** và URL của instance không còn accessible.

### Khởi động lại Instance (Restart)

1. Tại My Agents, lọc theo trạng thái **Stopped** để tìm instance.
2. Click **"Restart"** trên instance.
3. Instance chuyển qua trạng thái **Starting → Active**.

Sau khi Restart, URL hoạt động trở lại.

### Xóa Instance (Delete)

1. Tại My Agents, click **"Delete"** trên instance muốn xóa.
2. Hệ thống hiển thị dialog xác nhận yêu cầu nhập **tên instance**.
3. Nhập đúng tên instance và click **"Delete"** (màu đỏ) để hoàn tất.

{% hint style="warning" %}
**Lưu ý khi xóa:**

* Hành động xóa **không thể hoàn tác**.
* Toàn bộ dữ liệu của instance sẽ bị **xóa vĩnh viễn**.
{% endhint %}
