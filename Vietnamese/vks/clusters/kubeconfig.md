# Kubeconfig

**Kubeconfig** là file cấu hình cho phép công cụ `kubectl` xác thực và kết nối đến Kubernetes Cluster của bạn. Mỗi file kubeconfig chứa thông tin về cluster (địa chỉ API server), thông tin xác thực (client certificate), và ngữ cảnh (context) xác định cluster nào đang được sử dụng.

Trên VKS, file kubeconfig sử dụng cơ chế **Client Certificate** để xác thực. Bạn có thể chủ động chọn thời hạn hiệu lực của certificate khi tải xuống, giúp kiểm soát bảo mật tốt hơn.

***

## Tải xuống Kubeconfig

**Bước 1:** Truy cập vào [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Bước 2:** Tại màn hình **Overview**, chọn menu **Kubernetes Cluster.**

**Bước 3:** Tại Cluster cần lấy kubeconfig, chọn biểu tượng **Action** và chọn **Download Config File.**

**Bước 4:** Hệ thống hiển thị popup xác nhận. Tại đây, bạn chọn **thời hạn hiệu lực** của certificate trong kubeconfig:

| Thời hạn | Mô tả                                                                   |
| -------- | ----------------------------------------------------------------------- |
| 30 ngày  | Phù hợp cho môi trường staging, testing hoặc truy cập tạm thời          |
| 90 ngày  | Phù hợp cho môi trường production với chu kỳ rotate định kỳ             |
| 365 ngày | Phù hợp cho các trường hợp cần kubeconfig dài hạn, cần quản lý cẩn thận |

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
**Lưu ý về bảo mật:**

* File kubeconfig cấp quyền **cluster-admin** cho người sở hữu. Không chia sẻ file này với người không có thẩm quyền.
* Nếu cần **thu hồi certificate** trước thời hạn, vui lòng liên hệ đội ngũ hỗ trợ VKS để được xử lý.
* Nếu file kubeconfig bị lộ, hãy liên hệ đội ngũ hỗ trợ VKS để thực hiện xử lý kịp thời.
{% endhint %}

**Bước 5:** Chọn **Confirm** để tải xuống. File `config` sẽ được lưu về máy của bạn.

***

## Cấu hình kubectl sử dụng Kubeconfig

Sau khi tải xuống file kubeconfig, bạn cần đặt file vào đúng vị trí để `kubectl` nhận diện.

**Bước 1:** Tạo thư mục `.kube` nếu chưa có:

```bash
mkdir -p ~/.kube
```

**Bước 2:** Di chuyển file kubeconfig vừa tải về vào thư mục `.kube` và đặt tên là `config`:

```bash
mv <đường_dẫn_file_vừa_tải> ~/.kube/config
```

**Bước 3:** Kiểm tra kết nối đến Cluster:

```bash
kubectl get nodes
```

Nếu kết nối thành công, bạn sẽ thấy danh sách các node trong Cluster của mình.

{% hint style="info" %}
**Sử dụng nhiều Cluster cùng lúc:**

Nếu bạn cần quản lý nhiều Cluster, có thể đặt file kubeconfig ở vị trí khác và chỉ định đường dẫn khi chạy lệnh:

```bash
kubectl --kubeconfig <đường_dẫn_kubeconfig> get nodes
```

Hoặc thiết lập biến môi trường:

```bash
export KUBECONFIG=<đường_dẫn_kubeconfig>
```
{% endhint %}

***

## Quản lý thời hạn Certificate

### Xem thời hạn certificate hiện tại

**Cách 1: Xem trên Portal**

Khi nhấp **Download Config File** tại màn hình Kubernetes Cluster, hệ thống hiển thị popup thông tin kubeconfig, trong đó bao gồm thời hạn hiệu lực của certificate. Bạn có thể xem ngày hết hạn trực tiếp tại đây trước khi tải xuống.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

**Cách 2: Kiểm tra bằng lệnh**

Để kiểm tra thời hạn của certificate trong file kubeconfig đang sử dụng, chạy lệnh sau:

```bash
kubectl config view --raw -o jsonpath='{.users[0].user.client-certificate-data}' \
  | base64 --decode \
  | openssl x509 -noout -dates
```

Kết quả trả về sẽ hiển thị `notBefore` (ngày bắt đầu) và `notAfter` (ngày hết hạn) của certificate.

### Gia hạn (Renew) Certificate

Khi certificate sắp hết hạn (dưới 7 ngày), hệ thống VKS sẽ gửi thông báo đến bạn. Lúc này bạn có thể:

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

* **Tự động renew:** Hệ thống tự động gia hạn certificate nếu đủ điều kiện. Bạn sẽ nhận được thông báo xác nhận khi quá trình hoàn tất.
* **Thủ công renew:** Nếu hệ thống không thể tự động renew, bạn sẽ thấy nút **Renew** trong thông báo. Chọn **Renew** để hệ thống cấp lại certificate mới.

{% hint style="info" %}
**Chú ý:**

Sau khi renew, bạn cần tải xuống lại file kubeconfig mới và thay thế file cũ. Certificate vẫn sẽ hoạt động cho đến khi hết hạn sau khi đã renew.
{% endhint %}

### Tải xuống lại Kubeconfig mới

Thực hiện lại các bước trong mục [Tải xuống Kubeconfig](kubeconfig.md#tải-xuống-kubeconfig) để lấy file kubeconfig mới với certificate còn hiệu lực.

***

## Bảo mật Kubeconfig

Dưới đây là các khuyến nghị bảo mật khi sử dụng kubeconfig trên VKS:

* **Không commit file kubeconfig lên source code repository** (Git, GitLab...). Thêm `~/.kube/config` vào `.gitignore` của dự án.
*   **Giới hạn quyền truy cập file:** Đảm bảo chỉ user hiện tại có thể đọc file kubeconfig:

    ```bash
    chmod 600 ~/.kube/config
    ```
* **Chọn thời hạn certificate phù hợp:** Không nên sử dụng certificate 365 ngày cho tất cả trường hợp. Ưu tiên sử dụng 30 hoặc 90 ngày và thực hiện rotate định kỳ.

***

## Tạo Kubeconfig Read-only

Kubeconfig mặc định tải từ VKS cấp quyền **cluster-admin** — toàn quyền trên cluster. Nếu bạn cần cấp quyền cho người dùng khác (developer, auditor...) chỉ với quyền **xem** mà không có quyền chỉnh sửa, hãy tạo một kubeconfig riêng với quyền `view`.

Hướng dẫn dưới đây tạo kubeconfig read-only cho user `readonly-user`. Bạn có thể thay tên này theo nhu cầu thực tế.

### Bước 1 — Tạo private key và CSR

```bash
openssl genrsa -out readonly-user.key 2048
```

```bash
openssl req -new -key readonly-user.key -out readonly-user.csr -subj "/CN=readonly-user/O=read-only"
```

### Bước 2 — Tạo CertificateSigningRequest trong Kubernetes

**Bước 2a — Encode CSR sang base64**

```bash
CSR_BASE64=$(cat readonly-user.csr | base64 | tr -d '\n')
```

**Bước 2b — Tạo file YAML**

```bash
cat > csr.yaml <<EOF
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: readonly-user
spec:
  request: ${CSR_BASE64}
  signerName: kubernetes.io/kube-apiserver-client
  expirationSeconds: 31536000
  usages:
  - client auth
EOF
```

**Bước 2c — Apply file**

```bash
kubectl apply -f csr.yaml
```

### Bước 3 — Approve CSR

```bash
kubectl certificate approve readonly-user
```

### Bước 4 — Lấy certificate đã được ký

```bash
kubectl get csr readonly-user -o jsonpath='{.status.certificate}' | base64 -d > readonly-user.crt
```

### Bước 5 — Bind RBAC cho user

```bash
kubectl create clusterrolebinding readonly-user-binding \
  --clusterrole=view \
  --user=readonly-user
```

### Bước 6 — Tạo file kubeconfig

**Bước 6a — Lấy thông tin cluster**

```bash
CLUSTER_SERVER=$(kubectl config view --minify -o jsonpath='{.clusters[0].cluster.server}')
CLUSTER_CA=$(kubectl config view --minify --raw -o jsonpath='{.clusters[0].cluster.certificate-authority-data}')
CERT_DATA=$(cat readonly-user.crt | base64 | tr -d '\n')
KEY_DATA=$(cat readonly-user.key | base64 | tr -d '\n')
```

**Bước 6b — Tạo file kubeconfig**

```bash
cat > readonly-kubeconfig.yaml <<EOF
apiVersion: v1
kind: Config
clusters:
- cluster:
    certificate-authority-data: ${CLUSTER_CA}
    server: ${CLUSTER_SERVER}
  name: my-cluster
contexts:
- context:
    cluster: my-cluster
    user: readonly-user
  name: readonly-context
current-context: readonly-context
users:
- name: readonly-user
  user:
    client-certificate-data: ${CERT_DATA}
    client-key-data: ${KEY_DATA}
EOF
```

> User chỉ cần 1 file duy nhất là `readonly-kubeconfig.yaml`.

### Bước 7 — Xóa file tạm

```bash
rm readonly-user.key readonly-user.csr readonly-user.crt csr.yaml
```

{% hint style="warning" %}
File `.key` (private key) đã được nhúng vào `readonly-kubeconfig.yaml` dưới dạng `client-key-data`. Xóa file `.key` gốc để tránh rò rỉ private key.
{% endhint %}

### Bước 8 — Kiểm tra

```bash
# Kỳ vọng: danh sách pods được hiển thị bình thường
kubectl --kubeconfig=readonly-kubeconfig.yaml get pods -A
```

```bash
# Kỳ vọng: lệnh bị từ chối với lỗi Forbidden
kubectl --kubeconfig=readonly-kubeconfig.yaml delete pod some-pod
```

***

## Thu hồi quyền truy cập (Revoke)

### Xóa ClusterRoleBinding — bắt buộc

```bash
kubectl delete clusterrolebinding readonly-user-binding
```

Xóa ClusterRoleBinding → user **lập tức mất quyền truy cập**, dù certificate vẫn còn hạn.

### Xóa CSR — tùy chọn (dọn dẹp)

```bash
kubectl delete csr readonly-user
```

CSR chỉ là object lưu lịch sử quá trình ký certificate. Xóa CSR **không ảnh hưởng** đến certificate đã được ký — chỉ để tránh tồn đọng rác trong cluster.

{% hint style="info" %}
**Lưu ý quan trọng:**

Kubernetes **không có cơ chế revoke certificate**. Nếu user vẫn còn giữ file kubeconfig, certificate vẫn valid đến hết thời hạn. Xóa ClusterRoleBinding là cách duy nhất để chặn truy cập ngay lập tức.
{% endhint %}

{% hint style="warning" %}
**Khuyến nghị dành cho khách hàng:**

* **Không nên xóa ClusterRoleBinding** của cluster trừ khi bạn chắc chắn muốn thu hồi quyền truy cập vĩnh viễn.
* Nếu bạn **lỡ xóa ClusterRoleBinding** và không thể kết nối đến cluster, vui lòng **liên hệ đội ngũ hỗ trợ VKS** để được hỗ trợ tạo lại kubeconfig mới.
{% endhint %}

| Hành động            | Xóa ClusterRoleBinding | Xóa CSR  |
| -------------------- | ---------------------- | -------- |
| User mất quyền ngay? | **Có**                 | Không    |
| Mục đích             | Revoke quyền           | Dọn dẹp  |
| Bắt buộc?            | **Bắt buộc**           | Tùy chọn |
