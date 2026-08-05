# Bắt đầu với AI Coding (điều kiện cần)

> **Trang gốc.** Đọc trang này một lần để chuẩn bị đủ mọi thứ, sau đó chọn công cụ ở cuối trang. Mọi hướng dẫn công cụ đều giả định bạn đã làm xong 3 bước ở đây.

---

## 1. Hiểu nhanh trong 1 phút

Để dùng AI Coding, bạn ghép 2 thứ lại với nhau:

* **Agent** — phần mềm bạn cài trên máy để "trò chuyện" và nhờ AI làm việc (ví dụ Claude Desktop, Claude Code…).
* **LLM (model)** — bộ não AI thực sự trả lời. Ở đây là **GLM 5.2** do GreenNode tự vận hành, gọi qua hệ thống **MaaS** của GreenNode.

Việc của bạn là **chỉ cho agent quay sang nói chuyện với GLM 5.2 của GreenNode** — bằng cách khai báo 2 thông tin: một **địa chỉ (Base URL)** và một **chìa khoá (API key)**.

{% hint style="info" %}
Ví von cho dễ nhớ: **Base URL** = địa chỉ nhà của "bộ não" GLM. **API key** = chìa khoá để được cho vào. Thiếu 1 trong 2 thì không vào được.
{% endhint %}

---

## 2. Điều kiện cần — checklist

| # | Cần có | Là gì | Lấy ở đâu |
|---|--------|-------|-----------|
| 1 | **API key** | Chìa khoá cá nhân, dạng `--` / `vn-...` | [Trang API Keys](https://aiplatform.console.greennode.ai/keys) |
| 2 | **Base URL** | Địa chỉ MaaS: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | Cố định — chép nguyên văn từ đây |
| 3 | **Model GLM 5.2 đã bật (ENABLED)** | Bảo đảm GLM 5.2 đang mở để dùng | [Trang Models](https://aiplatform.console.greennode.ai/models) → gõ tìm **GLM 5.2** |

Model ID dùng khi cấu hình (ví dụ): **`z-ai/glm-5.2`**

{% hint style="info" %}
**GLM 5.2 ở đây chỉ là một model ví dụ.** GreenNode self-host **nhiều model** khác nhau — bạn thay bằng model mình muốn dùng. **Model ID** và **Base URL** chính xác của từng model đều nằm trong **trang chi tiết của model đó** trên [portal Models](https://aiplatform.console.greennode.ai/models).
{% endhint %}

---

## 3. Cách lấy từng điều kiện cần

### 3.1 — Lấy API key (chìa khoá)

1. Mở **[https://aiplatform.console.greennode.ai/keys](https://aiplatform.console.greennode.ai/keys)** và đăng nhập bằng tài khoản GreenNode.
2. Bấm **Create API Key** (Tạo API key).
3. Đặt tên gợi nhớ, ví dụ `ai-coding-<tên-bạn>` (chữ thường, số, gạch ngang; 5–50 ký tự).
4. Bấm tạo, rồi **Copy** key vừa hiện ra và dán tạm vào Notepad.

{% hint style="warning" %}
Key mới tạo có thể ở trạng thái **pending** (đang chờ). Đợi tới khi trạng thái là **ACTIVE** mới dùng được — bấm refresh trang để xem.
{% endhint %}

### 3.2 — Lấy Base URL (địa chỉ)

Base URL cũng hiển thị trong **trang chi tiết mỗi model**. Với các model qua MaaS, địa chỉ chung là:

```
https://maas-llm-aiplatform-hcm.api.vngcloud.vn
```

{% hint style="warning" %}
**Địa chỉ này khác nhau theo loại công cụ:**
* Công cụ chuẩn **Anthropic** (Claude Desktop, Claude Code): dùng `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` — **không** có `/v1`.
* Công cụ chuẩn **OpenAI** (OpenCode, Codex, Cursor…): thêm `/v1` ở cuối → `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1`.

Trang công cụ sẽ nói rõ bạn cần bản nào.
{% endhint %}

{% hint style="info" %}
**Nếu dùng key của gói Token Plan (subscription) thay vì API key trả theo mức dùng (pay-as-you-go)**, Base URL của Token Plan cũng theo đúng quy tắc Anthropic / OpenAI như trên, chỉ khác domain:
* Công cụ chuẩn **Anthropic** (Claude Desktop, Claude Code): `https://tokenplan.api.greennode.ai` — **không** có `/v1`.
* Công cụ chuẩn **OpenAI** (OpenCode, Codex, Cursor…): `https://tokenplan.api.greennode.ai/v1`.

Xem chi tiết tại [Token Plan](../token-plan/README.md).
{% endhint %}

### 3.3 — Kiểm tra model GLM 5.2 đã được bật

1. Mở **[trang Models](https://aiplatform.console.greennode.ai/models)** và gõ tìm model bạn muốn dùng (ví dụ **GLM 5.2**).
2. Mở model đó ra, xác nhận trạng thái là **ENABLED** (đang bật).
3. Ngay trong **trang chi tiết model**, copy sẵn **Model ID** và **Base URL** để điền vào công cụ (ví dụ GLM 5.2 → Model ID `z-ai/glm-5.2`).

{% hint style="info" %}
Nếu model chưa ENABLED, liên hệ đội quản trị AI Platform của GreenNode để được bật — bạn không tự làm bước này được.
{% endhint %}

✅ Có đủ 3 thứ (key **ACTIVE**, Base URL, model **ENABLED**) là bạn sẵn sàng chọn công cụ.

---

## 4. Chọn công cụ phù hợp

| Bạn thích... | Hệ điều hành | Nên dùng |
|--------------|--------------|----------|
| **Bấm chuột, chưa quen gõ lệnh** | macOS / Windows | Nhóm Có giao diện (GUI) → **Claude Desktop** *(đang cập nhật, sẽ có link sau)* |
| Gõ lệnh trong terminal | macOS / Linux / WSL / Windows | [Nhóm Dòng lệnh (CLI)](dong-lenh/README.md) → **Claude Code**, OpenCode, Codex CLI… |

{% hint style="info" %}
App **Claude Desktop chỉ có bản macOS và Windows.** Nếu bạn dùng **Linux hoặc WSL**, hãy đi theo nhóm **Dòng lệnh** (Claude Code) — cùng model GLM 5.2, chỉ khác cách cài.
{% endhint %}

---

## 5. Bảng giá trị tham chiếu nhanh

| Thông tin | Giá trị |
|-----------|---------|
| Base URL (chuẩn Anthropic) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` |
| Base URL (chuẩn OpenAI) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| Base URL (Token Plan, chuẩn Anthropic) | `https://tokenplan.api.greennode.ai` |
| Base URL (Token Plan, chuẩn OpenAI) | `https://tokenplan.api.greennode.ai/v1` |
| Model ID | Xem trong chi tiết model (ví dụ GLM 5.2 → `z-ai/glm-5.2`) |
| Tạo / lấy API key | https://aiplatform.console.greennode.ai/keys |
| Kiểm tra model GLM 5.2 | https://aiplatform.console.greennode.ai/models (gõ tìm GLM 5.2) |
| Xem usage & billing | https://aiplatform.console.greennode.ai/ |

---

## Cần hỗ trợ?

Nếu bạn làm theo mà vẫn chưa được, đừng ngại liên hệ bộ phận Hỗ trợ Khách hàng của GreenNode:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Trung tâm hỗ trợ: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Cảm ơn bạn đã sử dụng dịch vụ của GreenNode.
