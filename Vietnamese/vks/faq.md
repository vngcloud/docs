# FAQ

### 1. Phần rotation log container trên VKS hiện tại đang được thiết lập như thế nào?

Trên VKS, log của container được rotate theo mặc định với cấu hình:

* `max-size`: 10Mi (mỗi file log tối đa 10MB)
* `max-file`: 5 (giữ lại 5 file log)

Chi tiết vui lòng xem thêm tại: [https://kubernetes.io/docs/concepts/cluster-administration/logging/#log-rotation](https://kubernetes.io/docs/concepts/cluster-administration/logging/#log-rotation)

### 2. IngressClassName: vngcloud trên VKS có hỗ trợ annotations: basic-auth để cấu hình Basic Auth chặn truy cập từ bên ngoài không?

Hiện tại VKS chưa hỗ trợ Basic Auth qua annotation trên Ingress. Bạn chỉ có thể chặn truy cập bằng cách cấu hình IP whitelist trên Load Balancer.

### 3. Dùng APISIX Ingress Controller có lấy được real client IP không?

Được. Bạn có thể bật Proxy Protocol trong APISIX:

* **Bước 1**: Cấu hình trong ConfigMap APISIX:

```yaml
apisix:
  proxy_protocol:
    listen_http_port: 80
    listen_https_port: 443
  enable_tcp_pp: true

nginx_config:
  http:
    real_ip_header: proxy_protocol
```

* **Bước 2**: Bật proxy protocol trong LB theo tài liệu sau:\
  [https://docs.vngcloud.vn/vng-cloud-document/vn/vks/bat-dau-voi-vks/expose-mot-service-thong-qua-vlb-layer4/preserve-source-ip-khi-su-dung-vlb-layer4-va-nginx-ingress-controller#cau-hinh-vlb-layer-4](https://docs.vngcloud.vn/vng-cloud-document/vn/vks/bat-dau-voi-vks/expose-mot-service-thong-qua-vlb-layer4/preserve-source-ip-khi-su-dung-vlb-layer4-va-nginx-ingress-controller#cau-hinh-vlb-layer-4)

Sau khi cấu hình xong, header `X-Real-IP` sẽ cho biết real IP client.

### 4. Có thể thay đổi reclaimPolicy của StorageClass bằng cách xóa và tạo lại không?

* **PVC/PV đã tạo** sẽ **không bị ảnh hưởng** khi StorageClass bị xóa.
* Tuy nhiên, reclaimPolicy của chúng sẽ **không thay đổi**.
* Muốn thay đổi reclaimPolicy:
  * Tạo StorageClass mới.
  * Tạo lại PVC dùng StorageClass mới.

### 5. Dùng Terraform scale node trong khi bật autoscaling có hợp lý không?

* Nên **tắt autoscaling** nếu dùng Terraform để tránh xung đột.
* Chỉ dùng Terraform khi cần kiểm soát chặt node count.

### 6. Node Group full CPU thì nên xử lý ra sao?

* Scale thêm node nếu còn trong max size.
* Tạo Node Group mới, move workload.
* Hoặc đổi flavor node bằng cách:
  * Tạo Node Group mới.
  * Drain Node cũ.
  * Hệ thống sẽ move pod sang Node Group mới.

### 7. VKS đang dùng cgroup v2?

Đúng, hiện tại các node worker trên VKS đã dùng cgroup v2.

### 8. VKS có cho phép đổi tên cluster không?

Hiện tại **không hỗ trợ đổi tên cluster** sau khi tạo. Muốn đổi tên, cần tạo cluster mới.

### 9. VKS có hoạt động được với VLB auto-scale không?

Có. Cần thêm annotation sau:

```yaml
annotations:
  vks.vngcloud.vn/enable-autoscale: "true"
```

Chi tiết vui lòng xem thêm tại: [https://docs.vngcloud.vn/vng-cloud-document/vn/vks/network/auto-scaling](https://docs.vngcloud.vn/vng-cloud-document/vn/vks/network/auto-scaling)

### 10. VKS private cluster tại region HAN có hỗ trợ không?

Có, nhưng nếu bạn tạo VKS private cluster thông qua Terraform, bạn cần:

* Sửa lại URL API và provider về region HAN.
* Nên input đầy đủ image ID, flavor ID, disk type,... để tránh sai default value từ HCM.

### 11. Cluster upgrade policy hoạt động thế nào?

Upgrage trên VKS có 2 kiểu:

* Manually Upgrade là quá trình nâng cấp thủ công ngay lập tức theo chỉ định của bạn trên hệ thông VKS.
* Automatically Upgrade Cluster trên VKS là quá trình hệ thống VKS tự động nâng cấp cluster theo upgrade window mà bạn chỉ định, hoặc tự động nâng cấp nhằm cải thiện hiệu suất, bảo mật và khả năng tương thích của hệ thống.

Trước khi nâng cấp chúng tôi sẽ thông báo cho bạn qua email, tham khảo thêm tại link này. Chúng tôi sẽ thông báo qua email cho bạn trong trường hợp Automatic Upgrade. Chi tiết vui lòng xem thêm tại: [Upgrade Kubernetes Version](upgrade-kubernetes-version/).

### 12. Tạo resource với POC hoặc credit như thế nào?

* Để tạo resource với ví POC, đầu tiên bạn cần request tới VNG Cloud để chúng tôi cấp số dư ví POC cho bạn, lúc này khi tạo Cluster bạn sẽ thấy nút POC ở góc phải màn hình. Chọn option này và thực hiện thanh toán bằng ví POC. Chi tiết vui lòng xem thêm tại: [Khởi tạo một Cluster thông qua ví POC](bat-dau-voi-vks/khoi-tao-mot-cluster-thong-qua-vi-poc.md).
* Với credit, bạn thực hiện tạo resource và thực hiện thanh toán qua thẻ hoặc số dư credit. Chi tiết vui lòng xem thêm tại: [Khởi tạo một Public Cluster](bat-dau-voi-vks/khoi-tao-mot-public-cluster/) và [Khởi tạo một Private Cluster](bat-dau-voi-vks/khoi-tao-mot-private-cluster.md).

### 13. Stop POC và auto-renew node

* Stop POC: resource tạo bởi số dư ví POC sẽ có ngày hết hạn là ngày hết hạn ví POC. Trước thời gian hết hạn, có thể stop POC để đưa resource POC thành resource thật, cách thực hiện xem chi tiết tại \
  [POC và Stop POC.](clusters/stop-poc.md)
* Resource thường: vks tự động bật auto-renew để tránh lỗi gián đoạn dịch vụ ( ví dụ node bị xóa,...), VKS khuyến cáo nên bật option này và nạp sẵn credit trước thời hạn auto-renew tiếp theo.

### 14. Có disable auto-healing được không?

Không. Auto-healing đảm bảo High Availability cho hệ thống.

### 15. Dùng vMonitor log cho VKS thì nhiều cluster có thể dồn log về chung 1 project không?

Hoàn toàn có thể:

* Mỗi cluster 1 log project.
* Hoặc nhiều cluster chung 1 log project.

Khi search log, bạn có thể lọc theo cluster\_id.

### 16. Xóa cluster POC có được refund?

Có. Nếu ví POC còn hạn, khi xóa sẽ được refund lại số dư ví POC tương ứng.

### 17. Có tái sử dụng Load Balancer đã tạo trước không?

Có. Khi expose service qua ALB hoặc NLB, dùng annotation:

```yaml
vks.vngcloud.vn/load-balancer-id
```

Chi tiết vui lòng tham khảo thêm tại [https://docs.vngcloud.vn/vng-cloud-document/vn/vks/network/lam-viec-voi-application-load-balancer-alb/ingress-for-an-application-load-balancer](https://docs.vngcloud.vn/vng-cloud-document/vn/vks/network/lam-viec-voi-application-load-balancer-alb/ingress-for-an-application-load-balancer) hoặc [https://docs.vngcloud.vn/vng-cloud-document/vn/vks/network/lam-viec-voi-network-load-balancing-nlb/integrate-with-network-load-balancer](https://docs.vngcloud.vn/vng-cloud-document/vn/vks/network/lam-viec-voi-network-load-balancing-nlb/integrate-with-network-load-balancer)
