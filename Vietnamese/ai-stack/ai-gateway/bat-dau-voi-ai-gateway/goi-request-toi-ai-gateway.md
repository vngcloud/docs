# Gọi request tới AI Gateway

Sau khi khởi tạo xong một AI Gateway, bạn có thể bắt đầu gửi request đến mô hình AI đã cấu hình theo các bước sau:

**Bước 1:** Truy cập [AI Gateway Portal](http://aigateway.console.vngcloud.vn/), tìm đến gateway mà bạn vừa tạo.

**Bước 2:** Trong mục **Providers & Model**, tìm mô hình AI bạn đã cấu hình. Tại mô hình đó, nhấn vào biểu tượng **Curl command** để lấy câu lệnh mẫu.

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 3:** Sao chép đoạn lệnh `curl` được hiển thị và thực thi lệnh đó trên máy tính cá nhân của bạn (qua Terminal hoặc Command Prompt).

<figure><img src="../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Ví dụ:

```bash
curl -X POST https://user-60108-gateway-0b50037b-93.ai-gateway.vngcloud.vn/deepseek/deepseek-chat/chat/completions \
     --header 'Authorization: Bearer {AUTHENTICATION_TOKEN}' \
     --header 'Content-Type: application/json' \
     --data '{
       "model": "deepseek-chat",
       "messages": [
         {
           "role": "user",
           "content": "What is AI?"
         }
       ]
     }'
```

**Lưu ý:**

* Thay thế `{AUTHENTICATION_TOKEN}` bằng token được cung cấp sau khi tạo Gateway.
* Bạn có thể chỉnh sửa nội dung của prompt (nội dung câu hỏi) trong phần `"content"` để phù hợp với mục đích sử dụng của mình.
* Nếu AI Gateway mà bạn đang sử dụng **được bật chế độ xác thực (Authenticated Gateway)**, bạn cần t**hêm một header tên là `cf-aig-authorization`** vào request HTTP của bạn.&#x20;

Ví dụ, thay vì dùng header thông thường kiểu:

```http
Authorization: Bearer {AUTHENTICATION_TOKEN}
```

Bạn phải dùng:

```http
cf-aig-authorization: Bearer {AUTHENTICATION_TOKEN}
```

Sau khi thực hiện, bạn sẽ nhận được phản hồi từ mô hình AI theo đúng định dạng JSON.
