---
description: Cổng kết nối thông minh cho dịch vụ AI
---

# AI Gateway

## 1. AI Gateway là gì?

**AI Gateway** là một thành phần trung tâm trong hệ sinh thái **AI Stack** của VNG Cloud, đóng vai trò như **API Gateway chuyên biệt cho dịch vụ AI**. Nó giúp quản lý, bảo mật, tối ưu và giám sát việc truy cập đến các **Inference Services** (dịch vụ suy luận từ model AI) đã triển khai thông qua **AI Platform và các AI Model Provider phổ biến như ChatGPT, Gemini, AWS Bedrock,...**

**AI Gateway giup ích gì?**

Tóm lại, AI Gateway là lớp trung gian giữa **người dùng cuối / ứng dụng** và các **AI model API**, giúp:

* **Đảm bảo hiệu năng**: AI Gateway đóng vai trò như một **bộ điều phối thông minh**, giúp tối ưu hiệu năng truy cập đến các dịch vụ AI
  * **Tự động phân phối tải (load balancing)** giữa nhiều replica của một model inference → Giúp mô hình phản hồi nhanh hơn, kể cả khi có nhiều người dùng cùng truy cập.
  * **Caching thông minh** (tuỳ cấu hình) cho các kết quả inference có thể lặp lại.
  * Hỗ trợ **timeout control**, retry logic để bảo vệ hệ thống AI khi có lỗi tạm thời.
* **Cung cấp bảo mật**: AI Gateway tích hợp nhiều lớp bảo vệ giúp kiểm soát chặt chẽ việc truy cập mô hình AI
  * **Xác thực người dùng (Authentication)** qua API Key hoặc JWT Token.
  * Ghi log mọi request để phục vụ việc **audit, theo dõi hành vi bất thường** hoặc điều tra sự cố bảo mật.
* **Quản lý lưu lượng:** AI Gateway giúp kiểm soát và điều phối lưu lượng truy cập đến các model AI
* **Dễ dàng tích hợp vào hệ thống thật:** AI Gateway giúp đơn giản hóa việc đưa AI vào ứng dụng thực tế
  * Cung cấp endpoint dạng **RESTful API**, chuẩn hóa giao tiếp cho mọi nền tảng (web, mobile, backend, IoT).
  * Tự động sinh endpoint khi model được triển khai → Không cần dev sửa code hoặc làm DevOps thủ công.
  * Dễ tích hợp với hệ thống CI/CD để tự động cập nhật model, version mới

## 2. Các tính năng chinh của AI Gateway

**Authentication & Authorization**

* Hỗ trợ xác thực thông qua **API key** và **JWT token**.
* Có thể cấu hình **cấp quyền truy cập riêng biệt** cho từng model (theo user, app, nhóm...). (coming soon)
* Giúp bảo vệ model AI không bị truy cập trái phép.

**Routing & Load Balancing (coming soon)**

* Tự động định tuyến các request đến đúng **Inference Service** dựa trên URL endpoint hoặc header.
* Hỗ trợ **load balancing** giữa nhiều replica của cùng một model để đảm bảo hiệu suất cao và không bị nghẽn.

**Monitoring & Logging**

* Tích hợp **bảng điều khiển (dashboard)** theo dõi:
  * Số lượng request
  * Thời gian phản hồi (latency)
  * Tỷ lệ lỗi
* Ghi lại logs theo từng request để **debug** hoặc **audit**.

**Rate Limiting & Catching (**&#x63;oming soon)

* Giới hạn số lượng request theo: User/API Key, IP, Endpoint
* Lưu lại kết quả inference của các request trước đó để sử dụng lại khi có những request giống hệt sau này, giúp tiết kiệm tài nguyên và tăng tốc độ phản hồi.

**Payload Transformation (coming soon)**

* Cho phép thay đổi **cấu trúc request/response** nếu cần (ví dụ: chuyển đổi format đầu vào đầu ra giữa frontend và model).
* Giúp dễ dàng tích hợp AI vào các hệ thống hiện có, mà không cần sửa source code model.

## 3. Cách AI Gateway hoạt động

#### **Luồng hoạt động tổng quát**

1. **Ứng dụng (Client / Web / Mobile)** gửi request đến **AI Gateway** tại một endpoint cụ thể.
2. **AI Gateway**:
   * Kiểm tra xác thực (API key, token).
   * Kiểm tra quota, giới hạn rate.
   * Ghi log và thống kê.
   * Định tuyến request đến đúng **Inference Service** (model đã triển khai).
3. **Inference Service** xử lý request và trả kết quả về lại AI Gateway.
4. **AI Gateway** trả response lại cho người dùng.

#### **Tích hợp với AI Platform**

* AI Gateway được **kết nối trực tiếp với Model Registry và Inference Service** trên AI Platform.
* Khi bạn triển khai một model trên AI Platform, AI Gateway **tự động tạo endpoint tương ứng** để bạn có thể gọi API.
* Bạn có thể dùng dashboard để:
  * Quản lý endpoint,
  * Theo dõi usage,
  * Cấu hình access control và rate limit.

