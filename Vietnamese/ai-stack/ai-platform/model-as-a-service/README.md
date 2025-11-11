---
description: >-
  AI Platform cung cấp dịch vụ Mô hình dưới dạng Dịch vụ (MaaS), cho phép các
  nhà phát triển và doanh nghiệp dễ dàng tích hợp các mô hình AI mạnh mẽ vào ứng
  dụng của họ.
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# Model as a Service

Truy cập vào phần [Models ](https://aiplatform.console.vngcloud.vn/models)trong AI Platform:

Để sử dụng và enable bất kỳ mô hình nào, bạn cần có API key. [xem thêm](../bat-dau-voi-ai-platform.md#id-6.-quan-ly-api-keys)&#x20;

Bạn có thể lọc các mô hình bằng các tùy chọn ở thanh bên trái:

* Nhà cung cấp (Provider): Google, Anthropic, OpenAI, GreenNode, ...
* Loại mô hình (Model Type):&#x20;
  * Chat: Được thiết kế cho các cuộc hội thoại tương tác. Chúng có khả năng lưu giữ ngữ cảnh và lịch sử cuộc trò chuyện.
  * Image Generation: Tạo ra hình ảnh mới dựa trên mô tả văn bản.
  * Speech to Text: Chuyển đổi âm thanh (giọng nói) thành văn bản.
  * Text to Speech: Chuyển đổi văn bản thành âm thanh (giọng nói).
  * Embedding: chuyển đổi dữ liệu (văn bản, hình ảnh, âm thanh,…) thành vector nhiều chiều, giúp máy tính hiểu và so sánh ngữ nghĩa để phục vụ tìm kiếm, phân loại hoặc gợi ý nội dung.
  * Completion: Xử lý từng yêu cầu (prompt) một cách độc lập mà không lưu lại lịch sử hội thoại.
* Trường hợp sử dụng (Use-case):
  * Vietnamese: Tối ưu cho các tác vụ tiếng Việt.
  * General Tasks: Phù hợp cho nhiều tác vụ chung.
  * Translation: Chuyên về dịch thuật.
  * Research: Hỗ trợ các tác vụ nghiên cứu.
  * Finance: Chuyên về lĩnh vực tài chính.
  * Marketing: Tối ưu cho tiếp thị.
  * Technology: Phục vụ các tác vụ liên quan đến công nghệ.

### Bật /  Tắt mô hình

1. Nhấp vào nút "Bật/Tăt model" (Toggle models)&#x20;
2. Lựa chọn mô hình: Một cửa sổ popup sẽ hiện ra. Tại đây, bạn có thể tìm kiếm và lọc mô hình theo Nhà cung cấp (Provider), Trạng thái (Status) hoặc Loại mô hình (Type).
3. Bật/tắt riêng lẻ hoặc hàng loạt mô hình.
4. Lưu (Save) các thay đổi.

<figure><img src="../../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

Để bắt đầu thử nghiệm và so sánh các mô hình trước khi tích hợp, bạn có thể sử dụng [Playground](playground.md)&#x20;

<figure><img src="../../../.gitbook/assets/image (1120).png" alt=""><figcaption></figcaption></figure>

### **Thử nghiệm với AI Platform Playground**

Trước khi tích hợp vào ứng dụng của bạn, hãy khám phá các khả năng của mô hình trong Playground:

* So sánh các mô hình khác nhau dựa trên độ trễ, độ chính xác và khả năng hỗ trợ.
* Gửi các yêu cầu thử nghiệm một cách tương tác và đánh giá kết quả đầu ra.
* Tinh chỉnh các tham số để tìm ra mô hình hoạt động tốt nhất cho trường hợp sử dụng cụ thể.

[**Xây dựng với API của AI Platform MaaS**](maas-api.md)

Sau khi thử nghiệm trong Playground, bạn có thể truy cập các mô hình thông qua AI Platform MaaS:

* Hỗ trợ cả yêu cầu đồng bộ và truyền phát (streaming) cho các ứng dụng thời gian thực.
