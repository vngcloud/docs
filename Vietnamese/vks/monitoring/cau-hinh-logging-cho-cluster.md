# Cấu hình Logging cho Cluster

> Hướng dẫn bật Control Plane Logging cho Cluster VKS và đẩy log về OpenSearch hoặc Kafka của chính bạn trên vDB — bật ngay khi tạo Cluster, hoặc bật/tắt bất cứ lúc nào tại màn hình chi tiết Cluster.

---

## 1. Tổng quan

VKS là dịch vụ Kubernetes được quản lý (managed Kubernetes): các thành phần Control Plane — **kube-apiserver**, **kube-controller-manager**, **kube-scheduler** — chạy trên hạ tầng do VKS vận hành nên bạn không truy cập trực tiếp được. Vì vậy trước đây bạn không thể tự xem **audit log** (ai gọi API nào, lúc nào, kết quả ra sao) hay log của các thành phần Control Plane khi cần điều tra sự cố.

Tính năng **Logging configuration** cho phép bạn bật thu thập log Control Plane của từng Cluster và **giao log về hệ thống lưu trữ của chính bạn** — một **OpenSearch Cluster** hoặc một **Kafka Cluster** trên vDB. Log thuộc quyền sở hữu của bạn, được tách riêng theo từng tài khoản và từng Cluster.

Các trường hợp sử dụng phổ biến:

- Đáp ứng yêu cầu **audit / compliance**: lưu vết toàn bộ request gọi tới Kubernetes API.
- **Điều tra bảo mật**: truy vết ai đã tạo/sửa/xóa tài nguyên nào trong Cluster.
- **Debug sự cố Cluster**: đọc log apiserver, controller-manager, scheduler khi Pod không được xếp lịch, request bị từ chối, controller hoạt động bất thường.
- **Tích hợp vào hệ quan sát sẵn có**: đẩy log về Kafka để pipeline nội bộ của bạn tiêu thụ tiếp.

---

## 2. Điểm nổi bật

- **Bật/tắt bất cứ lúc nào.** Bật ngay tại bước tạo Cluster, hoặc vào chi tiết Cluster để bật/tắt sau. Khi tắt, tài nguyên thu thập log được dọn sạch và bạn không tốn tài nguyên cho phần này.
- **Chọn đúng loại log cần thiết.** Bật độc lập từng nguồn: **Audit**, **API Server**, **Controller Manager**, **Scheduler** — chỉ bật thứ bạn thực sự dùng để kiểm soát chi phí lưu trữ.
- **Log về đúng nơi bạn quản lý.** Đích nhận log (sink) là OpenSearch hoặc Kafka **của tài khoản bạn** trên vDB, dùng credential do bạn cấp.
- **Không mất log khi sink gián đoạn tạm thời.** Cơ chế giao log theo mô hình **at-least-once**: khi sink tạm ngừng phục vụ (bảo trì, mất kết nối, lỗi 5xx), log được giữ lại và giao bù sau khi sink phục hồi. Xem giới hạn của cơ chế này tại mục 7.
- **Cô lập theo Cluster.** Log của mỗi Cluster đi vào index/topic riêng theo tên `{user_id}_{cluster_id}_{component}` (xem mục 8), không lẫn giữa các Cluster hay giữa các tài khoản.

---

## 3. Điều kiện cần (Prerequisites)

{% hint style="info" %}
Tính năng hiện chỉ khả dụng tại **region HAN**. Nếu Cluster của bạn ở region khác, bước **Logging configuration** sẽ không hiển thị.
{% endhint %}

- Đã có tài khoản GreenNode và đã kích hoạt dịch vụ **VKS**.
- Đã tạo sink trên vDB, tùy loại bạn chọn:
  - **OpenSearch**: một [OpenSearch Cluster](../../vdb/opensearch-cluster-database-ods/) đang **ACTIVE**, kèm **Username** và **Password** có đủ quyền sau trên các index có tên bắt đầu bằng `{user_id}_{cluster_id}_`:
    - tạo index và ghi dữ liệu (`indices:admin/create`, `indices:data/write/bulk*`, `indices:data/write/index`);
    - Cách đơn giản nhất là dùng tài khoản admin của OpenSearch Cluster.
  - **Kafka**: một [Kafka Cluster](../../vdb/kafka-cluster-kds/) đang **ACTIVE** và bật public, kèm một [Kafka User](../../vdb/kafka-cluster-kds/quan-ly-kafka-cluster/quan-ly-kafka-user.md) có quyền **produce**. Kafka Cluster còn **quota topic** trống ít nhất bằng số nguồn log bạn bật (tối đa 4) — VKS sẽ tự tạo topic, xem mục 6.3.
