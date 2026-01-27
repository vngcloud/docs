# Lịch phát hành phiên bản

Trang này liệt kê các ngày phát hành và ngày kết thúc hỗ trợ cho các phiên bản Kubernetes trên VKS (VNGCloud Kubernetes Service).

## Tổng quan về Kênh phát hành

VKS cung cấp các kênh phát hành sau để quản lý vòng đời phiên bản Kubernetes:

<table><thead><tr><th width="189">Kênh phát hành</th><th>Mô tả</th></tr></thead><tbody><tr><td><strong>Rapid</strong></td><td>Phiên bản mới nhất, dành cho môi trường thử nghiệm và người dùng sớm.</td></tr><tr><td><strong>Stable</strong></td><td>Phiên bản ổn định, được khuyến nghị cho môi trường production.</td></tr><tr><td><strong>Extended</strong></td><td>Kéo dài thời gian hỗ trợ cho các phiên bản cũ hơn.</td></tr></tbody></table>

## Lịch phát hành phiên bản

Bảng bên dưới hiển thị lịch phát hành và thời gian hỗ trợ cho các phiên bản Kubernetes trên VKS. Các bản patch của một phiên bản sẽ tiếp tục khả dụng cho đến khi **kết thúc hỗ trợ tiêu chuẩn**, ngoại trừ các cluster sử dụng **kênh Extended** - nơi phiên bản và các bản patch của nó sẽ tiếp tục khả dụng cho đến khi **kết thúc hỗ trợ mở rộng**.

{% hint style="warning" %}
**Lưu ý:** Các ngày trong bảng là dự đoán tốt nhất và được cập nhật định kỳ khi có thông tin mới.
{% endhint %}

{% hint style="info" %}
**Chú thích:**

* **Khả dụng (Available)**: Ngày phiên bản có thể được sử dụng để tạo cluster mới.
* **\***: Phiên bản hiện đang được hỗ trợ trên VKS.
{% endhint %}

| Phiên bản     | Rapid Khả dụng | Stable Khả dụng | Kết thúc hỗ trợ tiêu chuẩn | Kết thúc hỗ trợ mở rộng |
| --------------- | ---------------- | ----------------- | -------------------------------- | ----------------------------- |
| **1.27**  | 17/04/2024       | 26/08/2024        | 12/05/2025                       | -                             |
| **1.28**  | 17/04/2024       | 26/08/2024        | 24/11/2025                       | -                             |
| **1.29*** | 17/04/2024       | 20/02/2025        | 05/2026                          | 11/2026                       |
| **1.30*** | 02/01/2025       | 22/05/2025        | 05/2027                          | 11/2027                       |
| **1.31**  | 03/2026          | 05/2026           | 05/2028                          | 11/2028                       |
| **1.32**  | 03/2026          | 06/2026           | 05/2029                          | 11/2029                       |
| **1.33**  | 05/2026          | 11/2026           | 05/2030                          | 11/2030                       |

{% hint style="warning" %}
**Lưu ý:** Sau thời gian **Kết thúc hỗ trợ tiêu chuẩn**, VKS sẽ tiến hành force upgrade từng cluster còn ở phiên bản cũ lên phiên bản được hỗ trợ tiếp theo. Khách hàng cần extended support vui lòng [liên hệ chúng tôi](https://vngcloud.vn/contact) để được tư vấn và hỗ trợ.
{% endhint %}

## Các giai đoạn dự đoán lịch phát hành

Các ngày trong lịch phát hành thường trải qua các giai đoạn sau, với mức độ chi tiết và chắc chắn tăng dần:

<table><thead><tr><th width="230">Giai đoạn</th><th>Mô tả</th></tr></thead><tbody><tr><td><strong>Chưa xác định (TBD)</strong></td><td>Khi một mục được đánh dấu là "TBD" (To Be Determined), ngày đó chưa được xác định.</td></tr><tr><td><strong>Dự đoán theo tháng hoặc quý</strong></td><td>Các ngày chỉ có tháng (ví dụ: 2025-03) hoặc quý (ví dụ: 2025-Q3) là các giá trị ước tính sẽ được cập nhật khi biết ngày cụ thể. Ngày được cập nhật từ dự đoán theo quý sang theo tháng khi ngày ước tính còn dưới ba tháng.</td></tr><tr><td><strong>Dự đoán theo ngày</strong></td><td>Các ngày <em>in nghiêng</em> với độ chi tiết theo ngày được cung cấp khi dự đoán theo tháng còn dưới 14 ngày kể từ lần cập nhật gần nhất của bảng lịch phát hành, nhưng ngày cụ thể vẫn chưa được xác định. Các ngày in nghiêng này là ước tính và sẽ được cập nhật khi biết ngày cụ thể.</td></tr><tr><td><strong>Ngày cụ thể</strong></td><td>Các ngày không in nghiêng là dự đoán tốt nhất, thể hiện mức độ chắc chắn cao nhất trong lịch phát hành.</td></tr></tbody></table>

## Chính sách hỗ trợ phiên bản

VKS tuân theo các nguyên tắc sau trong việc hỗ trợ phiên bản Kubernetes:

1. **Phiên bản mới**: Các phiên bản Kubernetes mới sẽ được phát hành đầu tiên trong **kênh Rapid** để người dùng có thể thử nghiệm trước khi chuyển sang **kênh Stable**.
2. **Thời gian hỗ trợ**: Mỗi phiên bản của Kubernetes sẽ được hỗ trợ trong một khoảng thời gian nhất định. Sau thời gian này, phiên bản sẽ được đánh dấu là ngừng hỗ trợ.
3. **Kết thúc hỗ trợ tiêu chuẩn**: Khi một phiên bản hết hạn hỗ trợ:
   * Người dùng sẽ không thể tạo cluster/node group mới với phiên bản đó.
   * Các cluster hiện có sẽ được tự động nâng cấp lên phiên bản được hỗ trợ tiếp theo.
4. **Khuyến nghị**: Để đảm bảo tính ổn định và bảo mật, chúng tôi khuyến nghị người dùng chủ động nâng cấp cluster lên phiên bản mới trước khi phiên bản hiện tại hết hạn hỗ trợ.

## Tài liệu liên quan

* [Release Notes](release-notes.md) - Xem chi tiết các cập nhật và tính năng mới của VKS.
* [Nâng cấp phiên bản Kubernetes](../upgrade-kubernetes-version/) - Hướng dẫn nâng cấp phiên bản Kubernetes cho cluster.
* [Tự động nâng cấp](../upgrade-kubernetes-version/automatically-upgrade.md) - Tìm hiểu về tính năng tự động nâng cấp phiên bản Kubernetes.
* [Nâng cấp thủ công](../upgrade-kubernetes-version/manually-upgrade.md) - Hướng dẫn nâng cấp phiên bản Kubernetes thủ công.
