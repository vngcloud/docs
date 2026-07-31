---
description: >-
  Tổng quan chức năng của các AI model trên MaaS — mục đích sử dụng, nguyên lý
  hoạt động cơ bản và loại dữ liệu đầu vào chính theo từng nhóm model.
---

# Giới thiệu về AI Model

GreenNode MaaS giúp bạn dùng ngay các AI model hàng đầu — từ trò chuyện, viết code đến xử lý ảnh và tài liệu — mà không cần tự huấn luyện hay vận hành hạ tầng GPU riêng. Trang này giải thích AI model dùng để làm gì, hoạt động theo nguyên lý nào, và mỗi nhóm model nhận loại dữ liệu đầu vào nào, giúp bạn chọn đúng model trước khi vào [Các Model được cung cấp](cac-model-duoc-cung-cap.md).

***

## Mục đích sử dụng

AI model trên MaaS là các model học sâu (deep learning) đã được huấn luyện sẵn, giúp tự động hoá các tác vụ mà trước đây cần con người xử lý trực tiếp: trả lời câu hỏi, tóm tắt/soạn nội dung, sinh và sửa code, đọc hiểu hình ảnh, tạo ảnh từ mô tả, trích xuất dữ liệu từ tài liệu, hoặc tìm kiếm theo ngữ nghĩa. Thay vì viết rule cứng cho từng trường hợp, bạn mô tả yêu cầu bằng ngôn ngữ tự nhiên (prompt) và model tự suy luận ra kết quả phù hợp.

## Nguyên lý hoạt động

Ở mức chức năng cơ bản, một AI model xử lý request theo 3 bước:

```
Input (text / ảnh / audio / PDF)
        │
        ▼
  Token hóa dữ liệu đầu vào
        │
        ▼
Model dự đoán/sinh output dựa trên
 pattern học được từ dữ liệu huấn luyện
        │
        ▼
   Output (text / ảnh / vector / JSON...)
```

* **Token hóa:** Dữ liệu đầu vào (câu chữ, pixel ảnh...) được chia thành các đơn vị nhỏ gọi là **token**.
* **Dự đoán theo ngữ cảnh:** Model không "hiểu" theo nghĩa con người, mà dự đoán token tiếp theo có khả năng phù hợp nhất, dựa trên toàn bộ ngữ cảnh (prompt, lịch sử hội thoại, system prompt) và pattern đã học từ khối dữ liệu huấn luyện khổng lồ.
* **Chế độ suy luận (thinking / non-thinking):** Một số model — đặc biệt các model dạng "Reasoning" như Qwen, GLM, DeepSeek — hỗ trợ chế độ **thinking** (suy luận từng bước, chain-of-thought) giúp tăng độ chính xác cho bài toán nhiều bước, đánh đổi bằng thời gian phản hồi lâu hơn; chế độ **non-thinking** trả lời nhanh hơn cho các tác vụ đơn giản.

{% hint style="info" %}
Càng nhiều token trong context (prompt + lịch sử hội thoại), model xử lý càng lâu và chi phí càng cao — xem cách tính phí theo token tại [Cách tính phí](cach-tinh-phi.md).
{% endhint %}

## Phân loại model theo chức năng

| Nhóm model                 | Mục đích sử dụng                                                       | Dữ liệu đầu vào chính                  | Use-case tiêu biểu                                                     |
| --------------------------- | ------------------------------------------------------------------------ | ---------------------------------------- | -------------------------------------------------------------------------- |
| Chat / Soạn thảo           | Hỏi đáp, tóm tắt, viết & chỉnh sửa nội dung                             | Văn bản (text), system prompt          | Trợ lý ảo, soạn báo cáo, hỏi đáp nội bộ                                   |
| Code                        | Sinh, sửa code, code review, viết unit test                            | Văn bản/code, ngữ cảnh nhiều file       | Tự động hoá script, chỉnh sửa đa file, vòng lặp code-run-fix              |
| Reasoning (Suy luận)       | Giải bài toán logic/nghiệp vụ nhiều bước, lập kế hoạch, kiểm tra ràng buộc | Văn bản mô tả bài toán/ràng buộc        | Tính toán nhiều bước, kiểm tra điều kiện, lập kế hoạch                    |
| Vision (đa phương thức)   | Đọc hiểu, mô tả, phân loại nội dung hình ảnh                            | Hình ảnh + văn bản                     | Đọc biểu đồ/screenshot, kiểm tra UI, trích nội dung từ ảnh               |
| Image Generation           | Sinh hình ảnh mới từ mô tả văn bản                                      | Văn bản (prompt)                        | Banner, ảnh minh hoạ, mockup cho social/marketing                        |
| OCR / Document AI (IDP)    | Trích xuất văn bản & trường dữ liệu có cấu trúc từ tài liệu             | Ảnh scan hoặc file PDF                  | Bóc tách hóa đơn, đọc CCCD/hộ chiếu/GPLX, chuyển ảnh tài liệu → text     |
| Embedding (RAG · Bước 1)  | Sinh vector biểu diễn ngữ nghĩa của văn bản                             | Văn bản                                 | Semantic search, xây pipeline RAG, tìm kiếm tài liệu nội bộ              |
| Rerank (RAG · Bước 2)     | Xếp hạng lại kết quả truy hồi theo độ liên quan                         | Cặp (câu hỏi, đoạn văn bản truy hồi)   | Tăng độ chính xác/relevance cho hệ thống RAG & tra cứu                    |

## Bắt đầu

| Tôi muốn...                                    | Đi đến                                            |
| ------------------------------------------------- | -------------------------------------------------- |
| Xem danh sách model theo từng nhóm chức năng    | [Các Model được cung cấp](cac-model-duoc-cung-cap.md) |
| Xem đơn giá theo model                          | [Bảng giá Model](bang-gia-model.md)                |
| Thử nhanh model trước khi tích hợp              | [Playground](playground.md)                        |
| Gọi model qua API                               | [MaaS API](maas-api.md)                            |
