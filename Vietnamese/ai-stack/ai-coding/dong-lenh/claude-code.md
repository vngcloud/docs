# Kết nối Claude Code với GreenNode MaaS (GLM 5.2)

> Dành cho người dùng terminal (macOS / Linux / WSL / Windows). Claude Code CLI sẽ dùng model **GLM 5.2** của GreenNode qua MaaS thay vì gọi thẳng Anthropic.

{% hint style="info" %}
**Trước tiên hãy chuẩn bị [Điều kiện cần](../bat-dau.md):** API key (ACTIVE), Base URL, và model GLM 5.2 đã ENABLED.
{% endhint %}

| Thông tin | Giá trị |
|-----------|---------|
| Base URL | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` (chuẩn Anthropic, **không** `/v1`) |
| API key | key của bạn |
| Model ID | `z-ai/glm-5.2` |

{% hint style="info" %}
**GLM 5.2 chỉ là model ví dụ.** GreenNode có nhiều model — bạn thay bằng model mình muốn. Model ID và Base URL của từng model đều xem được trong [trang chi tiết model](https://aiplatform.console.greennode.ai/models).
{% endhint %}

---

## Bước 1 — Cài Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

---

## Bước 2 — Khai báo Base URL & API key

Chọn đúng mục theo hệ điều hành của bạn.

{% tabs %}
{% tab title="macOS / Linux / WSL (bash hoặc zsh)" %}
Chạy tạm cho phiên hiện tại:

```bash
export ANTHROPIC_BASE_URL="https://maas-llm-aiplatform-hcm.api.vngcloud.vn"
export ANTHROPIC_AUTH_TOKEN="--"   # thay bằng API key của bạn
```

Để tự động mỗi lần mở terminal, thêm 2 dòng trên vào cuối `~/.zshrc` (macOS) hoặc `~/.bashrc` (Linux/WSL), rồi nạp lại:

```bash
source ~/.zshrc      # hoặc: source ~/.bashrc
```
{% endtab %}

{% tab title="Windows PowerShell" %}
Chạy tạm cho cửa sổ PowerShell hiện tại:

```powershell
$env:ANTHROPIC_BASE_URL = "https://maas-llm-aiplatform-hcm.api.vngcloud.vn"
$env:ANTHROPIC_AUTH_TOKEN = "--"   # thay bằng API key của bạn
```

Để lưu vĩnh viễn cho tài khoản (chỉ chạy một lần, rồi **mở lại PowerShell**):

```powershell
[Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "https://maas-llm-aiplatform-hcm.api.vngcloud.vn", "User")
[Environment]::SetEnvironmentVariable("ANTHROPIC_AUTH_TOKEN", "--", "User")
```
{% endtab %}
{% endtabs %}

---

## Bước 3 — Chạy Claude Code với GLM 5.2

Trong thư mục project, chạy:

```bash
claude --model z-ai/glm-5.2
```

{% hint style="info" %}
Cờ `--model z-ai/glm-5.2` chỉ định model cho phiên hiện tại. Trong Claude Code bạn cũng có thể đổi model bằng lệnh `/model`.
{% endhint %}

---

## Bước 4 — Kiểm tra

Trong Claude Code, gõ `/status` — đúng khi:

* Base URL trỏ về `maas-llm-aiplatform-hcm.api.vngcloud.vn`
* Model là `z-ai/glm-5.2`

Sau đó vào **[AI Platform Console](https://aiplatform.console.greennode.ai/)** để thấy lượt gọi được ghi nhận.

---

## Xử lý sự cố

| Hiện tượng | Nguyên nhân | Cách xử lý |
|------------|-------------|------------|
| `401` / "Unauthorized" | API key sai hoặc chưa ACTIVE | Kiểm tra `ANTHROPIC_AUTH_TOKEN`; đợi key **ACTIVE** |
| `404` / "Not Found" | Base URL sai (thừa `/v1` hoặc `/` cuối) | Đúng phải là `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` |
| Request đi thẳng Anthropic | Còn biến `ANTHROPIC_API_KEY` cũ | Chạy `unset ANTHROPIC_API_KEY` (macOS/Linux) hoặc xoá biến đó trong Windows |
| Sai model được dùng | Thiếu cờ `--model` | Chạy `claude --model z-ai/glm-5.2` hoặc dùng `/model` để đổi |
| AI không phản hồi | Hết credit nên model bị tắt | Nạp credit tại AI Platform Console |
| Connection timeout | Không ra được mạng tới MaaS | Kiểm tra VPN / mạng tới `*.api.vngcloud.vn` |

---

| Tôi muốn tiếp theo... | Đi đến |
|------------------------|--------|
| Dùng bản có giao diện | [Claude Desktop](../co-giao-dien/claude-desktop.md) |
| Dùng OpenCode | [OpenCode](opencode.md) |
| Xem điều kiện cần | [Bắt đầu với AI Coding](../bat-dau.md) |

---

## Cần hỗ trợ?

Nếu bạn làm theo mà vẫn chưa được, đừng ngại liên hệ bộ phận Hỗ trợ Khách hàng của GreenNode:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Trung tâm hỗ trợ: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Cảm ơn bạn đã sử dụng dịch vụ của GreenNode.
