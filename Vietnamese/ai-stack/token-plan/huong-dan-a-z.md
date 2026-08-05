# Hướng dẫn A-Z: Mua gói Token Plan và cấp cho cả nhóm

**Dành cho:** cá nhân tự mua tự dùng (B2C), và người nắm tài khoản Root/Admin của công ty cần cấp AI cho các phòng ban non-tech (B2B).

---

## 0. Hiểu nhanh trong 2 phút

Để một tool AI (Cursor, OpenCode, Codex, Claude Desktop…) chạy được bằng model của GreenNode, bạn chỉ cần **2 mẩu thông tin**:

| Thứ cần                                                        | Là gì                           | Ví von                         |
| ---------------------------------------------------------------- | --------------------------------- | ------------------------------- |
| **Base URL**                                               | Địa chỉ máy chủ AI           | Địa chỉ nhà của "bộ não" |
| **API key** (ở đây gọi là **subscription-key**) | Chìa khoá để được cho vào | Chìa khoá cửa                |

**Token Plan** là cách lấy 2 thứ đó theo kiểu **trả trước trọn gói 30 ngày**: bạn mua 1 gói, được cấp sẵn hạn mức token cố định, biết trước chi phí tháng — thay vì trả theo từng token dùng thực tế (PAYG).

```
Mua gói  →  Gói tự sinh subscription-key  →  Copy key + Base URL
        →  Dán vào tool  →  Chạy  →  Xem usage trên portal
```

{% hint style="info" %}
Muốn hiểu sâu Token Plan khác PAYG chỗ nào, kiến trúc ra sao → xem [Token Plan (tổng quan)](README.md).
{% endhint %}

---

## 1. Điều kiện cần — checklist trước khi bắt đầu

Tick đủ 3 dòng này rồi mới sang bước 2:

