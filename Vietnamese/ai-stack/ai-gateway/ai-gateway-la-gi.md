# AI Gateway là gì?

## Tổng quan

**AI Gateway** là cổng kết nối tập trung giúp bạn tích hợp nhiều AI models (OpenAI, Google, Deepseek,...).Việc sử dụng AI Gateway giúp giảm độ phức tạp khi chuyển đổi model, hỗ trợ giám sát và quản lý, tối ưu chi phí, bảo mật dữ liệu.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

## Những điểm nổi bật của AI Gateway

* **Hỗ trợ đa mô hình AI (Multi-LLM Support):** AI Gateway đóng vai trò như một cổng kết nối tập trung, cho phép tích hợp linh hoạt với nhiều mô hình ngôn ngữ lớn (LLM) từ các nhà cung cấp khác nhau như OpenAI, Google, Deepseek,...
* **Giám sát toàn diện:** AI Gateway hỗ trợ giám sát hiệu suất và hoạt động thông qua metrics và logs, giúp người dùng dễ dàng theo dõi, phân tích và tối ưu hóa quá trình vận hành.
* **Tối ưu chi phí:** Tính năng caching **(coming soon)** giúp giảm số lượng request tới LLM Mode ,qua đó tiết kiệm chi phí và cải thiện tốc độ phản hồi.
* **Kiểm soát nội dung và hành vi - Guardrails (coming soon):** AI Gateway cho phép bạn thiết lập các lớp bảo vệ để đảm bảo đầu vào/ra từ mô hình AI luôn phù hợp với mục tiêu và mong muốn của bạn.
* **Tự động cân bằng tải (coming soon):** AI Gateway tự động phân phối lưu lượng giữa các mô hình AI để tối ưu hiệu suất và đảm bảo khả năng mở rộng ổn định.
* **Tự động xử lý lỗi (coming soon):**&#x20;
  * **Automatic Retries:** Tự động gửi lại yêu cầu trong trường hợp lỗi tạm thời.
  * **Automatic Fallbacks:** Tự động chuyển sang mô hình thay thế khi mô hình chính gặp sự cố, đảm bảo dịch vụ không bị gián đoạn.
* **Bảo mật:** đảm bảo an toàn cho các thông tin nhạy cảm của khách hàng như **authentication token** và **API key.**
