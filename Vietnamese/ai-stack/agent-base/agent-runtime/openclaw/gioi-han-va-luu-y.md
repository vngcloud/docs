# Giới hạn và Lưu ý

## Giới hạn hiện tại

| Giới hạn | Mô tả |
| --- | --- |
| **Custom domain** | Chưa hỗ trợ |
| **Team/shared instance** | Chưa hỗ trợ |
| **Backup dữ liệu** | Chưa hỗ trợ |
| **Deploy Node từ Gateway** | Chưa hỗ trợ (Coming Soon — Phase 2) |

***

## Lưu ý quan trọng

{% hint style="warning" %}
**Xóa instance là vĩnh viễn:**

Khi xóa instance, toàn bộ dữ liệu sẽ bị **xóa vĩnh viễn** và không thể khôi phục. Hãy đảm bảo bạn đã sao lưu dữ liệu cần thiết trước khi xóa.
{% endhint %}

{% hint style="warning" %}
**BYOK — API key không hợp lệ:**

Nếu API key BYOK hết hạn hoặc bị thu hồi sau khi deploy, instance sẽ không thể gọi model AI. Bạn cần cập nhật key tại **Settings → Config** trong OpenClaw Gateway.
{% endhint %}

***

## Lưu ý khi kết nối Channel

| Tình huống | Vì sao cần lưu ý | Nên làm |
| --- | --- | --- |
| **Bot Token để trống khi deploy** | Form deploy không bắt buộc nhập Bot Token, nhưng thêm token sau khi instance đã tạo phải nhờ agent tự cập nhật cấu hình channel — khó thực hiện và dễ sai | Lấy bot token trước, rồi nhập ngay tại bước **Cấu hình Channel** khi deploy |
| **Gửi `/start` khi instance còn `Creating`** | Bot chỉ sinh được pairing code khi instance đã chạy; gửi sớm thì bot **không trả về code nào**, và tin nhắn đó không được xử lý lại khi instance Active | Đợi trạng thái 🟢 **Active** tại **My Agents**, sau đó mới gửi `/start` |

Chi tiết: [Lấy Bot Token và Pairing](lay-bot-token-va-pairing.md).

***

Nếu gặp bất kỳ khó khăn nào trong quá trình sử dụng, vui lòng liên hệ đội ngũ GreenNode để được hỗ trợ.
