# Auto Healing

### Tổng quan

Trên hệ thống VKS, tính năng Auto Healing được apply cho mỗi Node Group và luôn luôn ở trạng thái bật. Việc bật tính năng tự phục hồi (self-healing) trong Kubernetes mang lại nhiều lợi ích quan trọng, giúp đảm bảo tính sẵn sàng và độ tin cậy cao cho ứng dụng của bạn.&#x20;

Tính năng Auto Healing có những điểm nổi bật sau:

* **Tự động phát hiện lỗi:** Kubernetes có thể tự động phát hiện các node bị lỗi hoặc gặp sự cố thông qua việc theo dõi trạng thái của các node. Một số dấu hiệu cho thấy node bị lỗi bao gồm: node báo cáo trạng thái "NotReady", node không thể ping được, node bị lỗi phần cứng, v.v.
* **Tự động khởi động lại node:** Khi một node bị phát hiện lỗi, Kubernetes sẽ tự động khởi động lại node. Việc khởi động lại node có thể giúp khắc phục các lỗi tạm thời và đưa node trở lại trạng thái hoạt động bình thường.
* **Giảm thiểu sự can thiệp thủ công:** Auto Healing giúp giảm thiểu sự can thiệp thủ công của người quản trị viên hệ thống, tiết kiệm thời gian và công sức.
* **Cải thiện hiệu quả hoạt động:** Auto Healing giúp cải thiện hiệu quả hoạt động của hệ thống bằng cách đảm bảo rằng các node luôn hoạt động bình thường.

***

### Cơ chế hoạt động

Hệ thống VKS được trang bị cơ chế **Auto Healing** giúp tự động phát hiện, cô lập và thay thế các node gặp sự cố, đảm bảo cụm luôn duy trì trạng thái hoạt động ổn định và sẵn sàng cao.

Khi một node liên tục báo trạng thái **NotReady** trong khoảng **10 phút**, hệ thống sẽ tự động kích hoạt quy trình phục hồi gồm hai bước:

* **Bước 1:** Hệ thống **drain node**, di chuyển toàn bộ pod đang chạy trên node lỗi sang các node khác trong cùng nhóm trước khi loại bỏ node đó khỏi cụm.
* **Bước 2:** Hệ thống **tự động tạo node mới** với cấu hình tương tự và join trở lại cluster. Nếu node mới vẫn chưa hoạt động bình thường, quy trình sẽ tiếp tục được thực hiện cho đến khi cụm ổn định.

Để đảm bảo an toàn cho toàn hệ thống, cơ chế auto healing chỉ xử lý **một số lượng giới hạn node cùng lúc**, nhằm tránh tình huống thay thế hàng loạt gây ảnh hưởng đến khả năng vận hành của cụm.

| Quy mô cụm             | Số lượng node có thể phục hồi đồng thời (khuyến nghị) | Ghi chú                                        |
| ---------------------- | ----------------------------------------------------- | ---------------------------------------------- |
| Small (1–5 node)       | 1 node                                                | Đảm bảo cụm nhỏ vẫn duy trì ổn định.           |
| Medium (6–20 node)     | Khoảng 20% tổng số node                               | Cân bằng giữa tốc độ và độ an toàn.            |
| Large (21–100 node)    | Khoảng 10%                                            | Phù hợp cho cụm lớn, tránh ảnh hưởng lan rộng. |
| Very Large (>100 node) | Khoảng 5%                                             | Đảm bảo độ sẵn sàng cao nhất.                  |

> **Chú ý:** Khi số node gặp sự cố vượt quá ngưỡng cho phép, hệ thống sẽ **tạm ngừng khôi phục thêm node mới** và chỉ tiếp tục quá trình phục hồi khi cụm có đủ số node khỏe để đảm bảo ổn định.

Nhờ cơ chế này, VKS có thể **tự động phát hiện – khôi phục nhanh – vận hành an toàn**, giúp khách hàng yên tâm về **tính ổn định và độ tin cậy của hạ tầng**.

{% hint style="info" %}
**Chú ý:**

* Khi hệ thống thực hiện Auto Healing, việc tạo ra node mới có thể gặp lỗi nếu bạn không có đủ credit hoặc bạn đã hết quota để tạo VM trên hệ thống vServer. Lúc này, mỗi 30 phút thì hệ thống sẽ thực hiện khởi động lại node cho đến khi node trở lại trạng thái hoạt động bình thường. Để tránh gặp lỗi bên trên, bạn cần:
  * **Đảm bảo bạn có đủ credit:** Nếu bạn là người dùng trả trước, hãy nạp thêm credit vào tài khoản của bạn.
  * **Yêu cầu tăng quota:** Bạn có thể yêu cầu tăng quota cho tài khoản của mình tại [đây](https://hcm-3.console.vngcloud.vn/vserver/limit).
{% endhint %}

***

### Bật Auto Healing

Hiện tại, tính năng Auto Healing được apply cho mỗi Node Group và luôn luôn ở trạng thái **bật**. Bạn không cần thao tác bật thủ công khi khởi tạo Cluster cũng như Node Group.
