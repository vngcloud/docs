---
description: >-
  Model Caching lưu trữ kết quả trả về từ model để tái sử dụng cho các request
  giống hoặc tương tự, giúp giảm độ trễ, tiết kiệm tài nguyên và tăng khả năng
  xử lý khi có nhiều request lặp lại.
---

# Caching

## 1. Truy cập trang Model Caching

Truy cập thông qua đường dẫn: [https://aigateway.console.vngcloud.vn/model-caching/list](https://aigateway.console.vngcloud.vn/model-caching/list)

## 2. Tạo một cấu hình **Caching**

* Truy cập trang **Model Caching** và nhấn nút **"Tạo một cấu hình Caching"** .

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

* Trong form **Tạo một cấu hình Caching**, điền các thông tin sau:
  * **Tên cấu hình** (bắt buộc)
    * Cho phép chữ thường, số và dấu `-` , độ dài từ 5 đến 50 ký tự.
  * **Kiểu Caching** (bắt buộc)\
    Chọn một trong hai hoặc cả hai:
    * **Exact caching**: chỉ trả về cache khi request trùng khớp hoàn toàn.
    * **Semantic caching**: trả về cache cho các request có ý nghĩa tương tự. Khi chọn loại này, hệ thống sẽ hiển thị thêm trường **Semantic Threshold** (0.0–1.0).
      * Giá trị cao (ví dụ 0.9): chỉ nhận cache khi rất giống.
      * Giá trị thấp (ví dụ 0.7): chấp nhận mức tương tự rộng hơn.
  * **Thời gian tồn tại (TTL)**\
    Nhập thời gian (tính bằng giây) mà response được lưu trong cache trước khi hết hạn.
    * TTL càng lớn thời gian lưu càng lâu nhưng dữ liệu dễ lỗi thời hơn, tối đa 172800 giấy tương đương 48 tiếng;
  * Cấu hình chính sách bộ đệm có thể bị ảnh hưởng hoặc bị ghi đè bởi tiêu đề HTTP trong yêu cầu của máy khách\
    Tiêu đề bộ đệm được hỗ trợ x-cache-control headers gồm:
    * no-cache: buộc AI Gateway bỏ qua bộ đệm hiện có và gửi yêu cầu mới đến mô hình.
    * no-store: ngăn AI Gateway lưu phản hồi vào bộ đệm.
    * max-age=\<second>: đặt TTL từ client AI Gateway sẽ sử dụng giá trị nhỏ hơn giữa giá trị này và TTL của nhà cung cấp.
* Sau khi điền đầy đủ, nhấn **Create** để lưu cấu hình.

<div data-full-width="false"><figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure></div>

## 3. Quản lý Caching (Edit / Manage models / Delete)

* Sau khi tạo, bạn sẽ thấy cấu hình mới trong danh sách .
* Ở cột **Action** (**⋮**), nhấn mở menu để chọn:
  * **Manage models** — gán gateway và model .
  * **Edit configuration** — chỉnh TTL / tên / loại cache.
  * **Delete** — xóa cấu hình

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (2) (1).png" alt=""><figcaption></figcaption></figure>

### Manage models (gán gateway và model).

* Gán một caching configuration cho gateway là áp dụng cấu hình đó cho tất cả các model bạn chọn ở gateway đó.
* Có thể gán cùng một config cho nhiều gateway hoặc nhiều config cho cùng một gateway. Nhưng một model của một gateway chỉ có config duy nhất.
* Nếu muốn gỡ, mở **Manage models** → remove gateway hoặc bỏ chọn các model → Save

#### Các bước gán gateway và model

1. Trong danh sách Model Caching, tại config cần gán, nhấn menu → **Manage models**
2. Hộp thoại **Manage models** hiện — nếu chưa có gateway nào được thêm, bạn sẽ thấy thông báo **No Gateway added** và nút **Add a gateway**.
3. Nhấn **Add a gateway** → dropdown liệt kê các gateway đã tạo → chọn 1 gateway. Bạn có thể thêm nhiều gateway nếu cần.

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

4. Sau khi thêm gateway, dưới mỗi gateway sẽ có mục **API models** với ô **Select models**. Click vào ô này để mở danh sách các model có trong gateway.

* Bạn có thể **chọn từng model** hoặc **Select all models** để áp dụng cache cho tất cả model trong gateway.
* Có ô Search để tìm model theo tên (vd: `gemini-1.5-pro`, `gpt-4o`...).

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

5. Sau khi chọn model xong, nhấn **Save** để lưu thay đổi.

#### Xem các cấu hình Caching đã gán cho một Gateway

1. Mở trang Gateway list: [https://aigateway.console.vngcloud.vn/ai-gateway/list](https://aigateway.console.vngcloud.vn/ai-gateway/list).
2. Chọn Gateway mong muốn → vào trang chi tiết Gateway.
3. Chọn tab **Model Caching** — sẽ hiển thị danh sách các cấu hình Caching đã gán cho gateway đó, kèm cột: **Caching type**, **Caching configuration** (TTL, semantic threshold), **Associated models.**
4. Từ đây bạn có thể truy cập nhanh cấu hình, biết model nào đang dùng cache nào.

<figure><img src="../../../.gitbook/assets/image (437).png" alt=""><figcaption></figcaption></figure>

### Edit Configuration (chỉnh TTL / tên / loại cache)

1. Trong danh sách cấu hình, tại cột **Action** (**⋮**) chọn **Edit Configuration** .
2. Cập nhật các thông số:
   * Input Caching Strategy (Exact ↔ Semantic).
   * TTL, Semantic Threshold.
   * Tên hoặc mô tả configuration.
3. Nhấn **Save changes** để lưu.

📌 Lưu ý: Việc chỉnh sửa sẽ áp dụng cho tất cả model/gateway đang sử dụng configuration đó

### Delete (xoá cấu hình)

1. Trên danh sách hình, tại cột **Action** (**⋮**) chọn **Delete**.
2. Xác nhận thao tác.

📌 Lưu ý: Chỉ xoá được khi cấu hình không còn được gán cho bất kỳ model/gateway nào. Nếu còn thì gỡ gán (detach model/gateway)

<figure><img src="../../../.gitbook/assets/image (8) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
