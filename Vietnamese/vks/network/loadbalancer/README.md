# Load Balancer

## NLB là gì?

### Tổng quan

* **Network Load Balancer (NLB)** là bộ cân bằng tải được cung cấp bởi VNG Cloud giúp phân phối lưu lượng mạng đến nhiều máy chủ backend trong một nhóm máy tính (instance group). NLB hoạt động ở tầng 4 của mô hình OSI, cung cấp cân bằng tải dựa trên địa chỉ IP và cổng TCP/UDP. Để biết thông tin chi tiết hơn về NLB, vui lòng tham khảo \[Cách hoạt động (NLB)]

### Mô hình triển khai

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FVYBtJjEoUNgDi1f5J9vL%252Fimage.png%3Falt%3Dmedia%26token%3D554a2d62-320e-48d1-a884-3c7cce589071&width=768&dpr=4&quality=100&sign=d7f786ac&sv=1" alt=""><figcaption></figcaption></figure>

## ALB là gì?

### Tổng quan

* **Application Load Balancer (ALB)** là một công cụ trong hạ tầng mạng và máy chủ được sử dụng để phân phối lưu lượng mạng đến nhiều máy chủ hoặc máy ảo nhằm cải thiện hiệu suất và tính khả dụng của ứng dụng. ALB hoạt động ở tầng ứng dụng, cho phép phân phối lưu lượng dựa trên nhiều yếu tố như loại yêu cầu, trạng thái máy chủ và thuật toán phân phối tải. ALB cung cấp khả năng định tuyến nâng cao, cho phép điều hướng lưu lượng dựa trên Host hoặc Path Header. ALB cũng hỗ trợ tính năng session persistence, giúp duy trì phiên làm việc của người dùng tới cùng một máy chủ. Điều này hữu ích cho các ứng dụng yêu cầu tính nhất quán trong tương tác của người dùng. Để biết thêm thông tin về ALB, vui lòng tham khảo \[Cách hoạt động (ALB)]

### Mô hình triển khai

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## VNG Cloud LoadBalancer Controller

VNG Cloud Load Balancer Controller đơn giản hóa việc triển khai và quản lý bộ cân bằng tải trong môi trường VNG Cloud cho các cụm Kubernetes. Controller tự động hóa việc tạo, cấu hình và quản lý vòng đời của bộ cân bằng tải cho các dịch vụ Kubernetes và tài nguyên ingress. Controller đảm bảo tích hợp liền mạch với các dịch vụ VNG Cloud, cho phép cân bằng tải động, kết thúc SSL và định tuyến lưu lượng hiệu quả. Controller liên tục giám sát và đồng bộ tài nguyên để duy trì trạng thái mong muốn, đảm bảo tính khả dụng cao, khả năng mở rộng và hiệu suất tối ưu cho các ứng dụng chạy trên VNG Cloud.

### Cài đặt

#### Tạo Service Account và cài đặt VNG Cloud LoadBalancer Controller

* Tạo hoặc sử dụng **service account** đã tạo trên IAM và gắn policy: **vLBFullAccess**, **vServerFullAccess**. Để tạo service account, truy cập [tại đây](https://iam.console.vngcloud.vn/service-accounts) và thực hiện theo các bước sau:
  * Chọn "**Create a Service Account**", nhập tên cho Service Account và nhấn **Next Step** để gán quyền cho Service Account
  * Tìm và chọn **Policy: vLBFullAccess và Policy: vServerFullAccess**, sau đó nhấn "**Create a Service Account**" để tạo Service Account, Policy: vLBFullAccess và Policy: vServerFullAccess được tạo bởi VNG Cloud, bạn không thể xoá các policy này.
  * Sau khi tạo thành công, bạn cần lưu lại **Client\_ID** và **Secret\_Key** của Service Account để thực hiện bước tiếp theo.

#### Cài đặt VNG Cloud LoadBalancer Controller

* Cài đặt Helm phiên bản 3.0 trở lên. Tham khảo [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/) để biết cách cài đặt.
* Thay thế thông tin ClientID và Client Secret của bạn và chạy lệnh sau:

```bash
helm install vngcloud-load-balancer-controller oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/vngcloud-load-balancer-controller \
  --namespace kube-system \
  --set mysecret.global.clientID= __________________ \
  --set mysecret.global.clientSecret= __________________
```

* Sau khi cài đặt hoàn tất, kiểm tra trạng thái của pod:

```bash
kubectl -n kube-system get pod -l app.kubernetes.io/name=vngcloud-load-balancer-controller
```

Ví dụ, trong hình dưới đây bạn đã cài đặt thành công vngcloud-controller-manager:

```bash
NAME                                                              READY   STATUS    RESTARTS   AGE
vngcloud-load-balancer-controller-1736217866-manager-77599vrxpz   1/1     Running   0          4h24m
```
