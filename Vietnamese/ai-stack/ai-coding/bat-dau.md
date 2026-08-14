# Bắt đầu với AI Coding (điều kiện cần)

> **Trang gốc.** Đọc trang này một lần để chuẩn bị đủ mọi thứ, sau đó chọn công cụ ở cuối trang. Mọi hướng dẫn công cụ đều giả định bạn đã làm xong các bước ở đây.

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

## 2. Xác định loại dịch vụ bạn đang dùng

GreenNode có **hai loại dịch vụ** để gọi model, mỗi loại dùng **host riêng** và **loại key riêng**. Đây là bước dễ sai nhất khi copy ví dụ — làm xong bước này rồi hãy đọc tiếp.

| Loại dịch vụ | Key dùng để gọi | Lấy key ở đâu | Host của Base URL |
|---|---|---|---|
| **PAYG** — trả theo token thực dùng | API Key | AI Platform → **API Keys** | `maas-llm-aiplatform-hcm.api.vngcloud.vn` |
| **Token Plan** — gói prepaid 30 ngày, hạn mức cố định | subscription-key | AI Platform → **Token Plan** → **My Token Plans** → mở gói → tab **Subscription keys** | `tokenplan.api.greennode.ai` |

### 2.1 — Bảng tra Base URL

Base URL = **host theo loại dịch vụ** (bảng trên) + **hậu tố `/v1` hay không, theo chuẩn của tool**:

| Loại dịch vụ | Tool chuẩn **Anthropic**<br>(Claude Code, Claude Desktop) | Tool chuẩn **OpenAI**<br>(Codex, OpenCode, Cursor, LiteLLM, OpenAI SDK) |
|---|---|---|
| **PAYG** | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| **Token Plan** | `https://tokenplan.api.greennode.ai` | `https://tokenplan.api.greennode.ai/v1` |

{% hint style="warning" %}
**Key và Base URL phải cùng một loại dịch vụ.** Dùng API Key PAYG với host `tokenplan…`, hoặc subscription-key với host `maas-llm-aiplatform-hcm…`, đều trả về `401 Unauthorized` — dù cả key và URL đều hợp lệ khi đứng riêng.

Bạn **không nhận biết được loại key bằng mắt** — hãy nhớ theo **nơi bạn đã lấy key**: trang **API Keys** là PAYG, tab **Subscription keys** trong một gói là Token Plan.
{% endhint %}

### 2.2 — Tự kiểm tra trước khi copy bất kỳ ví dụ nào

Ba câu hỏi này quyết định bạn copy tab nào trong các trang hướng dẫn công cụ:

