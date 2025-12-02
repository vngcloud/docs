# Sử dụng MaaS với AI Gateway

Để MaaS có thể sử dụng các tính năng của AI Gateway (Rate Limit, Model Caching... ), bạn hãy thực hiện theo các bước sau:

**Bước 1:** Truy cập giao diện AI Gateway tại VNG Cloud Console thông qua đường dẫn: [http://aigateway.console.vngcloud.vn/](http://aigateway.console.vngcloud.vn/)

**Bước 2:** Trong menu bên trái, chọn mục **AI Gateway**, sau đó nhấn vào nút **Create an AI Gateway**.

<figure><img src="/broken/files/qqp6KDcpdeNxUHH7VDyH" alt=""><figcaption></figcaption></figure>

**Bước 3:** Tại màn hình **Tạo Gateway mới**, vui lòng điền đầy đủ các thông tin sau:

* **AI Gateway Name:** Đặt tên dễ nhớ cho gateway của bạn. Tên này chỉ được chứa các ký tự **a–z, A–Z, 0–9, dấu gạch dưới (\_) hoặc dấu gạch ngang (-)**, và có độ dài từ **5 đến 50 ký tự**.
* **Model Provider:**
  * Chọn nhà cung cấp mô hình AI OpenAI Compatible.
  * **Model Type**: Chọn Model Type (xem tại [MaaS](https://aiplatform.console.vngcloud.vn/models/md-37404b64-0656-4c85-978c-a6e1b84ea8ac) ở portal AI Platform).
  * **Model Endpoint**: Điền URL của model (xem tại [MaaS](https://aiplatform.console.vngcloud.vn/models/md-37404b64-0656-4c85-978c-a6e1b84ea8ac) ở poral AI Platform).
  *

      <figure><img src="/broken/files/g41wCXIWChs9gqtqIDzp" alt=""><figcaption></figcaption></figure>
  *   **Authentication info**:

      * header\_name: Điền `Authorization`.
      * header\_value: Điền Api Key MaaS ( API Key trong hình được tạo ở [Portal ](https://aiplatform.console.vngcloud.vn/keys)AI Platform).

      <figure><img src="/broken/files/bWwHHoVEXQLXNFYlKG6K" alt="123"><figcaption></figcaption></figure>
* **Gateway Config:** Mặc định, hệ thống sẽ bật tính năng **Authenticated Gateway.**

**Bước 4**: Chọn Create an AI Gateway, AI Gateway của bạn sẽ được khởi tạo và sẵn sàng để sử dụng.

<figure><img src="../../../.gitbook/assets/image (15) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 5**: Sau khi AI Gateway được khởi tạo bạn cần [tạo Token](https://docs.vngcloud.vn/vng-cloud-document/vn/ai-stack/ai-gateway/ai-gateway/lam-viec-voi-authentication-token) để gọi API.

**Bước 6**: Sau khi bạn tạo token, bạn có thể cấu hình rate limit cụ thể trên từng token theo nhu cầu cá nhân.

<figure><img src="/broken/files/07oQFBAMzbJUalPdUhwe" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

\
**Bước 7**: Trong mục **Providers & Model**, tìm mô hình AI bạn đã cấu hình. Tại mô hình đó, nhấn vào biểu tượng **Curl command** để lấy câu lệnh mẫu.

<figure><img src="/broken/files/lI3wkln8QrS0fGY7W9Rs" alt=""><figcaption></figcaption></figure>

**Bước 8**: Sao chép đoạn lệnh `curl` được hiển thị và thực thi lệnh đó trên máy tính cá nhân của bạn (qua Terminal hoặc Command Prompt).

<figure><img src="../../../.gitbook/assets/image (19) (3).png" alt=""><figcaption></figcaption></figure>

Ví dụ:

```
curl --request POST \
--url 'https://user-55461-demo-aigateway.ai-gateway.vngcloud.vn/openai-compatible/gemini-2.5-pro/v1/chat/completions' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {AUTHENTICATION_TOKEN}' \
--data '{
  "model": "gemini-2.5-pro",
  "messages": [
    {
      "role": "user",
      "content": "What is AI?"
    }
  ]
}'
```

**Lưu ý:**

* Thay thế `{AUTHENTICATION_TOKEN}` bằng token được tạo ở bước 5.
