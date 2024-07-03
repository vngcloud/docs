# Stop POC

Trước khi tìm hiểu cách Stop POC cho tài nguyên của bạn trên VKS, bạn nên hiểu rõ các khái niệm cũng các hành động mà bạn có thể thao tác đối với tài nguyên POC. Chi tiết tham khảo thêm [tại đây](https://docs.vngcloud.vn/vng-cloud-document/v/vn/quan-ly-hoa-don-chi-phi-and-tai-nguyen-tren-vng-cloud/trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/quan-ly-vong-doi-tai-nguyen/tai-nguyen-poc).&#x20;

**Trong trường hợp người dùng dừng POC trước thời hạn kết thúc tài nguyên POC, hệ thống sẽ:**

* Tiến hành hoàn phí sử dụng tài nguyên POC còn lại (nếu có) vào ví POC.

**Để tiếp tục sử dụng tài nguyên vừa dừng POC như một tài nguyên bình thường (với mục đích giữ nguyên cấu hình), người dùng có thể thực hiện:**&#x20;

**Bước 1:** Truy cập vào [VKS Portal](https://vks.console.vngcloud.vn/k8s-cluster), chọn Cluster mà bạn muốn Stop POC.

**Bước 2:** Chọn nút **Stop POC** phía trên góc phải màn hình.

<figure><img src="../../.gitbook/assets/image (517).png" alt=""><figcaption></figcaption></figure>

**Bước 3:** Lúc này, màn hình hiển thị danh sách tất cả các Server và Volume thuộc Cluster đang có trạng thái POC. Bạn có thể kiểm tra thông tin sau đó chọn **Stop POC**

<figure><img src="../../.gitbook/assets/image (518).png" alt=""><figcaption></figcaption></figure>

**Bước 4**: Tiến hành thanh toán tài nguyên bằng tiền thật, bạn có thể lựa chọn **Chu kỳ sử dụng mong muốn, bật tắt Tự động gia hạn, nhập Coupon** nếu có và chọn **Continue** để thực hiện Thanh toán tài nguyên

<figure><img src="../../.gitbook/assets/image (519).png" alt=""><figcaption></figcaption></figure>

**Bước 5**: Thực hiện thanh toán bằng số dư credit hoặc qua các hình thức thanh toán khác nếu có.

<figure><img src="../../.gitbook/assets/image (520).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Chú ý:**&#x20;

* Để đảm bảo VKS hoạt động chính xác, việc thực hiện Stop POC cần được tiến hành trên VKS Portal thay vì thực hiện riêng lẻ trên từng resource server hoặc volume trên vServer Portal. Nếu bạn đã thực hiện stop POC riêng lẻ cho từng resource trên vServer Portal trước đó, bạn vẫn cần thực hiện Stop POC cho Cluster tại VKS Portal theo hướng dẫn bên trên.
* Sau khi stop POC trên VKS, nút "Stop POC" sẽ tiếp tục hiển thị nếu vẫn còn resource chưa được Stop POC sau khi thực hiện trên VKS Portal. Bạn có thể tiếp tục chọn và thực hiện Stop POC cho đến khi tất cả các resource được chuyển về resource thật.
{% endhint %}
