# Kết nối Codex Desktop với GreenNode MaaS (GLM 5.2)

> Dành cho **người mới bắt đầu** dùng macOS hoặc Windows. Cấu hình bằng cách sửa 1 file `config.toml` qua Settings — có thể nhờ AI hỗ trợ soạn, không cần thuộc cú pháp TOML. Codex Desktop sẽ dùng model **GLM 5.2** chạy nội bộ của GreenNode.

{% hint style="info" %}
**Trước tiên hãy chuẩn bị [Điều kiện cần](../bat-dau.md):** API key (ACTIVE), Base URL, và model GLM 5.2 đã ENABLED. Trang này chỉ hướng dẫn cài và cấu hình.
{% endhint %}

Bạn sẽ cần 3 giá trị này (lấy ở trang Điều kiện cần):

| Thông tin | Giá trị |
|-----------|---------|
| Base URL (chuẩn OpenAI) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` (**có** `/v1`) |
| API key | key `vn-...` của bạn |
| Model ID | `z-ai/glm-5.2` |

{% hint style="info" %}
**GLM 5.2 chỉ là model ví dụ.** GreenNode có nhiều model — bạn thay bằng model mình muốn. Model ID và Base URL của từng model đều xem được trong [trang chi tiết model](https://aiplatform.console.greennode.ai/models).
{% endhint %}

---

## Bước 1 — Tải và cài Codex Desktop

Vào **[openai.com/index/introducing-the-codex-app](https://openai.com/index/introducing-the-codex-app/)** và tải app cho máy của bạn, cài như phần mềm bình thường.

---

## Bước 2 — Mở app và đăng nhập

Mở Codex, đăng nhập bằng tài khoản ChatGPT/OpenAI của bạn.

<figure><img src="../../../.gitbook/assets/ai-coding/codex-ui-chat.png" alt=""><figcaption><p>Màn hình chính Codex sau khi đăng nhập</p></figcaption></figure>

---

## Bước 3 — Mở file config.toml

1. Bấm avatar/tên tài khoản ở góc dưới bên trái → **Settings**.
2. Ở ô tìm kiếm bên trái, gõ **"config.toml"**.
3. Bấm nút **Open config.toml** ở góc trên bên phải mục **Custom config.toml settings** — file sẽ mở bằng trình soạn thảo mặc định của máy.

<figure><img src="../../../.gitbook/assets/ai-coding/find-config-toml-file.png" alt=""><figcaption><p>Tìm và mở config.toml trong Settings</p></figcaption></figure>

---

## Bước 4 — Thêm cấu hình model self-host

Thêm đoạn sau vào **cuối** file `config.toml` (giữ nguyên nội dung có sẵn phía trên):

```toml
[model_providers.vngcloud-glm]
name = "VNGCloud GLM"
base_url = "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1"
experimental_bearer_token = "vn-...key-của-bạn..."
wire_api = "responses"
stream_idle_timeout_ms = 3000000
request_max_retries = 3
supports_websockets = false

