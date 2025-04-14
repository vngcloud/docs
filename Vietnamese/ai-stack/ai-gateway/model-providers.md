---
description: AI Gateway hỗ trợ kết nối đến các Model Provider hàng đầu
---

# Model Providers

Bên cạnh khả năng phục vụ các mô hình AI do người dùng tự triển khai thông qua AI Platform, **AI Gateway tại VNG Cloud** còn hỗ trợ **kết nối trực tiếp đến các nhà cung cấp Large Language Model (LLM) phổ biến nhất thế giới** hiện nay, giúp bạn:

* Sử dụng sức mạnh của các mô hình tiên tiến mà không cần tự triển khai hoặc huấn luyện.
* Gọi API qua **một endpoint thống nhất** của AI Gateway, không cần quản lý nhiều token hoặc SDK riêng lẻ.
* Kết hợp linh hoạt giữa mô hình nội bộ và mô hình của các bên thứ ba trong cùng hệ thống.

## **Các Model Provider được hỗ trợ**

### **Anthropic**

Nhà phát triển dòng mô hình Claude – nổi bật với khả năng hiểu ngữ cảnh dài và xử lý ngôn ngữ tự nhiên rất tốt.

* `claude-3-5-haiku-latest`: mô hình nhẹ, phản hồi nhanh, chi phí thấp.
* `claude-3-7-sonnet-latest`: cân bằng giữa tốc độ và chất lượng, phù hợp cho đa số ứng dụng.
* `claude-3-opus-latest`: mô hình mạnh nhất của Anthropic, phù hợp với yêu cầu reasoning phức tạp.

### **Google DeepMind**

Dòng mô hình Gemini với khả năng xử lý **đa modal** (văn bản + hình ảnh), chất lượng cao và phù hợp với ứng dụng cấp doanh nghiệp.

* `google/gemini-1.5-pro`: bản tiêu chuẩn, đa nhiệm, hiểu ngữ cảnh dài.
* `google/gemini-1.5-flash`: tối ưu tốc độ, chi phí thấp hơn.
* `google/gemini-2.0-flash`: bản mới nhất, nâng cấp hiệu suất.

### **OpenAI**

Dẫn đầu thị trường với các dòng GPT nổi tiếng, có hệ sinh thái phong phú và hiệu suất cao.

* `gpt-4o`: model mới nhất (GPT-4 Omni), đa modal, phản hồi nhanh, chi phí hợp lý hơn GPT-4 trước đây.
* `gpt-4o-mini`: phiên bản rút gọn, tiết kiệm chi phí.
* `gpt-3.5-turbo`: mô hình phổ biến cho chatbot, tổng hợp nội dung, hỗ trợ viết code.

### **DeepSeek**

Đội ngũ phát triển LLM nguồn mở với hiệu suất vượt trội trong các tác vụ lập luận và suy luận logic.

* `deepseek-chat`: tối ưu cho hội thoại, tốc độ phản hồi nhanh.
* `deepseek-reasoner`: nổi bật trong các bài toán reasoning, giải thích, và phân tích dữ kiện.

## **Ưu điểm khi dùng AI Gateway để gọi model bên thứ ba**

| Tính năng                             | Mô tả                                                                                |
| ------------------------------------- | ------------------------------------------------------------------------------------ |
| **Một API key – nhiều model**         | Không cần đăng ký riêng lẻ với từng provider.                                        |
| **Quản lý usage tập trung**           | Theo dõi tổng usage của tất cả model trên cùng một dashboard.                        |
| **Bảo mật & kiểm soát truy cập**      | Xác thực, giới hạn rate, phân quyền – giống như khi dùng model nội bộ.               |
| **Tương thích API format**            | Dùng cùng định dạng API chuẩn hóa bởi AI Gateway – không cần học nhiều SDK.          |
| **Chuyển đổi dễ dàng giữa các model** | Cùng một use case có thể thử Claude, GPT hoặc Gemini mà không cần sửa backend logic. |