| # | Cần có                                                         | Cách kiểm tra                                                                                                       |
| - | ---------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 1 | **Tài khoản GreenNode** đăng nhập được AI Platform | Mở [aiplatform.console.greennode.ai](https://aiplatform.console.greennode.ai/)                                         |
| 2 | **Vai trò Root hoặc Admin**                              | Chỉ 2 role này được mua gói. Xem [Phân quyền theo Role](../agent-base/team-permissions/phan-quyen-theo-role.md) |
| 3 | **Đủ Credits** trong tài khoản cho giá gói           | Số dư hiển thị ngay ở màn thanh toán (**Balance**). 1 credit = 1 VND                                     |

{% hint style="warning" %}
Nếu bạn là **Developer/Viewer**, bạn **không** mua gói được — nhờ Root/Admin mua rồi cấp subscription-key cho bạn (xem [Mục 6](#6-quan-ly-cap-phat-cho-tung-thanh-vien)).
{% endhint %}

{% hint style="info" %}
Credit chưa đủ? Nạp thêm tại AI Platform Console trước khi mua — hệ thống trừ credit ngay khi bấm xác nhận, không cho mua nợ.
{% endhint %}

---

## 2. Chọn gói

**Đường đi trên portal:** `AI Platform` → sidebar → **Token Plan** → **Packages**

1. Danh sách các **Plan Type** hiện ra dạng card. Mỗi card cho biết ngay: giá, thời hạn, model đi kèm, số subscription-key tối đa.
   *Ví dụ card **Token Plan Alpha**: `1.080.000 VND / 30 ngày` — model GLM 5.2 — tối đa 5 keys.*
2. Bấm vào 1 card để mở **Package Detail** và đọc kỹ trước khi xuống tiền:

| Xem mục                              | Để biết                                                                                                                                 |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **Max keys**                    | Cấp được tối đa bao nhiêu người/tool                                                                                              |
| **Duration**                    | Chu kỳ gói (thường 30 ngày)                                                                                                           |
| **Tokens / Requests per cycle** | Hạn mức mỗi chu kỳ — tính **riêng cho từng model**, không bù trừ qua lại                                                  |
| **Included Models**             | Danh sách model được gọi (Model, Status, **Model code**, Provider) — nhớ **Model code**, lát nữa cần điền vào tool |
| **Subscription Endpoint** | `https://tokenplan.api.greennode.ai` — chính là **Base URL** bạn sẽ dùng. Tool chuẩn OpenAI thêm `/v1` ở cuối, tool chuẩn Anthropic thì **không** — xem [Mục 5](#5-setup-vao-tool-dang-chay-agent) |
| **What happens when activated** | Điều gì xảy ra ngay sau khi kích hoạt                                                                                                |

{% hint style="warning" %}
Gói đã mua **không đổi được sang Plan Type khác** và **không trả lại tuỳ ý**. Nếu buộc phải dừng giữa chu kỳ, dùng **Delete** — phần hạn mức chưa dùng được hoàn pro rata vào Credits. Cân nhắc kỹ ở bước này.
{% endhint %}

**Chọn gói cỡ nào?** Nguyên tắc đơn giản cho nhóm non-tech: một người dùng coding assistant đều đặn cả ngày tiêu thụ khá nhiều token — nếu chưa có số liệu, mua gói nhỏ nhất 1 chu kỳ để đo, rồi xem thực tế ở [Mục 7](#7-theo-doi-usage-theo-tung-goi) trước khi mua gói lớn.

📎 *Chi tiết đầy đủ về màn Packages: [Mua gói Token Plan](mua-goi-token-plan.md)*

---

## 3. Mua gói

1. Bấm **Buy Now** trên card (hoặc **Buy package** trong Package Detail).
2. Màn **Confirm & checkout** hiện ra — điền và kiểm tra:

| Trường                                      | Ví dụ                                                        | Lưu ý                                                                                                                       |
| --------------------------------------------- | -------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **Plan name** (bắt buộc)              | `ENG-GLM-1`                                                  | Chỉ `a-z A-Z 0-9 _ - .`, tối đa 50 ký tự. **Đặt tên theo phòng ban/dự án** để sau này lọc usage cho dễ |
| **Plan price / Duration / VAT / Total** | `1.080.000 VND` / `30 days` / Included / `1.080.000 VND` | Tự tính theo Plan Type                                                                                                      |
| **Auto-renew**                          | ON (mặc định)                                               | Tự gia hạn cuối mỗi chu kỳ — tắt được sau khi mua                                                                   |
| **Payment method**                      | Credits                                                        | 1 credit = 1 VND                                                                                                              |
| **Balance**                             | Số dư hiện tại                                             | Đối chiếu xem có đủ không                                                                                              |

3. Bấm **Confirm & Pay**.

{% hint style="warning" %}
Bấm xác nhận là **trừ ngay** số tiền ở dòng Total. Provisioning chạy nền — gateway endpoint và subscription-key chỉ hiện đầy đủ trên Plan Detail **sau khi provisioning xong**. Đợi vài giây rồi refresh nếu chưa thấy.
{% endhint %}

**Kết quả:** gói xuất hiện trong **My Token Plans**, trạng thái `ACTIVE`, Auto-renew ON, và hệ thống **tự tạo sẵn 1 key tên `default-key`** dùng được ngay — không cần tạo key thủ công để bắt đầu.

📎 *Chi tiết: [Mua gói Token Plan](mua-goi-token-plan.md)*

---

## 4. Lấy API key + Base URL

**Đường đi:** `API Key` → `Token Plan` → **My Token Plans** → bấm vào **tên gói** vừa mua

Trang **Plan Detail** có 2 tab — bạn cần lấy thông tin ở cả hai:

**Tab `Models`** → lấy 2 thứ:

- **Gateway base URL** dùng chung cho cả gói — chọn dạng theo chuẩn của tool:
  - Tool chuẩn **OpenAI** (Cursor, OpenCode, Codex…): `https://tokenplan.api.greennode.ai/v1`
  - Tool chuẩn **Anthropic** (Claude Code, Claude Desktop): `https://tokenplan.api.greennode.ai` — **không** có `/v1`
- **Model code** của model muốn dùng (ví dụ `glm-5.2`) — copy chính xác, sai một ký tự là lỗi

**Tab `Subscription keys`** → lấy chìa khoá:

- Copy `default-key` (hoặc key bạn tự tạo ở [Mục 6](#6-quan-ly-cap-phat-cho-tung-thanh-vien))

Chép 3 giá trị này ra Notepad:

| Thông tin         | Giá trị                                      |
| ------------------ | ---------------------------------------------- |
| **Base URL** | `https://tokenplan.api.greennode.ai/v1` (chuẩn OpenAI) hoặc `https://tokenplan.api.greennode.ai` (chuẩn Anthropic, **không** `/v1`) |
| **API key**  | subscription-key vừa copy                     |
| **Model**    | model code từ tab Models (ví dụ `glm-5.2`) |

{% hint style="warning" %}
Subscription-key là **bí mật** — ai cầm được key là gọi được model và tiêu hạn mức của gói. Không dán vào chat nhóm, không commit lên Git. Cấp riêng cho từng người (xem [Mục 6](#6-quan-ly-cap-phat-cho-tung-thanh-vien)) để lỡ lộ thì thu hồi đúng một key.
{% endhint %}

---

## 5. Setup vào tool đang chạy agent

Token Plan dùng chung một host cho mọi tool — hai chuẩn chỉ khác nhau ở hậu tố `/v1` và ở tên biến môi trường:

| Chuẩn của tool | Base URL điền vào |
|---|---|
| **OpenAI** (Cursor, Continue.dev, OpenCode, Codex, LiteLLM, OpenAI SDK…) | `https://tokenplan.api.greennode.ai/v1` — **có** `/v1` |
| **Anthropic** (Claude Code, Claude Desktop, Anthropic SDK) | `https://tokenplan.api.greennode.ai` — **không** có `/v1` |

Ngoài Base URL thì không đổi gì khác — vẫn đúng 3 giá trị ở Mục 4.

### 5.1 Tool chuẩn OpenAI có ô cấu hình sẵn (Cursor, Continue.dev, và tương tự)

Vào phần Settings của tool, điền:

| Trường           | Giá trị                                 |
| ------------------ | ----------------------------------------- |
| **Base URL** | `https://tokenplan.api.greennode.ai/v1` |
| **API Key**  | `<subscription-key của bạn>`          |
| **Model**    | `<model code>` — ví dụ `glm-5.2`   |

### 5.2 Tool chuẩn OpenAI đọc biến môi trường (CLI)

{% tabs %}
{% tab title="macOS / Linux / WSL" %}

```bash
export OPENAI_BASE_URL="https://tokenplan.api.greennode.ai/v1"
export OPENAI_API_KEY="<subscription-key của bạn>"
```

Thêm 2 dòng trên vào cuối `~/.zshrc` (macOS) hoặc `~/.bashrc` (Linux/WSL) để không phải gõ lại mỗi lần, rồi chạy `source ~/.zshrc`.
{% endtab %}

{% tab title="Windows PowerShell" %}

```powershell
$env:OPENAI_BASE_URL = "https://tokenplan.api.greennode.ai/v1"
$env:OPENAI_API_KEY  = "<subscription-key của bạn>"
```

Lưu vĩnh viễn cho tài khoản (chạy 1 lần rồi **mở lại PowerShell**):

```powershell
[Environment]::SetEnvironmentVariable("OPENAI_BASE_URL", "https://tokenplan.api.greennode.ai/v1", "User")
[Environment]::SetEnvironmentVariable("OPENAI_API_KEY", "<subscription-key của bạn>", "User")
```

{% endtab %}
{% endtabs %}

### 5.3 Gọi bằng code (OpenAI SDK)

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://tokenplan.api.greennode.ai/v1",
    api_key="<subscription-key của bạn>",
)

response = client.chat.completions.create(
    model="glm-5.2",
    messages=[{"role": "user", "content": "Hello"}],
)
print(response.choices[0].message.content)
```

### 5.4 Kiểm tra kết nối (test 30 giây)

Dán nguyên đoạn này vào terminal, thay 2 giá trị trong `<>`:

```bash
curl https://tokenplan.api.greennode.ai/v1/chat/completions \
  -H "Authorization: Bearer <subscription-key của bạn>" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "<model code>",
    "messages": [{"role": "user", "content": "ping"}]
  }'
```

✅ **Đúng khi:** response JSON có trường `choices[0].message.content`.

### 5.5 Bảng lỗi thường gặp

| Triệu chứng                   | Nguyên nhân                                       | Cách xử lý                                                                  |
| ------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------ |
| `401 Unauthorized`            | Key sai, key bị Disable, hoặc copy thiếu ký tự | Copy lại key ở tab **Subscription keys**, kiểm tra Status = `ACTIVE` |
| `403 Forbidden`               | Gọi model **không nằm trong gói**          | Chỉ gọi model có trong tab **Models** của gói đó                   |
| `402 Payment Required`        | Gói đã hết hạn hoặc đã bị xoá             | Mua lại (**Buy again**) hoặc bật lại Auto-renew                      |
| `404 Not Found` | Base URL sai dạng so với chuẩn của tool | Tool chuẩn OpenAI: Base URL phải kết thúc bằng `/v1`. Tool chuẩn Anthropic (Claude Code): Base URL **không** được có `/v1` |
| Request hết token giữa chừng | Pool token của model đó đã về 0               | Đợi chu kỳ mới, mua thêm 1 gói, hoặc tạm chuyển sang API Key PAYG     |
| Response lỗi parse             | Tool tự nối `/v1` vào base URL                  | Thử bỏ `/v1` nếu tool tự xử lý                                          |

### 5.6 Tool chuẩn Anthropic (Claude Code, Claude Desktop)

Nhóm này nói giao thức Anthropic chứ không phải OpenAI, nên Base URL là **cùng host nhưng không có `/v1`**, và tên biến môi trường cũng khác:

{% tabs %}
{% tab title="macOS / Linux / WSL" %}

```bash
export ANTHROPIC_BASE_URL="https://tokenplan.api.greennode.ai"
export ANTHROPIC_AUTH_TOKEN="<subscription-key của bạn>"
```

{% endtab %}

{% tab title="Windows PowerShell" %}

```powershell
$env:ANTHROPIC_BASE_URL   = "https://tokenplan.api.greennode.ai"
$env:ANTHROPIC_AUTH_TOKEN = "<subscription-key của bạn>"
```

{% endtab %}
{% endtabs %}

Hướng dẫn đầy đủ: [Kết nối Claude Code với GreenNode MaaS](../ai-coding/dong-lenh/claude-code.md).

📎 *Cấu hình chi tiết cho từng tool cụ thể (LiteLLM, Cursor, Continue.dev, Node.js SDK…): [Kết nối OpenAI-compatible với GreenNode MaaS](../ai-coding/ket-noi-openai-compatible-voi-maas.md) — các bước giữ nguyên, chỉ đổi Base URL và key sang giá trị Token Plan ở Mục 4.*

📎 *Danh sách tool đang hỗ trợ và cách chọn tool phù hợp: [AI Coding](../ai-coding/README.md) · [Bắt đầu với AI Coding](../ai-coding/bat-dau.md) · [Nhóm Dòng lệnh (CLI)](../ai-coding/dong-lenh/README.md)*

---

## 6. Quản lý: cấp phát cho từng thành viên

Phần này dành cho người nắm **Root/Admin** cần chia gói cho cả nhóm.

### 6.1 Xem các gói đã mua & chi tiết từng gói

**Đường đi:** `API Key` → `Token Plan` → **My Token Plans**

Danh sách hiển thị: tên plan, Plan Type, ngày hết hạn (**Expires**), trạng thái **Auto-renew**.

| Trạng thái | Ý nghĩa                                                                  |
| ------------ | -------------------------------------------------------------------------- |
| `ACTIVE`   | Gói đang chạy                                                           |
| `EXPIRED`  | Gói hết hạn, không gia hạn — mọi key trong gói ngừng hoạt động |

Bấm vào tên gói để mở **Plan Detail**:

- **General information:** Package, Price, Purchase date, Expiry date, Cycle, số key đang dùng (ví dụ `1/5 in use`), Auto-renew, hạn mức Tokens/cycle và Requests/cycle
- **Tab `Models`:** Gateway base URL + bảng model (Model, Model code, Enabled types, Endpoint) — thông tin để gọi API
- **Tab `Subscription keys`:** danh sách key trong gói (Name, Status, Key, Created at)
- **Action góc trên phải:** **Buy again** (mua thêm 1 gói cùng loại) và **Delete** (huỷ gói)

{% hint style="info" %}
Mua nhiều gói song song = nhiều plan instance **độc lập**, quota **không gộp** — kể cả khi trùng Plan Type. Muốn tách ngân sách theo phòng ban thì mua mỗi phòng 1 gói riêng, đặt Plan name theo tên phòng.
{% endhint %}

### 6.2 Cấp subscription-key cho từng thành viên

**Nguyên tắc: mỗi người / mỗi tool một key riêng.** Cùng chung hạn mức gói, nhưng tách key thì thu hồi được từng người và lọc usage được từng người.

**Bước 1 — Lên kế hoạch trước khi tạo.** Gói có giới hạn **Max keys** (ví dụ 5), nên liệt kê trước ai cần gì:

| Key name           | Cấp cho               | Dùng vào việc gì                |
| ------------------ | ---------------------- | ----------------------------------- |
| `default-key`    | (hệ thống tạo sẵn) | Giữ để test, không phát cho ai |
| `mkt-an`         | An — Marketing        | Cursor trên máy cá nhân         |
| `sale-binh`      | Bình — Sales         | Codex Desktop                       |
| `ops-agent-prod` | (không phải người) | Agent tự động chạy nền         |

Đặt tên theo mẫu `{phòngban}-{tên}` hoặc `{hệthống}-{môitrường}` — nhìn tên là biết thu hồi cái nào.

**Bước 2 — Tạo key.**

1. Vào **Plan Detail** → tab **Subscription keys** → bấm **+ Add key**
2. Điền **Key name** theo bảng kế hoạch
3. Popup cho biết key sẽ kế thừa từ gói: gọi được **toàn bộ model trong gói**, **dùng chung** hạn mức token/request, **cùng 1 gateway endpoint**
4. Bấm **Create key**

Key mới xuất hiện với trạng thái `ACTIVE`, đồng thời tự động hiện trên trang [Access Control](../agent-base/access-control/README.md) với nhãn `Key Type = Plan: {tên gói}` — cùng một bản ghi, không bị trùng.

**Bước 3 — Giao key cho thành viên.** Gửi cho mỗi người đúng 3 giá trị:

```
Base URL : https://tokenplan.api.greennode.ai/v1   # tool chuẩn OpenAI (Cursor, OpenCode, Codex…)
           https://tokenplan.api.greennode.ai      # tool chuẩn Anthropic (Claude Code, Claude Desktop)
API key  : <key riêng của người đó>
Model    : <model code>
```

Kèm link [Mục 5](#5-setup-vao-tool-dang-chay-agent) để họ tự setup.

{% hint style="warning" %}
Gửi key qua kênh riêng tư (1-1, password manager), **không** đăng lên channel chung.
{% endhint %}

**Bước 4 — Thu hồi / sửa key.** Trong tab **Subscription keys**, bấm icon **⋮** ở dòng key → chọn **Enable** / **Disable** / **Rename** / **Delete**.

| Tình huống                             | Làm gì                                                                         |
| ---------------------------------------- | -------------------------------------------------------------------------------- |
| Thành viên nghỉ việc / đổi dự án | **Disable** (tạm) hoặc **Delete** (hẳn)                           |
| Nghi key bị lộ                         | **Delete** key cũ → **+ Add key** tạo key mới, gửi lại         |
| Đặt sai tên                           | **Rename**                                                                 |
| Hết Max keys, cần cấp thêm người   | **Delete** key không còn dùng, hoặc **Buy again** mua thêm gói |

{% hint style="warning" %}
**Disable** hoặc **Delete** có hiệu lực **ngay lập tức** — tool của người đó dừng gọi được model từ request kế tiếp.
{% endhint %}

### 6.3 Bật/tắt Auto-renew

Bấm toggle **Auto-renew** trong danh sách hoặc trong Plan Detail. Popup **Turn off auto-renew?** nêu rõ:

- Gói **không** tự gia hạn nữa, nhưng vẫn `ACTIVE` **đến đúng ngày hết hạn**
- Đến ngày hết hạn, **toàn bộ** subscription-key trong gói ngừng hoạt động ngay
- Không trừ credit lúc này, và **không hoàn tiền** cho việc tắt Auto-renew
- Bật lại, hoặc **Buy again**, bất cứ lúc nào trước khi gói hết hạn

{% hint style="info" %}
Auto-renew ON: hệ thống gia hạn trước hạn. Nếu credit không đủ, hệ thống retry — vẫn thất bại thì gói chuyển `EXPIRED` và cả nhóm mất quyền gọi model. **Nhớ giữ đủ credit trước ngày hết hạn.**
{% endhint %}

### 6.4 Xoá/huỷ gói

Trong **Plan Detail** bấm **Delete**, hoặc trong **My Token Plans** tick checkbox rồi bấm icon thùng rác (bulk). Popup nêu rõ: toàn bộ key bị vô hiệu **ngay lập tức**, hạn mức chưa dùng được hoàn **pro rata** vào Credits, gói biến mất khỏi danh sách nhưng lịch sử usage vẫn giữ để đối soát.

{% hint style="warning" %}
Xoá gói **không thể hoàn tác**. Báo trước cho cả nhóm trước khi bấm.
{% endhint %}

📎 *Chi tiết đầy đủ mục 6: [Quản lý Token Plan](quan-ly-token-plan.md)*

---

## 7. Theo dõi usage theo từng gói

**Đường đi:** `AI Platform Console` → sidebar → **Usage & Budget** → **Usage & Cost** → **Tab Usage**

{% hint style="info" %}
**Với Token Plan, bạn chỉ xem Tab Usage — không xem Tab Cost.** Gói là **trả trước trọn gói**: chi phí đã cố định ngay lúc mua, không phát sinh thêm theo từng request. Vì vậy subscription-key **không** có cost breakdown theo token như API Key PAYG. Cái cần theo dõi là **đã tiêu bao nhiêu token trên hạn mức đã trả**, không phải tiêu bao nhiêu tiền.
{% endhint %}

### 7.1 Cách lọc đúng gói muốn xem

1. Mở dropdown **All API Keys** trên filter bar (single select)
2. Chọn **subscription-key của gói** cần xem
3. Đặt **Time Range** trùng chu kỳ gói — dùng tab **Absolute** trong picker panel, điền From = ngày mua, To = hôm nay

Toàn bộ số liệu Tab Usage lập tức chỉ còn của key đó.

{% hint style="info" %}
Filter **All API Keys** là **single select** — mỗi lần chỉ xem được 1 key. Muốn ra tổng của cả gói có nhiều key, cộng thủ công từng key, hoặc đối chiếu trực tiếp với hạn mức còn lại hiển thị sẵn trong **Plan Detail**.
{% endhint %}

### 7.2 Đọc số liệu Tab Usage

| Chỉ số                     | Ý nghĩa với gói Token Plan                                                                                                         |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **Tokens Consumed**    | Số quan trọng nhất — tổng Input + Output + Cache. So với **Tokens/cycle** trong Plan Detail để biết còn lại bao nhiêu |
| **Total Requests**     | So với **Requests/cycle** trong Plan Detail                                                                                      |
| **Errors**             | Số request lỗi — tăng đột biến thường là key sai, gọi model ngoài gói, hoặc gói đã hết hạn mức                     |
| **Requests over time** | Line chart theo giờ/ngày — xem nhịp sử dụng đều hay dồn cục                                                                  |
| **Token Breakdown**    | Doughnut tách Cache / Output / Input                                                                                                  |

{% hint style="info" %}
Nguồn chính xác nhất về hạn mức còn lại vẫn là **Plan Detail** của gói (Tokens/cycle, Requests/cycle). Tab Usage dùng để **bóc tách theo từng key** — biết ai đang tiêu phần nào trong pool chung.
{% endhint %}

### 7.3 Dùng số liệu để làm gì

| Câu hỏi                                   | Cách trả lời                                                                                  |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Ai đang xài nhiều nhất?                 | Lọc lần lượt từng key thành viên, so **Tokens Consumed**                             |
| Gói sắp cạn chưa?                       | So Tokens Consumed với **Tokens/cycle** trong Plan Detail                                  |
| Chu kỳ sau nên mua gói to hay nhỏ hơn? | Xem tổng tiêu thụ trọn 1 chu kỳ (Time Range = Absolute từ ngày mua đến ngày hết hạn) |
| Có ai gọi lỗi liên tục không?         | Xem card **Errors** khi lọc theo key đó                                                  |

📎 *Chi tiết dashboard, các filter khác và phân quyền xem theo role: [Xem Usage & Cost](../usage-budget/xem-usage-cost.md)*

---

## 8. Câu hỏi thường gặp

**Nhiều người dùng chung 1 gói thì quota chia thế nào?**
Không chia. Mọi key trong cùng 1 gói **dùng chung một pool** token/request của từng model — ai gọi trước tiêu trước. Muốn tách quota cứng theo phòng ban thì mua **gói riêng** cho từng phòng.

**Hết token giữa chu kỳ thì sao?**
Request gọi model đó bị tạm ngưng cho tới chu kỳ mới. Muốn dùng tiếp ngay: mua thêm 1 gói, hoặc tạm chuyển sang [API Key PAYG](../ai-coding/bat-dau.md).

**Subscription-key có xuất hiện chung với API Key PAYG không?**
Không. Hai loại tách biệt hoàn toàn, không dùng chung dropdown ở bất kỳ đâu trong AgentBase. Subscription-key cũng bị loại khỏi trang [Rate Limit](../agent-base/protect-govern/rate-limit.md).

**Gọi model ngoài gói được không?**
Không — gateway chặn với lỗi `403 Forbidden`. Chỉ model trong tab **Models** của gói mới gọi được.

**Đổi gói sang Plan Type khác giữa chừng?**
Không đổi được. Phải **Delete** gói cũ (hoàn pro rata phần chưa dùng) rồi mua gói mới.

---

## Đi tiếp

| Tôi muốn...                                    | Đi đến                                                                                            |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| Hiểu Token Plan vs PAYG, kiến trúc hệ thống | [Token Plan (tổng quan)](README.md)                                                                  |
| Chi tiết màn Packages & thanh toán            | [Mua gói Token Plan](mua-goi-token-plan.md)                                                          |
| Chi tiết quản lý gói & subscription-key      | [Quản lý Token Plan](quan-ly-token-plan.md)                                                         |
| Cấu hình chi tiết từng tool AI coding        | [Kết nối OpenAI-compatible với GreenNode MaaS](../ai-coding/ket-noi-openai-compatible-voi-maas.md) |
| Chọn tool phù hợp (GUI hay CLI)               | [Bắt đầu với AI Coding](../ai-coding/bat-dau.md)                                                  |
| Dashboard usage (Tab Usage)                      | [Xem Usage & Cost](../usage-budget/xem-usage-cost.md)                                             |
| Phân quyền thành viên trong tổ chức        | [Phân quyền theo Role](../agent-base/team-permissions/phan-quyen-theo-role.md)                      |

---

## Cần hỗ trợ?

* Email: [support@greennode.ai](mailto:support@greennode.ai)
* Hotline: 19001549
* Trung tâm hỗ trợ: [helpdesk.greennode.ai](https://helpdesk.greennode.ai)

Cảm ơn bạn đã sử dụng dịch vụ của GreenNode.
