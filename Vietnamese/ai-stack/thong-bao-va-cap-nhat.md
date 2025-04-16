# Thông báo và cập nhật

## Tính năng sắp ra mắt

### AI Platform

**Model Tuning**

Tùy chỉnh mô hình AI theo tập dữ liệu riêng của bạn thông qua giao diện đơn giản.

* Hỗ trợ các mô hình ngôn ngữ phổ biến như LLaMA, Mistral, Falcon…
* Hệ thống tối ưu tài nguyên và tự động hoá quá trình training.

**Model as a Service (MaaS)**

Đóng gói và public mô hình như một dịch vụ.

* Cung cấp endpoint API riêng biệt cho mỗi mô hình.
* Hỗ trợ billing và phân quyền truy cập.

**Tích hợp trực tiếp với AI Gateway**

Triển khai inference và tạo endpoint qua AI Gateway chỉ bằng một click.

* Không cần cấu hình thủ công.
* Tận dụng tính năng bảo mật và traffic control từ AI Gateway.

### AI Gateway

**Rate Limiting**

Cấu hình giới hạn linh hoạt theo IP, user, token hoặc thời điểm trong ngày.

* Hỗ trợ theo cấp độ tổ chức và cá nhân.
* Tự động cảnh báo khi tiệm cận ngưỡng.

**Caching thông minh**

Tùy chỉnh thời gian lưu cache và vùng dữ liệu được cache.

* Tối ưu performance cho các use case nhiều lượt truy vấn giống nhau.
* Giảm chi phí inference đáng kể.

**Retry & Fallbacks**

Tự động retry khi model trả lỗi hoặc timeout.

* Có thể cấu hình fallback sang model khác (VD: từ GPT-4o fallback sang GPT-3.5)
* Tăng độ tin cậy cho ứng dụng AI trong môi trường production.

**Guardrails**

Kiểm soát đầu ra của mô hình trước khi trả về cho người dùng:

* Lọc nội dung nhạy cảm hoặc độc hại.
* Hỗ trợ custom rules theo yêu cầu từng doanh nghiệp.

## Apr 16, 2025

### AI Platform

**Notebook: Trải nghiệm phát triển linh hoạt hơn**

* Hỗ trợ **nhiều loại môi trường dựng sẵn (pre-built)** theo từng framework: PyTorch, TensorFlow,...
* Cho phép **mount Network Volume trực tiếp vào Notebook**, dễ dàng lưu trữ và chia sẻ dữ liệu.

**Model Registry: Quản lý mô hình tập trung và chuyên nghiệp**

* Hỗ trợ import model từ Network Volume hoặc S3 nhanh chóng.

#### **Inference: Tự động mở rộng và tối ưu hiệu suất**

* Giao diện khởi tạo đơn giản, hỗ trợ chọn **pre-built container (Triton, vLLM)**.
* Hỗ trợ **GPU instance đa dạng**, auto-scaling với cấu hình replica min/max.
* Tích hợp với Model Registry: chỉ cần chọn model là có thể triển khai ngay.

**Network Volume: Lưu trữ dữ liệu linh hoạt**

* Cho phép tạo, gắn và chia sẻ **Network Volume giữa các Notebook và Inference**.
* Dễ dàng kết nối với S3 để upload dataset, model checkpoint, v.v.
* Tăng hiệu năng đọc/ghi cho khối lượng lớn dữ liệu AI.

### AI Gateway

**Kết nối nhiều nguồn mô hình mạnh mẽ**

* Hỗ trợ kết nối đến **các nhà cung cấp LLM hàng đầu**: **OpenAI** (gpt-4o, gpt-3.5-turbo...); **Anthropic** (claude-3-opus, haiku, sonnet); **Google Gemini** (gemini-1.5, 2.0...); **DeepSeek** (deepseek-chat, reasoner)

**Cấu hình dễ dàng, triển khai nhanh chóng**

* Khởi tạo AI Gateway chỉ trong vài bước: đặt tên, chọn model, cấu hình rate limit, tạo token.

**Tính năng mới: Token Management & Rate Limiting**

* Quản lý token theo từng ứng dụng/client – dễ dàng phân quyền truy cập.
* Cấu hình giới hạn truy cập theo thời gian (requests per second/minute).

#### **Monitoring & Logging nâng cao**

* Giao diện hiển thị real-time logs và thống kê theo thời gian: tổng số request, tỉ lệ lỗi, latency...
* Hỗ trợ lọc theo endpoint, token, status code.
