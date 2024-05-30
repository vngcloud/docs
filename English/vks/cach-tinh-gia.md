# Pricing

Đối với VKS chi phí **Managed Control Plane là hoàn toàn miễn phí.** Bạn chỉ cần chi trả cho các resource khác mà thực tế bạn sử dụng bao gồm:&#x20;

* Tất cả các node có trong Cluster (VM). Chi tiết cách tính giá của vServer bạn có thể tham khảo thêm tại [đây](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/cach-tinh-gia-vserver).
* Load Balancer được integrated vào Cluster của bạn. Chi tiết cách tính giá của Load Balancer bạn có thể tham khảo thêm tại [đây](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/cach-tinh-gia-vserver).
* Persistent Volume, Snapshot được integrated vào Cluster của bạn. Chi tiết cách tính giá của Volume bạn có thể tham khảo tại [đây](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/cach-tinh-gia-vserver).

{% hint style="info" %}
**Chú ý:**

* Để đảm bảo Cluster của bạn hoạt động ổn định, chúng tôi đã tự động thiết lập Auto-renew cho tất cả các resource trên Cluster của bạn. Trước ngày hết hạn của các resource, hãy đảm bảo số dư credit của bạn đủ để hệ thống có thể thực hiện Auto-renew thành công.
{% endhint %}