- Cluster VKS và Cluster vDB dùng làm sink nằm trong cùng một tài khoản GreenNode.
- OpenSearch/Kafka Cluster đã bật **public endpoint** — VKS kết nối tới sink qua public endpoint của vDB.

{% hint style="info" %}
Chỉ những **Kafka User** có quyền produce (`produceAll` hoặc `produceConsumeAll`) mới xuất hiện trong danh sách chọn. Nếu không thấy user mong muốn, hãy cấp quyền produce cho user đó tại console vDB rồi nhấn biểu tượng làm mới trong form.
{% endhint %}

---

## 4. Bật Logging khi tạo Cluster mới

**Bước 1:** Truy cập [https://vks.console.greennode.ai/overview](https://vks.console.greennode.ai/overview), chọn menu **Kubernetes cluster** và nhấn **Create a Cluster**.

**Bước 2:** Khai báo các bước cấu hình Cluster như thông thường (Cluster Configuration, Node Group, Plugin).

**Bước 3:** Tại bước **Logging configuration (optional)**, bật công tắc **Enable control plane logging**.

<figure><img src="../../.gitbook/assets/Logging-config-cluster/create-cluster-enable-log.png" alt="Bước Logging configuration khi tạo Cluster"><figcaption><p>Bật Logging ngay tại bước tạo Cluster</p></figcaption></figure>

**Bước 4:** Tại khối **Log Sources**, chọn các thành phần Control Plane cần thu thập log: **Audit**, **API Server**, **Controller Manager**, **Scheduler**. Bạn có thể chọn một hoặc nhiều nguồn.

**Bước 5:** Tại khối **Log Destination**, chọn **Sink type** là **OpenSearch** hoặc **Kafka**, sau đó điền thông tin kết nối tương ứng (xem chi tiết từng trường tại mục 6 bên dưới).

**Bước 6:** Nếu **Sink type** là **OpenSearch**, nhấn **Test connection** để kiểm tra VKS kết nối và xác thực được tới sink của bạn. Form Kafka không có bước kiểm tra kết nối này — xem cách tự xác nhận tại mục 8.

**Bước 7:** Nhấn **Create Kubernetes cluster** để hoàn tất. Logging sẽ được kích hoạt cùng lúc với Cluster.

{% hint style="info" %}
Bước **Logging configuration** là tùy chọn. Nếu bạn bỏ qua, Cluster vẫn được tạo bình thường và bạn có thể bật logging bất cứ lúc nào sau đó theo hướng dẫn ở mục 5.
{% endhint %}

---

## 5. Bật hoặc tắt Logging cho Cluster đang chạy

**Bước 1:** Truy cập [https://vks.console.greennode.ai/overview](https://vks.console.greennode.ai/overview) và chọn menu **Kubernetes cluster**.

**Bước 2:** Chọn Cluster cần cấu hình để mở màn hình chi tiết, sau đó mở hộp thoại **Logging configuration**.

**Bước 3:** Bật hoặc tắt công tắc **Enable control plane logging**.

<figure><img src="../../.gitbook/assets/Logging-config-cluster/edit-cluster-turn-on-log.png" alt="Hộp thoại Logging configuration với công tắc đang tắt"><figcaption><p>Khi công tắc tắt, toàn bộ phần cấu hình sink được ẩn đi</p></figcaption></figure>

**Bước 4:** Khi bật, chọn lại các nguồn log tại **Log Sources** và cấu hình đích nhận log tại **Log Destination**.

<figure><img src="../../.gitbook/assets/Logging-config-cluster/detail-edit-log-2.png" alt="Cấu hình Log Sources và Log Destination với sink type Kafka"><figcaption><p>Chọn nguồn log và đích nhận log — ví dụ với Sink type là Kafka</p></figcaption></figure>

**Bước 5:** Nhập thông tin xác thực tại khối **Authentication**. Nếu **Sink type** là **OpenSearch**, nhấn thêm **Test connection** để xác nhận kết nối trước khi lưu.

<figure><img src="../../.gitbook/assets/Logging-config-cluster/detail-edit-log.png" alt="Khối Log Destination với sink type OpenSearch"><figcaption><p>Với Sink type là OpenSearch, bạn cần nhập Username và Password của OpenSearch Cluster</p></figcaption></figure>

**Bước 6:** Nhấn **Save** để lưu cấu hình.

---

## 6. Mô tả các trường cấu hình

### 6.1. Log Sources

| Nguồn log                   | Tên trong index/topic | Nội dung thu thập                                                                                                                                  | Dùng khi nào                                                                 |
| ---------------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **Audit**              | `audit`              | Sự kiện audit của kube-apiserver theo policy chuẩn VKS (xem bên dưới): ai gọi API nào, trên tài nguyên nào, lúc nào, kết quả ra sao | Đáp ứng compliance, điều tra bảo mật, truy vết thay đổi              |
| **API Server**         | `apiserver`          | Log hoạt động (stdout) của kube-apiserver                                                                                                        | Debug lỗi request, timeout, vấn đề xác thực/phân quyền                 |
| **Controller Manager** | `kcm`                | Log hoạt động (stdout) của kube-controller-manager                                                                                               | Debug khi controller không reconcile đúng, tài nguyên không được tạo |
| **Scheduler**          | `scheduler`          | Log hoạt động (stdout) của kube-scheduler                                                                                                        | Debug khi Pod ở trạng thái Pending                                          |

**Audit policy chuẩn của VKS** — áp dụng cố định cho mọi Cluster, không tùy chỉnh được:

| Loại request                                                                                                                                                                                   | Mức ghi                  | Ghi chú                                                                                            |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- | --------------------------------------------------------------------------------------------------- |
| Thao tác trên `leases`, `endpointslices`, `events`                                                                                                                                       | **Không ghi**      | Tài nguyên đổi liên tục (leader-election, heartbeat), không có giá trị audit              |
| Health/metrics endpoint (`/healthz*`, `/readyz*`, `/livez*`, `/version`, `/metrics`, `/swagger*`) và các request nội bộ của kube-proxy, kubelet, controller-manager, scheduler | **Không ghi**      | Lọc nhiễu                                                                                         |
| Đọc/ghi `secrets`, `configmaps`, `tokenreviews`                                                                                                                                          | **Metadata**        | Chỉ ghi ai/lúc nào/kết quả; **không ghi nội dung** để tránh lộ dữ liệu nhạy cảm |
| Tạo token ServiceAccount (`serviceaccounts/token`)                                                                                                                                           | **Request**         | Ghi request, không ghi response chứa token                                                        |
| Đọc (`get`, `list`, `watch`) các tài nguyên khác                                                                                                                                    | **Request**         | Có vết đọc cho compliance, không ghi nội dung trả về                                        |
| Ghi (`create`, `update`, `patch`, `delete`, `deletecollection`) các tài nguyên khác                                                                                               | **RequestResponse** | Ghi đầy đủ request và response (bỏ `managedFields`)                                          |
| Còn lại                                                                                                                                                                                       | **Metadata**        |                                                                                                     |

Ngoài ra, chỉ ghi stage `ResponseComplete`/`Panic` (không ghi `RequestReceived`), và một sự kiện audit lớn hơn **256 KB** sẽ bị cắt bớt phần `requestObject`/`responseObject` (Kubernetes đánh dấu `audit.k8s.io/truncated`).

### 6.2. Log Destination — Sink type: OpenSearch

| Trường                     | Bắt buộc | Mô tả                                                                                                                                                                                                         |
| ---------------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Sink type**          | Có        | Chọn **OpenSearch** làm đích nhận log                                                                                                                                                                 |
| **OpenSearch cluster** | Có        | Chọn một OpenSearch Cluster đang ACTIVE trong tài khoản của bạn. Nhấn biểu tượng làm mới để tải lại danh sách, hoặc dùng liên kết trong form để sang console vDB tạo/quản lý Cluster |
| **Username**           | Có        | Tài khoản OpenSearch có quyền tạo/ghi index (xem mục 3)                                                                                                                                                   |
| **Password**           | Có        | Mật khẩu tương ứng                                                                                                                                                                                         |
| **Test connection**    | —         | Nút kiểm tra VKS kết nối và xác thực được tới OpenSearch Cluster                                                                                                                                     |

VKS tự tạo index theo ngày và (nếu có quyền) index template cho từng Cluster; bạn không cần tạo trước.

### 6.3. Log Destination — Sink type: Kafka

| Trường                      | Bắt buộc | Mô tả                                                                                                                                                                                                                                                                                         |
| ----------------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Sink type**           | Có        | Chọn **Kafka** làm đích nhận log                                                                                                                                                                                                                                                      |
| **Kafka cluster**       | Có        | Chọn một Kafka Cluster đang ACTIVE trong tài khoản của bạn, hiện chỉ hỗ trợ cụm vKafka public (Cần cấu hình public cụm vKafka từ vDB). Nhấn biểu tượng làm mới để tải lại danh sách, hoặc dùng liên kết trong form để sang console vDB tạo/quản lý Cluster |
| **Kafka user**          | Có        | Chọn Kafka User dùng để ghi log. Danh sách chỉ hiển thị user có quyền **produce** trên Kafka Cluster                                                                                                                                                                            |
| **Authentication mode** | Có        | Phương thức xác thực khi ghi log: **SASL** hoặc **mTLS**. Chỉ chọn được phương thức mà cả Kafka Cluster và Kafka User đều hỗ trợ                                                                                                                                |

Khác với OpenSearch, form Kafka không có nút **Test connection**.

**VKS tự tạo topic** trên Kafka Cluster của bạn — một topic cho mỗi nguồn log đang bật, tên `{user_id}_{cluster_id}_{component}` (3 partition, 3 replica). Các topic này tính vào quota topic của Kafka Cluster. Bạn không cần tạo trước và **không nên xóa** khi logging còn bật; nếu xóa, VKS sẽ tạo lại ở lần giao log tiếp theo.

---

## 7. Lưu ý quan trọng

- **Bạn tự quản lý retention.** VKS không áp thời gian lưu trữ lên dữ liệu tại sink. Hãy cấu hình chính sách xóa dữ liệu (ví dụ ISM trên OpenSearch, retention trên topic Kafka) phù hợp với nhu cầu và chi phí của bạn. Index OpenSearch được tạo theo ngày (`-YYYY.MM.dd`) nên rất thuận tiện để áp ISM theo tuổi index.
- **Chi phí lưu trữ thuộc về sink của bạn.** Càng bật nhiều nguồn log, lượng dữ liệu ghi vào OpenSearch/Kafka càng lớn. Với Cluster có lưu lượng API cao, **Audit** là nguồn sinh nhiều dữ liệu nhất.
- **OpenSearch đầy đĩa → log tạm dừng, không mất.** Khi OpenSearch Cluster chạm ngưỡng dung lượng (flood-stage, index chuyển read-only), VKS giữ log lại và giao bù sau khi bạn giải phóng dung lượng hoặc mở rộng Cluster. Trong thời gian đó log mới sẽ **không** xuất hiện.
- **Log có thể trùng lặp.** Cơ chế at-least-once ưu tiên không mất log, nên khi giao bù sau sự cố, một số bản ghi có thể xuất hiện nhiều hơn một lần. Với OpenSearch, sự kiện audit dùng `auditID` làm `_id` nên OpenSearch tự deduplicate (ghi đè bản ghi trùng); log **API Server / Controller Manager / Scheduler** không có định danh nên có thể bị ghi đôi.
- **Log không phải thời gian thực.** Bộ giao log co giãn theo lượng log chờ (scale từ 0), nên sau khi bật hoặc khi Cluster ít traffic, log có thể xuất hiện trễ **vài phút**.
- **Xóa Cluster VKS không xóa log của bạn.** Toàn bộ tài nguyên logging phía VKS được dọn sạch, nhưng log đã giao vẫn nằm nguyên trong OpenSearch/Kafka của bạn.

---

## 8. Kết quả

Sau khi bật thành công, log Control Plane của Cluster bắt đầu được giao về sink bạn đã chọn (thường sau vài phút), tách theo tài khoản, Cluster và loại log.

**Quy ước đặt tên** — với `user_id` là ID tài khoản GreenNode của bạn và `cluster_id` là ID Cluster VKS (dạng `k8s-xxxxxxxx`), `component` ∈ `audit`, `apiserver`, `kcm`, `scheduler`:

| Sink                          | Tên                                              | Ví dụ                                 |
| ----------------------------- | ------------------------------------------------- | --------------------------------------- |
| OpenSearch index (theo ngày) | `{user_id}_{cluster_id}_{component}-YYYY.MM.dd` | `11413_k8s-662308fa_audit-2026.09.07` |
| Kafka topic                   | `{user_id}_{cluster_id}_{component}`            | `11413_k8s-662308fa_audit`            |

**Định dạng bản ghi:**

- **Audit**: sự kiện [Kubernetes audit Event](https://kubernetes.io/docs/reference/config-api/apiserver-audit.v1/) (`audit.k8s.io/v1`) nguyên bản, bổ sung các trường định tuyến `user_id`, `cluster_id`, `component`, `host` (tên pod apiserver) và `@timestamp`. Với Kafka, key của message là `auditID`.
- **API Server / Controller Manager / Scheduler**: một bản ghi JSON cho mỗi dòng log, gồm `@timestamp`, `level`, `stream`, `user_id`, `cluster_id`, `component`, `host`, `message`.

**Kiểm tra:**

- Với **OpenSearch**: mở OpenSearch Dashboard, tạo index pattern `{user_id}_{cluster_id}_*` (hoặc `{user_id}_{cluster_id}_audit-*` riêng cho audit) và truy vấn.
- Với **Kafka**: sau vài phút, các topic `{user_id}_{cluster_id}_{component}` xuất hiện trên console vDB Kafka — đó là dấu hiệu VKS đã kết nối và xác thực thành công; consume các topic này bằng consumer của bạn.
