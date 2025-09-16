---
description: >-
  Là cơ chế giới hạn số lượng request, token trong một khoảng thời gian nhất
  định để bảo vệ hệ thống khỏi lạm dụng, công bằng khi dùng chung một gateway và
  tối ưu chi phí, tính ổn định cho model
---

# Giới Hạn rate

## 1. Truy cập tính năng giới hạn Rate

1. Sau khi đã [ tạo Authentication Token](lam-viec-voi-authentication-token.md#tao-moi-authentication-token), tại danh sách các token chọn icon ở cột Hành Động như hình dưới để mở cấu hình giới hạn Rate

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

2. Hoặc có thể chọn Configure Rate limit khi tạo Authentication Token.&#x20;

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

## 2. Tạo mới **Rate Limit Token**

1. **Limit by** (chọn một hoặc cả hai):

* **Requests**: giới hạn theo số lượng request.
  * Số lượng request tối đa trong khoảng thời gian định sẵn.
  * Ví dụ: `1,000,000 Requests / 1 Minute`.
* **Tokens**: giới hạn theo số lượng token.
* **Giới hạn Request**
  *
* **Giới hạn Token**
  * Tổng số token input/output tối đa trong khoảng thời gian định sẵn.
  * Ví dụ: `5,000,000,000 Tokens / 1 Minute`.
* Nhấn **Tạo mã thông báo xác thực** để lưu cấu hình.

