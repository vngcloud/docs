# Lịch phát hành phiên bản VKS

Trang này liệt kê các ngày phát hành và ngày kết thúc hỗ trợ cho các phiên bản Kubernetes trên VKS (VNGCloud Kubernetes Service).

## Tổng quan về Release Channel

VKS cung cấp các release channel sau để quản lý vòng đời phiên bản Kubernetes:

| Release Channel    | Mô tả                                                                         |
| ------------------ | ------------------------------------------------------------------------------- |
| **Rapid**    | Phiên bản mới nhất, dành cho môi trường thử nghiệm và early adopter. |
| **Stable**   | Phiên bản ổn định, được khuyến nghị cho môi trường production.     |
| **Extended** | Kéo dài thời gian hỗ trợ cho các phiên bản cũ hơn.                    |

## Lịch phát hành phiên bản

VKS tự động nâng cấp các cluster vào hoặc sau các ngày được chỉ định trong cột **Auto Upgrade** của bảng lịch trình bên dưới. Các bản patch của một phiên bản minor sẽ tiếp tục khả dụng cho đến khi **kết thúc hỗ trợ tiêu chuẩn**, ngoại trừ các cluster sử dụng **Extended channel** - nơi phiên bản minor và các bản patch của nó sẽ tiếp tục khả dụng cho đến khi **kết thúc hỗ trợ mở rộng**.

{% hint style="warning" %}
**Lưu ý:** Các ngày trong bảng là dự đoán tốt nhất và được cập nhật định kỳ khi có thông tin mới.
{% endhint %}

{% hint style="info" %}
**Chú thích:**

* **Available**: Ngày phiên bản có thể được sử dụng để tạo cluster mới.
* **Auto Upgrade**: Ngày hệ thống bắt đầu tự động nâng cấp các cluster lên phiên bản tiếp theo.
{% endhint %}

<table>
  <thead>
    <tr>
      <th rowspan="2">Phiên bản</th>
      <th colspan="2" style="text-align:center">Rapid</th>
      <th colspan="2" style="text-align:center">Stable</th>
      <th colspan="2" style="text-align:center">Extended</th>
      <th rowspan="2">Kết thúc hỗ trợ tiêu chuẩn</th>
      <th rowspan="2">Kết thúc hỗ trợ mở rộng</th>
    </tr>
    <tr>
      <th>Available</th>
      <th>Auto Upgrade</th>
      <th>Available</th>
      <th>Auto Upgrade (Deprecated)</th>
      <th>Available</th>
      <th>Auto Upgrade (End of support)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>1.27</strong></td>
      <td>17/04/2024</td>
      <td>25/04/2025</td>
      <td>26/08/2024</td>
      <td>25/04/2025</td>
      <td>12/05/2025</td>
      <td>-</td>
      <td>12/05/2025</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>1.28</strong></td>
      <td>17/04/2024</td>
      <td>10/11/2025</td>
      <td>26/08/2024</td>
      <td>10/11/2025</td>
      <td>24/11/2025</td>
      <td>-</td>
      <td>24/11/2025</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>1.29</strong></td>
      <td>17/04/2024</td>
      <td>20/02/2025</td>
      <td>20/02/2025</td>
      <td>03/2026</td>
      <td>03/2026</td>
      <td>09/2026</td>
      <td>03/2026</td>
      <td>09/2026</td>
    </tr>
    <tr>
      <td><strong>1.30</strong></td>
      <td>02/01/2025</td>
      <td>22/05/2025</td>
      <td>22/05/2025</td>
      <td>03/2027</td>
      <td>03/2027</td>
      <td>09/2027</td>
      <td>03/2027</td>
      <td>09/2027</td>
    </tr>
    <tr>
      <td><strong>1.31</strong></td>
      <td>03/2026</td>
      <td>05/2026</td>
      <td>05/2026</td>
      <td>03/2028</td>
      <td>03/2028</td>
      <td>09/2028</td>
      <td>03/2028</td>
      <td>09/2028</td>
    </tr>
    <tr>
      <td><strong>1.32</strong></td>
      <td>03/2026</td>
      <td>06/2026</td>
      <td>06/2026</td>
      <td>03/2029</td>
      <td>03/2029</td>
      <td>09/2029</td>
      <td>03/2029</td>
      <td>09/2029</td>
    </tr>
    <tr>
      <td><strong>1.33</strong></td>
      <td>05/2026</td>
      <td>11/2026</td>
      <td>11/2026</td>
      <td>03/2030</td>
      <td>03/2030</td>
      <td>09/2030</td>
      <td>03/2030</td>
      <td>09/2030</td>
    </tr>
  </tbody>
