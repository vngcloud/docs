---
description: >-
  Playground là một giao diện trực quan trên nền tảng, cho phép bạn thử nghiệm
  và so sánh các mô hình AI một cách nhanh chóng mà không cần viết code. Đây là
  môi trường lý tưởng để khám phá các khả năng
---

# Playground

### Truy cập [Playground](https://aiplatform.console.vngcloud.vn/playground)

### Hướng dẫn thử nghiệm mô hình

1. Chọn loại mô hình tùy thuộc vào tác vụ của bạn: Chat, Completion, Image Generation, Text to Speech, Speech to Text, Embedding
2. Chọn loại mô hình: Ở bảng điều khiển bên phải, chọn một mô hình từ danh sách&#x20;
3. Thiết lập prompt&#x20;
   * Trong phần System prompt, hãy định nghĩa các hướng dẫn hoặc ngữ cảnh cho mô hình. Bạn cũng có thể thêm các ví dụ để định hướng hành vi của nó.
4.  [Tinh chỉnh các tham số:](playground.md#huong-dan-tinh-chinh-thamso-mo-hinh)

    <figure><img src="/broken/files/nenCdlcVcXXtvDGkUDAG" alt=""><figcaption></figcaption></figure>
5. Bắt đầu thử nghiệm:

* Nhập câu lệnh của bạn và quan sát cách các mô hình khác nhau phản hồi.

6. Lưu cấu hình:

* Sao chép dưới dạng code: Nhấp vào biểu tượng `<> API`&#x20;
* Chọn ngôn ngữ lập trình:&#x20;
  * Curl: Mã lệnh này được sử dụng trong Terminal hoặc Command Prompt, giúp bạn dễ dàng kiểm tra API trực tiếp mà không cần viết code.
  * Python: Cung cấp đoạn mã Python sẵn sàng để bạn sao chép và sử dụng trong các dự án Python của mình.
  * Node.js: Cung cấp đoạn mã Node.js, phù hợp cho các dự án web và ứng dụng server-side.

<figure><img src="../../../.gitbook/assets/image (1124).png" alt=""><figcaption></figcaption></figure>

### Hướng dẫn tinh chỉnh tham số mô hình

Khi sử dụng Playground, bạn có thể điều chỉnh các thông số sau để kiểm soát kết quả đầu ra của mô hình. Các thông số này có thể khác nhau tùy thuộc vào loại mô hình bạn chọn.

**Mô hình Chat**

* &#x20;Past messages included: Số lượng tin nhắn gần nhất mà mô hình sẽ ghi nhớ.
  * Phạm vi: 1 - 20 (Mặc định: 10).
* Maximum token output: Số token tối đa mà mô hình có thể tạo ra.
  * Phạm vi: 1 - 10000 (Mặc định: 800).
* Temperature: Kiểm soát độ ngẫu nhiên của câu trả lời.
  * 0: Kết quả nhất quán, mang tính xác định cao.
  * < 1: Kết quả tập trung, chính xác, lý tưởng cho tóm tắt hoặc hỏi đáp.
  * ≈ 1: Khuyến khích sự sáng tạo và đa dạng trong câu trả lời.
  * Phạm vi: 0 - 2 (Mặc định: 1).
* Top P: Ngưỡng xác suất để mô hình chọn từ vựng. Giúp cân bằng giữa sự tự nhiên và đa dạng của câu trả lời.
  * Phạm vi: 0 - 1 (Mặc định: 0.7).
* Presence Penalty: Mức phạt cho các từ đã xuất hiện trong cuộc trò chuyện, khuyến khích mô hình tạo ra các chủ đề mới và giảm lặp từ.
  * Phạm vi: -2 đến 2 (Mặc định: 0).

**Mô hình Completion**

* Maximum token output: Tương tự như Chat, đây là Số token tối đa mà mô hình có thể tạo ra.
  * Phạm vi: 1 - 10000 (Mặc định: 2048).
* Temperature: Tương tự như Chat, kiểm soát tính ngẫu nhiên của kết quả.
  * Phạm vi: 0 - 2 (Mặc định: 1).
* Top P: Tương tự như Chat, giúp cân bằng tính tự nhiên và đa dạng của văn bản.
  * Phạm vi: 0 - 1 (Mặc định: 0.7).

**Mô hình Image Generation**

* Number of Images: Số lượng hình ảnh được tạo ra sau mỗi yêu cầu.
  * Phạm vi: 1 - 4 (Mặc định: 1).
* Kích thước ảnh (Image size): Kích thước của hình ảnh được tạo ra.
  * Các tùy chọn: 256x256, 512x512, 1024x1024 (Mặc định: 1024x1024).
* Định dạng phản hồi (Response format): Định dạng trả về của kết quả (thường là Base64).

**Mô hình Text to Speech**

* Voice: Lựa chọn giọng nam/nữ theo vùng miền.
  * Các tùy chọn: (Mặc định: Nữ Miền Nam)
    * Nữ Miền Nam&#x20;
    * Nữ  Miền Bắc
    * Nam Miền Nam&#x20;
    * Nam Miền Bắc
* Speed: Tốc độ đọc của giọng nói.
  * Phạm vi: 0.8 - 1.2 (Mặc định: 1).
* Encoding type: Định dạng tệp âm thanh đầu ra.
  * Các tùy chọn: WAV, MP3 (Mặc định: MP3).

**Mô hình Speech to Text**

* Encoding type: Định dạng tệp âm thanh đầu vào.
  * Các tùy chọn: WAV, MP3 (Mặc định: MP3).

**Mô hình Embedding**

* Presence Penalty: Mức phạt cho các từ đã xuất hiện trong cuộc trò chuyện, khuyến khích mô hình tạo ra các chủ đề mới và giảm lặp từ.
  * Phạm vi: -2 đến 2 (Mặc định: 0).

Để xem thêm các thông số chi tiết, bạn có thể tham khảo tài liệu của [vLLM ](../../../)và [OpenAI](https://platform.openai.com/docs/api-reference/introduction).

### So sánh mô hình&#x20;

Tính năng này cho phép bạn chạy và so sánh kết quả đầu ra của hai mô hình cùng lúc.

* Nhấp vào nút So sánh (Compare) để mở hai cửa sổ trò chuyện song song.
* Bạn có thể nhập câu lệnh và gửi tới cả hai mô hình cùng một lúc để xem phản hồi và đánh giá hiệu quả.

<figure><img src="../../../.gitbook/assets/image (1125).png" alt="" width="164"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1127).png" alt="" width="563"><figcaption></figcaption></figure>