| # | Câu hỏi | Cách trả lời |
|---|---|---|
| 1 | Key của tôi thuộc loại nào? | Lấy ở trang **API Keys** → **PAYG**. Lấy ở tab **Subscription keys** của một gói → **Token Plan** |
| 2 | Tool của tôi theo chuẩn nào? | Claude Code / Claude Desktop → **Anthropic**, Base URL **không** `/v1`. Các tool còn lại → **OpenAI**, Base URL **có** `/v1` |
| 3 | Model ID lấy từ đâu? | **PAYG:** trang chi tiết model trên [portal Models](https://aiplatform.console.greennode.ai/models) (ví dụ `z-ai/glm-5.2`). **Token Plan:** cột **Model code** ở tab **Models** của gói (ví dụ `glm-5.2`) |

{% hint style="info" %}
Model ID của hai loại dịch vụ **có thể khác nhau** cho cùng một model. Luôn copy đúng nguồn ở câu 3 — sai một ký tự là lỗi `404` hoặc model không load.
{% endhint %}

---

## 3. Điều kiện cần — checklist

| # | Cần có | Là gì | Lấy ở đâu |
|---|--------|-------|-----------|
| 1 | **API key** | Chìa khoá cá nhân | **PAYG:** [Trang API Keys](https://aiplatform.console.greennode.ai/keys) · **Token Plan:** tab **Subscription keys** của gói |
| 2 | **Base URL** | Địa chỉ endpoint theo loại dịch vụ | Bảng tra ở **Mục 2.1** phía trên |
| 3 | **Model đã bật (ENABLED)** | Bảo đảm model đang mở để dùng | **PAYG:** [Trang Models](https://aiplatform.console.greennode.ai/models) · **Token Plan:** tab **Models** của gói |

Model ID dùng khi cấu hình (ví dụ PAYG): **`z-ai/glm-5.2`**

{% hint style="info" %}
**GLM 5.2 ở đây chỉ là một model ví dụ.** GreenNode self-host **nhiều model** khác nhau — bạn thay bằng model mình muốn dùng. Với PAYG, **Model ID** và **Base URL** chính xác của từng model nằm trong **trang chi tiết của model đó** trên [portal Models](https://aiplatform.console.greennode.ai/models). Với Token Plan, xem tab **Models** của gói bạn đã mua.
{% endhint %}

---

## 4. Cách lấy từng điều kiện cần

### 4.1 — Lấy API key (chìa khoá)

{% tabs %}
{% tab title="PAYG — API Key" %}
1. Mở **[https://aiplatform.console.greennode.ai/keys](https://aiplatform.console.greennode.ai/keys)** và đăng nhập bằng tài khoản GreenNode.
2. Bấm **Create API Key** (Tạo API key).
3. Đặt tên gợi nhớ, ví dụ `ai-coding-<tên-bạn>` (chữ thường, số, gạch ngang; 5–50 ký tự).
4. Bấm tạo, rồi **Copy** key vừa hiện ra và dán tạm vào Notepad.

{% hint style="warning" %}
Key mới tạo có thể ở trạng thái **pending** (đang chờ). Đợi tới khi trạng thái là **ACTIVE** mới dùng được — bấm refresh trang để xem.
{% endhint %}
{% endtab %}

{% tab title="Token Plan — subscription-key" %}
1. Vào **API Key** → **Token Plan** → **My Token Plans**, bấm vào **tên gói** bạn đã mua.
2. Mở tab **Subscription keys**.
3. Copy `default-key` (key hệ thống tự tạo khi mua gói), hoặc key bạn tự tạo thêm.
4. Sang tab **Models** để copy luôn **Model code** của model muốn dùng.

Chưa có gói? Xem [Mua gói Token Plan](../token-plan/mua-goi-token-plan.md), hoặc đi hết một vòng theo [Hướng dẫn A-Z](../token-plan/huong-dan-a-z.md).

{% hint style="warning" %}
Subscription-key là **bí mật** — ai cầm được key là gọi được model và tiêu hạn mức của gói. Không dán vào chat nhóm, không commit lên Git.
{% endhint %}
{% endtab %}
{% endtabs %}

### 4.2 — Lấy Base URL (địa chỉ)

Chọn đúng ô trong bảng tra ở **Mục 2.1** phía trên theo **loại dịch vụ** của key và **chuẩn** của tool:

{% tabs %}
{% tab title="PAYG" %}
```
# Tool chuẩn Anthropic (Claude Code, Claude Desktop) — KHÔNG có /v1
https://maas-llm-aiplatform-hcm.api.vngcloud.vn

# Tool chuẩn OpenAI (Codex, OpenCode, Cursor, LiteLLM…) — CÓ /v1
https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1
```

Base URL này cũng hiển thị trong **trang chi tiết mỗi model** trên portal Models.
{% endtab %}

{% tab title="Token Plan" %}
```
# Tool chuẩn Anthropic (Claude Code, Claude Desktop) — KHÔNG có /v1
https://tokenplan.api.greennode.ai

# Tool chuẩn OpenAI (Codex, OpenCode, Cursor, LiteLLM…) — CÓ /v1
https://tokenplan.api.greennode.ai/v1
```

Base URL này hiển thị ở tab **Models** của gói, dưới nhãn **Gateway base URL**. Xem thêm [Token Plan](../token-plan/README.md).
{% endtab %}
{% endtabs %}

### 4.3 — Kiểm tra model đã được bật

{% tabs %}
{% tab title="PAYG" %}
1. Mở **[trang Models](https://aiplatform.console.greennode.ai/models)** và gõ tìm model bạn muốn dùng (ví dụ **GLM 5.2**).
2. Mở model đó ra, xác nhận trạng thái là **ENABLED** (đang bật).
3. Ngay trong **trang chi tiết model**, copy sẵn **Model ID** và **Base URL** để điền vào công cụ (ví dụ GLM 5.2 → Model ID `z-ai/glm-5.2`).

{% hint style="info" %}
Nếu model chưa ENABLED, liên hệ đội quản trị AI Platform của GreenNode để được bật — bạn không tự làm bước này được.
{% endhint %}
{% endtab %}

{% tab title="Token Plan" %}
1. Mở **Plan Detail** của gói → tab **Models**.
2. Bảng model liệt kê đúng những model **nằm trong gói** — chỉ gọi được các model này.
3. Copy **Model code** của model muốn dùng (ví dụ `glm-5.2`).

{% hint style="warning" %}
Gọi model **không nằm trong gói** trả về `403 Forbidden`. Muốn dùng model khác, mua gói có model đó hoặc tạm chuyển sang API Key PAYG.
{% endhint %}
{% endtab %}
{% endtabs %}

### 4.4 — Kiểm tra cặp Base URL + key trước khi cấu hình tool

Chạy thử ngay trong terminal. Nếu bước này chạy được, mọi tool phía sau chỉ là điền lại đúng 2 giá trị vừa dùng:

{% tabs %}
{% tab title="PAYG" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/models \
  -H "Authorization: Bearer <API-key-PAYG-của-bạn>"
```
{% endtab %}

{% tab title="Token Plan" %}
```bash
curl https://tokenplan.api.greennode.ai/v1/chat/completions \
  -H "Authorization: Bearer <subscription-key-của-bạn>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "<model-code-từ-tab-Models>",
    "messages": [{"role": "user", "content": "ping"}]
  }'
```
{% endtab %}
{% endtabs %}

Đọc kết quả:

| Kết quả | Nghĩa là | Làm gì |
|---|---|---|
| Response JSON hợp lệ | Cặp URL + key đúng | Sang Mục 5 chọn công cụ |
| `401 Unauthorized` | Key sai, chưa **ACTIVE**, hoặc **key và host lệch loại dịch vụ** | Đối chiếu lại Mục 2 — key lấy ở đâu thì dùng host của loại đó |
| `403 Forbidden` | Model không nằm trong gói Token Plan | Chỉ gọi model có trong tab **Models** của gói |
| `404 Not Found` | Base URL sai dạng | Kiểm tra `/v1` theo chuẩn tool ở Mục 2.1 |

✅ Có đủ 3 thứ (key **ACTIVE**, Base URL đúng loại dịch vụ, model **ENABLED**) và bước kiểm tra trên chạy được là bạn sẵn sàng chọn công cụ.

---

## 5. Chọn công cụ phù hợp

| Bạn thích... | Hệ điều hành | Nên dùng |
|--------------|--------------|----------|
| **Bấm chuột, chưa quen gõ lệnh** | macOS / Windows | Nhóm Có giao diện (GUI) → **Claude Desktop** *(đang cập nhật, sẽ có link sau)* |
| Gõ lệnh trong terminal | macOS / Linux / WSL / Windows | [Nhóm Dòng lệnh (CLI)](dong-lenh/README.md) → **Claude Code**, OpenCode, Codex CLI… |

{% hint style="info" %}
App **Claude Desktop chỉ có bản macOS và Windows.** Nếu bạn dùng **Linux hoặc WSL**, hãy đi theo nhóm **Dòng lệnh** (Claude Code) — cùng model GLM 5.2, chỉ khác cách cài.
{% endhint %}

---

## 6. Bảng giá trị tham chiếu nhanh

| Thông tin | PAYG | Token Plan |
|---|---|---|
| Base URL (chuẩn Anthropic) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | `https://tokenplan.api.greennode.ai` |
| Base URL (chuẩn OpenAI) | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | `https://tokenplan.api.greennode.ai/v1` |
| Loại key | API Key | subscription-key |
| Lấy key | [Trang API Keys](https://aiplatform.console.greennode.ai/keys) | Plan Detail → tab **Subscription keys** |
| Model ID | Trang chi tiết model (ví dụ `z-ai/glm-5.2`) | Tab **Models** → cột **Model code** (ví dụ `glm-5.2`) |
| Danh sách model khả dụng | [Trang Models](https://aiplatform.console.greennode.ai/models) | Tab **Models** của gói |
| Xem usage | [AI Platform Console](https://aiplatform.console.greennode.ai/) → tab **Usage** & **Cost** | [AI Platform Console](https://aiplatform.console.greennode.ai/) → chỉ tab **Usage** |

---

## Cần hỗ trợ?

Nếu bạn làm theo mà vẫn chưa được, đừng ngại liên hệ bộ phận Hỗ trợ Khách hàng của GreenNode:

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Trung tâm hỗ trợ: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Cảm ơn bạn đã sử dụng dịch vụ của GreenNode.
