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

#### Cơ chế Auto Healing: hệ thống VKS tự động phục hồi node gặp sự cố

Hệ thống VKS được trang bị cơ chế **Auto Healing** giúp tự động phát hiện, cô lập và thay thế các node gặp sự cố để đảm bảo cụm luôn duy trì trạng thái hoạt động ổn định.

Khi một node liên tục báo trạng thái **NotReady** trong khoảng thời gian **10 phút**, hệ thống sẽ tự động kích hoạt quy trình auto healing gồm 2 bước:

* **Bước 1:** Hệ thống thực hiện **drain node**, di chuyển toàn bộ pod đang chạy trên node lỗi sang các node khác trong cùng nhóm trước khi loại bỏ node đó khỏi cluster.
* **Bước 2:** Hệ thống **tự động tạo node mới** với cấu hình tương tự và join trở lại cụm. Nếu node mới chưa hoạt động bình thường, quy trình sẽ tiếp tục được thực hiện cho đến khi cụm ổn định.

Để đảm bảo an toàn cho toàn bộ hệ thống, cơ chế auto healing chỉ xử lý **một số lượng giới hạn node cùng lúc**, giúp tránh tình huống thay thế hàng loạt gây ảnh hưởng đến khả năng vận hành của cụm.

<table><thead><tr><th width="191.6640625">Quy mô cụm</th><th width="263.83984375">Số lượng node có thể phục hồi đồng thời</th><th>Ghi chú</th></tr></thead><tbody><tr><td>Small (1–5 node)</td><td>1 node</td><td>Đảm bảo cụm nhỏ vẫn duy trì ổn định.</td></tr><tr><td>Medium (6–20 node)</td><td>Khoảng 20% tổng số node</td><td>Cân bằng giữa tốc độ và an toàn.</td></tr><tr><td>Large (21–100 node)</td><td>Khoảng 10%</td><td>Phù hợp cho cụm lớn, hạn chế ảnh hưởng lan rộng.</td></tr><tr><td>Very Large (>100 node)</td><td>Khoảng 5%</td><td>Tối đa hóa độ sẵn sàng và ổn định.</td></tr></tbody></table>

Nhờ cơ chế này, VKS có thể **tự động phát hiện – khôi phục nhanh – đảm bảo tính sẵn sàng cao**, giúp khách hàng yên tâm về **độ tin cậy và khả năng tự phục hồi của hệ thống**.

{% hint style="info" %}
**Chú ý:**

* Khi hệ thống thực hiện Auto Healing, việc tạo ra node mới có thể gặp lỗi nếu bạn không có đủ credit hoặc bạn đã hết quota để tạo VM trên hệ thống vServer. Lúc này, mỗi 30 phút thì hệ thống sẽ thực hiện khởi động lại node cho đến khi node trở lại trạng thái hoạt động bình thường. Để tránh gặp lỗi bên trên, bạn cần:
  * **Đảm bảo bạn có đủ credit:** Nếu bạn là người dùng trả trước, hãy nạp thêm credit vào tài khoản của bạn.
  * **Yêu cầu tăng quota:** Bạn có thể yêu cầu tăng quota cho tài khoản của mình tại [đây](https://hcm-3.console.vngcloud.vn/vserver/limit).
{% endhint %}

***

### Bật Auto Healing

Hiện tại, tính năng Auto Healing được apply cho mỗi Node Group và luôn luôn ở trạng thái **bật**. Bạn không cần thao tác bật thủ công khi khởi tạo Cluster cũng như Node Group.
