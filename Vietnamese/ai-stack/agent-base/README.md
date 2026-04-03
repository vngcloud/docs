# Agentbase

## Agentbase là gì?

**GreenNode Agentbase** là nền tảng hạ tầng chuyên biệt dành cho AI Agent — giúp bạn đưa ý tưởng từ code đến production mà không cần lo về server, scaling hay vận hành.

Thay vì mất hàng tuần tự dựng infra, bạn chỉ cần tập trung vào điều quan trọng nhất: **logic của agent**. Agentbase lo toàn bộ phần còn lại.

> *"Agentbase = Vercel dành riêng cho AI Agent"*

***

## Agentbase giải quyết vấn đề gì?

Xây dựng và triển khai AI Agent thực tế thường gặp những rào cản lớn:

* Tự quản lý server, container, autoscaling — tốn thời gian và công sức
* Bảo mật credential và API key khi kết nối với các dịch vụ bên ngoài
* Agent không có bộ nhớ — mỗi cuộc hội thoại bắt đầu lại từ đầu
* Khó theo dõi logs, metrics khi agent chạy trên production

Agentbase giải quyết tất cả những vấn đề này trong một nền tảng duy nhất.

***

## Lợi ích nổi bật

### Triển khai nhanh, không lo infra

Deploy agent lên cloud chỉ trong vài phút. Agentbase tự động quản lý vòng đời container, autoscaling theo tải thực tế và zero-downtime deployment — bạn không cần can thiệp vào hạ tầng.

### Bảo mật credential tự động

Mọi API key và token kết nối với dịch vụ bên ngoài (LLM, Slack, Google...) được quản lý tập trung và **tự động inject** vào agent khi chạy. Không cần hardcode, không lo lộ key.

### Agent có trí nhớ

Agentbase tích hợp sẵn Memory Service giúp agent ghi nhớ lịch sử hội thoại và học từ các tương tác trước — tạo trải nghiệm cá nhân hóa thực sự cho từng người dùng.

### Kết nối sẵn với GreenNode MaaS

Truy cập ngay các LLM model mạnh nhất qua GreenNode Model-as-a-Service với API tương thích OpenAI — không cần đăng ký thêm bất kỳ dịch vụ nào.

### Quan sát toàn diện

Logs, metrics CPU/RAM, lịch sử request — tất cả có sẵn trong dashboard. Bạn luôn biết agent đang hoạt động như thế nào trên production.

***

## Dành cho ai?

| Đối tượng | Agentbase mang lại |
| --- | --- |
| **AI Engineer / Developer** | Tập trung viết logic agent, không mất thời gian quản lý infra |
| **Startup / Product Team** | Ra mắt AI product nhanh hơn, tiết kiệm chi phí vận hành |
| **Doanh nghiệp** | Triển khai AI Agent an toàn với identity, credential và observability đầy đủ |

***

## Bắt đầu với Agentbase

| Tôi muốn... | Hướng đến |
| --- | --- |
| Dùng AI Agent ngay, không cần code | [OpenClaw 1-Click](one-click-openclaw/README.md) |
