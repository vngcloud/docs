# Sandbox — Bảo mật và giới hạn

## Mô hình cô lập

| Ranh giới | Mang lại gì |
|---|---|
| microVM mỗi session | Kernel, tiến trình, filesystem, bộ nhớ riêng. Trạng thái của session này không thấy được từ session khác và bị huỷ khi xoá session. Dùng Kata Containers + Cloud Hypervisor |
| Namespace mỗi người dùng | Mọi VM của một người dùng nằm trong namespace riêng (`agent-core-<userId>`), do nền tảng gắn — người gọi không thể đặt hay ghi đè |
| Xác thực ở gateway | Chỉ token hợp lệ của chủ sở hữu tài nguyên mới đi qua gateway; các chặng sau tin vào thông tin tenant do gateway gắn |
| Loại bỏ credential | Header `Authorization`, `Cookie` và các header danh tính bị gỡ trước khi request vào VM; không service-account token nào được mount vào pod sandbox |
| Node group riêng trên vKS | Workload sandbox tách sang node group bật nested virtualization, taint `nested-virt=true:NoSchedule`; pod sandbox chạy qua RuntimeClass `kata-clh` |

## Credential trong sandbox

| Chủ đề | Hành vi |
|---|---|
| Token của người gọi | Không bao giờ tới VM — bị gỡ ở gateway/runtime trước khi relay vào |
| Token nội bộ của nền tảng | Không mount vào pod sandbox; tool service tự ký JWT ngắn hạn riêng khi gọi vào runtime |
| Credential cho agent dùng | Nếu agent trong sandbox cần credential, truyền qua kênh riêng của bạn — không qua header mặc định |
| Vault credential | Hướng phát triển: tính năng credential vault của OpenSandbox chưa được tích hợp ở bản hiện tại |

## Mạng

| Luồng | Cho phép? |
|---|---|
| Vào: từ gateway và quản lý sandbox | Có |
| Ra: DNS, telemetry collector | Có |
| Ra: Internet công cộng | Có |
| Ra: dải IP riêng (RFC 1918), metadata service, API server Kubernetes | Không — chặn bằng network policy deny |

## Giới hạn và quota

| Giới hạn | Giá trị | Ghi chú |
|---|---|---|
| Số Code Interpreter mỗi người dùng | 5 (mặc định) | Ghi vào quota lần đầu bị tính |
| Số Browser mỗi người dùng | 5 (mặc định) | Cộng dồn theo loại tool |
| Tổng số session mỗi người dùng | 10 (mặc định) | Cộng qua mọi tool — session mới là thứ giới hạn tài nguyên thật |
| Thời gian tạo session (có VM nóng) | ~3 giây | |
| Thời gian tạo session (boot VM nguội) | ~17 giây | Burst vượt số VM nóng trong pool |
| Thời gian tạo tool lần đầu | vài phút | Phải dựng pool và boot VM đầu tiên |
| Một lời gọi proxy (kể cả streaming) | 10 phút | Vượt thì `504` |
| Lệnh shell đồng bộ | 30 giây | Dùng `startCommandExecution` cho việc dài hơn |
| Lệnh chạy nền | 15 phút | Kết quả lấy qua `getTask` |
| Dung lượng file mỗi lần đọc/ghi | 10 MiB | Vượt thì `413`; mỗi lần một file |
| Dung lượng recording | 64 MiB | Bản ghi lớn hơn không được lưu |
| Session mỗi endpoint | dưới 100 | Kể cả VM nóng trong pool |
| Lời gọi HTTP proxy đồng thời toàn service | 25 | Trần dùng chung mọi người gọi; vượt thì `503` |
| WebSocket proxy đồng thời toàn service | 25 | Vượt thì đóng với mã `1013` |
| WebSocket idle / kích thước message | 5 phút / 1 MiB | |
| TTL / idle timeout của session | Không có | Session chỉ kết thúc khi bị xoá |

{% hint style="warning" %}
Không có cơ chế tự dọn session: session bị quên vẫn giữ VM và chiếm slot quota cho tới khi bị xoá hoặc tool bị xoá. Luôn xoá session khi dùng xong.
{% endhint %}

## Trạng thái tài nguyên

| Trạng thái | Mô tả |
|---|---|
| `CREATING` | Đang dựng pool VM và boot VM đầu tiên |
| `ACTIVE` | Sẵn sàng tạo session và gọi tool |
| `FAILED` | Quá thời hạn chờ khi tạo — trạng thái cuối |
| `DELETED` | Đã xoá, quota đã trả |

## Mã lỗi thường gặp

| Mã | Ý nghĩa |
|---|---|
| `401` | Chưa đăng nhập hoặc token hết hạn — chạy lại flow đăng nhập của MCP client |
| `404` | Tài nguyên không tồn tại — hoặc thuộc người dùng khác (không lộ sự tồn tại) |
| `409` | Tài nguyên chưa `ACTIVE` khi gọi session/invoke |
| `413` | File vượt giới hạn dung lượng |
| `429` / `503` | Nền tảng bận hoặc quá số lời gọi đồng thời — thử lại sau |
| `502` / `504` | Lỗi/timeout hạ tầng sandbox; lời gọi vượt giới hạn 10 phút |

## Hướng phát triển

| Chủ đề | Trạng thái |
|---|---|
| Vault credential cho sandbox | Chưa tích hợp (tính năng upstream của OpenSandbox) |
| Custom sandbox runtime (image riêng, API session trực tiếp) | Đang nội bộ, chưa mở công khai — phụ thuộc mô hình billing |
| TTL / tự dọn session | Đang cân nhắc (TTL hoặc job dọn) |
| Ngôn ngữ khác Python cho `executeCode` | Hướng phát triển |