[profiles.glm]
model = "z-ai/glm-5.2"
model_provider = "vngcloud-glm"
model_context_window = 200000
model_auto_compact_token_limit = 200000
model_reasoning_effort = "medium"
model_reasoning_summary = "auto"
```

**Giải thích các field quan trọng:**

| Field | Mục đích |
|---|---|
| `model_providers.vngcloud-glm` | Tên provider tuỳ bạn đặt — dùng lại ở `model_provider` bên dưới |
| `base_url` | Base URL chuẩn OpenAI, **có** `/v1` |
| `experimental_bearer_token` | API key của bạn, dán trực tiếp vào file — Codex Desktop không cần export biến môi trường như CLI |
| `wire_api` | Để `"responses"` — đúng chuẩn Responses API mà Codex Desktop dùng |
| `stream_idle_timeout_ms` | Thời gian chờ tối đa (ms) trước khi coi stream là timeout |
| `request_max_retries` | Số lần retry lại request khi gọi lỗi |
| `supports_websockets` | Để `false` — MaaS chưa hỗ trợ websocket |
| `profiles.glm` | Tên profile tuỳ bạn đặt — sẽ hiện trong model picker của app |
| `model` | Model ID gửi lên MaaS |
| `model_provider` | Trỏ về provider đã khai báo ở trên |
| `model_context_window` | Khai báo thủ công vì MaaS không expose metadata model |
| `model_auto_compact_token_limit` | Ngưỡng token để Codex tự nén (compact) lại context |
| `model_reasoning_effort` | Mức độ suy luận mặc định (`low` / `medium` / `high`) |
| `model_reasoning_summary` | Để `"auto"` — Codex tự quyết có tóm tắt reasoning hay không |

{% hint style="warning" %}
**Đừng copy nguyên mẫu cấu hình theo kiểu biến môi trường của Claude Code** (`export ANTHROPIC_BASE_URL=...`, `claude --model ...`) — đó là cú pháp riêng cho Claude Code CLI, **không** áp dụng được cho Codex. Codex Desktop đọc cấu hình qua `config.toml` với `model_providers` / `profiles` như mẫu trên.
{% endhint %}

{% hint style="info" %}
**Chưa quen cú pháp TOML?** Copy toàn bộ nội dung file `config.toml` hiện tại, dán vào một AI chat (Codex, ChatGPT, Claude...) kèm 3 giá trị Base URL / API key / Model ID ở trên, nhờ AI viết giúp đoạn `[model_providers.*]` và `[profiles.*]` đúng chuẩn Codex rồi dán lại vào file.
{% endhint %}

---

## Bước 5 — Lưu file và khởi động lại Codex

1. Lưu file `config.toml`.
2. Thoát hẳn và mở lại Codex Desktop.

---

## Bước 6 — Kiểm tra

1. Ở khung chat, bấm vào ô chọn model (góc dưới bên phải, ví dụ **"5.6 Terra Medium"**).
2. Tìm profile bạn vừa thêm (ví dụ **glm**) trong danh sách — chọn nó.
3. Gõ thử một câu, ví dụ *"Viết hàm cộng hai số bằng Python."* Nếu trả lời được là thành công.
4. Vào **[AI Platform Console](https://aiplatform.console.greennode.ai/)** để thấy lượt gọi được ghi nhận.

<figure><img src="../../../.gitbook/assets/ai-coding/done-setup-glm-into-codex.png" alt=""><figcaption><p>Cấu hình thành công — chat trả lời được và model picker hiện "Custom" thay vì model mặc định</p></figcaption></figure>

{% hint style="warning" %}
**Lưu ý khi đổi qua lại giữa model mặc định và model self-host:** Nếu bạn chọn một model mặc định của Codex ngay trong model picker (UI), app **chỉ ghi đè field `model`** trong `config.toml`, **không** tự reset `model_provider` về provider mặc định (`openai`). Nếu sau đó muốn quay lại model self-host, bấm chọn qua UI có thể khiến `model` và `model_provider` bị lệch nhau (không khớp provider). Để chắc chắn, khi cần đổi qua lại giữa model mặc định và model self-host, hãy **sửa trực tiếp `model` / `model_provider` trong `config.toml`** (hoặc nhờ AI sửa giúp) thay vì chỉ bấm switch trong model picker.
{% endhint %}

---

## Xử lý sự cố

| Hiện tượng | Nguyên nhân | Cách xử lý |
|------------|-------------|------------|
| Không thấy profile mới trong model picker | Chưa restart app, hoặc sai tên section `[profiles.*]` | Thoát hẳn và mở lại Codex; kiểm tra lại cú pháp TOML |
| `401` / "Unauthorized" | API key sai hoặc chưa ACTIVE | Kiểm tra lại key; đợi trạng thái **ACTIVE** |
| `404` / "Not Found" | Base URL sai (thiếu `/v1`) | Đúng phải là `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| App báo lỗi khi mở / không đọc được config | Sai cú pháp TOML (thiếu dấu `"`, sai indent) | Nhờ AI kiểm tra lại đoạn vừa thêm, hoặc so lại với mẫu ở Bước 4 |
| AI không phản hồi dù đã chọn đúng model | Hết credit nên model bị tắt | Nạp credit tại AI Platform Console |
| Đổi model qua model picker (UI) xong, model self-host không dùng được nữa | `model` và `model_provider` trong `config.toml` bị lệch nhau — picker chỉ ghi đè `model`, không reset `model_provider` | Mở lại `config.toml`, sửa `model` / `model_provider` cho khớp đúng cặp (xem mẫu ở Bước 4), lưu rồi restart Codex |

---

| Tôi muốn tiếp theo... | Đi đến |
|------------------------|--------|
| Dùng bằng dòng lệnh | [Codex CLI](../dong-lenh/codex-cli.md) |
| Xem điều kiện cần | [Bắt đầu với AI Coding](../bat-dau.md) |
| Xem usage & billing | [AI Platform Console](https://aiplatform.console.greennode.ai/) |

---

## Cần hỗ trợ?

Nếu bạn làm theo mà vẫn chưa được, đừng ngại liên hệ bộ phận Hỗ trợ Khách hàng của GreenNode:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Trung tâm hỗ trợ: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Cảm ơn bạn đã sử dụng dịch vụ của GreenNode.
