# Khởi tạo AI Gateway

Để bắt đầu sử dụng AI Gateway trên VNG Cloud, bạn hãy thực hiện theo các bước sau:

**Bước 1:** Truy cập giao diện AI Gateway tại VNG Cloud Console thông qua đường dẫn: [http://aigateway.console.vngcloud.vn/](http://aigateway.console.vngcloud.vn/)

**Bước 2:** Trong menu bên trái, chọn mục **AI Gateway**, sau đó nhấn vào nút **Create an AI Gateway**.

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

**Bước 3:** Tại màn hình **Tạo Gateway mới**, vui lòng điền đầy đủ các thông tin sau:

* **AI Gateway Name:** Đặt tên dễ nhớ cho gateway của bạn. Tên này chỉ được chứa các ký tự **a–z, A–Z, 0–9, dấu gạch dưới (\_) hoặc dấu gạch ngang (-)**, và có độ dài từ **5 đến 50 ký tự**.
* **Model Provider:**
  * Chọn nhà cung cấp mô hình AI bạn muốn kết nối như **OpenAI, Anthropic, Google, DeepSeek**.
  * **API Key:** Nhập **API Key** tương ứng từ nhà cung cấp. Nếu chưa có, bạn có thể nhấn **Get API Key** — chúng tôi sẽ chuyển bạn đến trang tương ứng để lấy thông tin.
  * **Chọn mô hình (Model):** Lựa chọn mô hình AI bạn muốn sử dụng (ví dụ: _gemini-1.5_, _gemini-2.0_,...). Nếu muốn xem toàn bộ danh sách, hãy nhấn **View full list** để hiển thị tất cả các model mà chúng tôi hỗ trợ.
* **Gateway Config:** Mặc định, hệ thống sẽ bật tính năng **Authenticated Gateway**. Một **authenticated token** sẽ được tạo tự động – bạn có thể sử dụng token này để gửi request đến AI Gateway.

**Bước 4**: Chọn Create an AI Gateway, AI Gateway của bạn sẽ được khởi tạo và sẵn sàng để sử dụng.

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
