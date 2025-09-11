# Làm việc với Authentication Token

## Tạo mới Authentication Token

Để tạo một token mới phục vụ cho việc xác thực AI Gateway:

1. Truy cập tab **Authentication token** trong giao diện quản lý AI Gateway.
2. Nhấn nút **Create authentication token** để mở popup tạo token.
3. Trong cửa sổ popup:
   * Nhập **Token name** (bắt buộc). Đây là tên định danh để bạn dễ dàng quản lý token.
   * Ví dụ: `token-user01, token-user02,...`
4. Nhấn **Create** để khởi tạo token.

Mỗi token sẽ gắn liền với AI Gateway cụ thể và có thể được sử dụng để gọi API hoặc truy cập Gateway một cách an toàn.

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

## Quản lý danh sách token

Sau khi tạo, token sẽ xuất hiện trong danh sách với các thông tin:

<table><thead><tr><th width="148.09088134765625">Trường</th><th>Mô tả</th></tr></thead><tbody><tr><td><strong>Token name</strong></td><td>Tên định danh bạn đã đặt khi tạo token</td></tr><tr><td><strong>Created at</strong></td><td>Thời gian tạo</td></tr><tr><td><strong>Status</strong></td><td>Trạng thái của token (ví dụ: <code>ACTIVE</code>)</td></tr><tr><td><strong>Action</strong></td><td>Xóa token khi không còn cần sử dụng</td></tr></tbody></table>

Chỉ các token đang ở trạng thái **ACTIVE** mới được sử dụng để xác thực API Gateway.

<figure><img src="../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Xoá Authentication Token

Để xoá một token:

1. Tick chọn token trong danh sách.
2. Nhấn nút **Delete.**
3. Xác nhận để hoàn tất thao tác xoá.

Token sau khi xoá sẽ không thể sử dụng lại được để xác thực các truy cập vào AI Gateway.

<figure><img src="../../../.gitbook/assets/image (8) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Lưu ý:**

* Token hoạt động như một **chứng chỉ tạm thời** – hãy bảo mật tuyệt đối, tránh chia sẻ công khai.
* Mỗi token chỉ dùng cho **1 AI Gateway cụ thể**.
* Nên định kỳ rà soát và xoá các token không còn sử dụng để giảm rủi ro bảo mật.
{% endhint %}

Tuyệt vời! Dưới đây là phần hướng dẫn **tích hợp Authentication Token để gọi API qua AI Gateway**:

## Tích hợp Authentication Token để gọi API

Sau khi đã tạo token và token đang ở trạng thái `ACTIVE`, bạn có thể sử dụng token này để gọi API thông qua AI Gateway.

Bạn cần **gửi token trong header** của HTTP request. Token này sẽ được AI Gateway kiểm tra trước khi forward request đến LLM Model.

**Ví dụ với `curl`:**

```bash
curl -X POST https://user-123456-demo-gateway.ai-gateway.vngcloud.vn/deepseek/deepseek-chat/chat/completions \
                --header 'Authorization: Bearer {YOUR_TOKEN}' \
                --header 'Content-Type: application/json' \
                --data '{"model": "deepseek-chat", "messages": [{"role": "user", "content": "What is AI?"}]}'
```

**Trong đó:**

* `<YOUR_TOKEN>` chính là **token vừa tạo.**

Nếu token sai hoặc đã hết hiệu lực, AI Gateway sẽ trả về lỗi `Invalid authentication token.`
