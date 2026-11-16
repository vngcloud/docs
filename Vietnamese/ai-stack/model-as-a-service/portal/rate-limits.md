---
description: "Mỗi tài khoản có giới hạn request mặc định trên từng model. Mức cao hơn được xét theo từng trường hợp."
---

# Rate limit

## Giới hạn mặc định

| Giới hạn | Giá trị | Cách đếm |
| --- | --- | --- |
| Request mỗi phút | **10 RPM** trên mỗi model | Theo tài khoản và theo model. Mọi API key của tài khoản dùng chung một bộ đếm. |

* Chạy đều 10 RPM cả ngày tương đương 14.400 request cho mỗi model. Mặc định không có giới hạn ngày riêng.
* Tạo thêm API key không làm tăng giới hạn, vì các key dùng chung bộ đếm của tài khoản.
* Một số model có giới hạn riêng thay cho mặc định (ví dụ giới hạn request và token theo ngày). Trang model trên portal và các header `x-ratelimit-*` của response cho biết giới hạn đang áp dụng cho bạn.
* Tài khoản đã được cấp mức cao hơn thì dùng mức đó.

{% hint style="info" %}
**Đã đối chiếu production**

Mức mặc định và cách đếm đã đối chiếu với cấu hình gateway production ngày 2026-11-14.
{% endhint %}

## Khi chạm giới hạn

Request trả `429` kèm `x-ai-error-code: request_denied` và message nêu giới hạn bị vượt. Các header `x-ratelimit-*` trong response cho biết giới hạn nào đang áp dụng và còn bao nhiêu giây đến lúc reset. Xem [Giới hạn & rate limit](../api-reference/limits.md).

* Retry với exponential backoff và tuân theo `Retry-After`. Xem [Lỗi](../api-reference/errors.md).
* Dàn đều lưu lượng: 10 RPM tương đương 6 giây một request.
* Giảm reasoning effort để mỗi lần gọi ngắn hơn, và gộp việc vào ít request hơn.

## Đề nghị tăng giới hạn

Cần hơn 10 RPM? [Liên hệ GreenNode](https://helpdesk.greennode.ai/portal/en/newticket) để được xét vào whitelist. Ghi rõ tài khoản, model ID, mức RPM cần và lưu lượng dự kiến. Yêu cầu được xét theo từng trường hợp và phụ thuộc năng lực phục vụ của model.