</table>

## Các giai đoạn dự đoán lịch phát hành

Các ngày trong lịch phát hành thường trải qua các giai đoạn sau, với mức độ chi tiết và chắc chắn tăng dần:

| Giai đoạn                                 | Mô tả                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **TBD**                               | Khi một mục được đánh dấu là "TBD", ngày đó chưa được xác định.                                                                                                                                                                                                                                                                   |
| **Dự đoán theo tháng hoặc quý** | Các ngày chỉ có tháng (ví dụ: 2025-03) hoặc quý (ví dụ: 2025-Q3) là các giá trị ước tính sẽ được cập nhật khi biết ngày cụ thể. Ngày được cập nhật từ dự đoán theo quý sang theo tháng khi ngày ước tính còn dưới ba tháng.                                                                          |
| **Dự đoán theo ngày**             | Các ngày *in nghiêng* với độ chi tiết theo ngày được cung cấp khi dự đoán theo tháng còn dưới 14 ngày kể từ lần cập nhật gần nhất của bảng lịch phát hành, nhưng ngày cụ thể vẫn chưa được xác định. Các ngày in nghiêng này là ước tính và sẽ được cập nhật khi biết ngày cụ thể. |
| **Ngày cụ thể**                    | Các ngày không in nghiêng là dự đoán tốt nhất, thể hiện mức độ chắc chắn cao nhất trong lịch phát hành.                                                                                                                                                                                                                         |

## Chính sách hỗ trợ phiên bản

VKS tuân theo các nguyên tắc sau trong việc hỗ trợ phiên bản Kubernetes:

1. **Phiên bản mới**: Các phiên bản Kubernetes mới sẽ được phát hành đầu tiên trong **Rapid channel** để người dùng có thể thử nghiệm trước khi chuyển sang **Stable channel**.
2. **Thời gian hỗ trợ**: Mỗi phiên bản minor của Kubernetes sẽ được hỗ trợ trong một khoảng thời gian nhất định. Sau thời gian này, phiên bản sẽ được đánh dấu là ngừng hỗ trợ.
3. **Tự động nâng cấp**: Khi một phiên bản hết hạn hỗ trợ:

   * Người dùng sẽ không thể tạo cluster/node group mới với phiên bản đó.
   * Các cluster hiện có sẽ được tự động nâng cấp lên phiên bản được hỗ trợ tiếp theo.
4. **Khuyến nghị**: Để đảm bảo tính ổn định và bảo mật, chúng tôi khuyến nghị người dùng chủ động nâng cấp cluster lên phiên bản mới trước khi phiên bản hiện tại hết hạn hỗ trợ.

## Tài liệu liên quan

* [Release Notes](release-notes.md) - Xem chi tiết các cập nhật và tính năng mới của VKS.
* [Nâng cấp phiên bản Kubernetes](../cluster/upgrade-cluster-voi-zero-downtime.md) - Hướng dẫn nâng cấp phiên bản Kubernetes cho cluster.
* [Tự động nâng cấp](../upgrade-kubernetes-version/automatically-upgrade.md) - Tìm hiểu về tính năng tự động nâng cấp phiên bản Kubernetes.
* [Nâng cấp thủ công](../upgrade-kubernetes-version/manually-upgrade.md) - Hướng dẫn nâng cấp phiên bản Kubernetes thủ công.
