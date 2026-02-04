# Multi-AZ Control Plane

## Tổng quan <a href="#multi-az-control-plane-tongquan" id="multi-az-control-plane-tongquan"></a>

**Multi-AZ Control Plane** là tính năng cho phép triển khai Kubernetes Cluster với Control Plane được phân bổ trên nhiều Availability Zones (AZ) khác nhau, đảm bảo **High Availability** (HA) cho cluster của bạn.

### Multi-AZ Control Plane là gì?

Trong mô hình Multi-AZ, các thành phần của Control Plane (API Server, Controller Manager, Scheduler, etcd) được triển khai trên nhiều AZ. Điều này đảm bảo rằng:

* Nếu một AZ gặp sự cố, Control Plane vẫn hoạt động bình thường từ các AZ còn lại
* Tự động failover mà không cần can thiệp thủ công
* Đáp ứng yêu cầu compliance về disaster recovery

### So sánh Single-AZ và Multi-AZ Cluster

| Đặc điểm | Single-AZ | Multi-AZ |
| --- | --- | --- |
| **Control Plane Availability** | 99.9% | 99.99% |
| **Khả năng chịu lỗi** | Single point of failure tại AZ level | Chịu được lỗi ở cấp độ AZ |
| **Chi phí** | Thấp hơn | Cao hơn (Multi-AZ Control Plane) |
| **Độ trễ (Latency)** | Thấp (cùng AZ) | Cao hơn một chút (cross-AZ cho Control Plane) |
| **Private DNS (VPC)** | Tùy chọn | Bắt buộc (prerequisite) |
| **Use Case** | Development, Testing | Production, Mission-critical |
| **Yêu cầu Subnet** | 1 subnet | Tối thiểu 2 subnets từ 2 AZ khác nhau |
| **Node Group** | 1 AZ (1 subnet) | 1 AZ per Node Group (chọn 1 subnet từ danh sách subnets của cluster) |

### Khi nào nên sử dụng Multi-AZ Cluster?

* **Production workloads**: Các ứng dụng yêu cầu uptime cao và không chấp nhận downtime
* **Mission-critical applications**: Hệ thống thanh toán, giao dịch, dữ liệu quan trọng
* **Enterprise requirements**: Tuân thủ các yêu cầu compliance về disaster recovery
* **High Availability**: Khi cần đảm bảo cluster vẫn hoạt động ngay cả khi một AZ gặp sự cố

{% hint style="info" %}
**Lưu ý:**

* **Single-AZ Cluster** phù hợp cho môi trường **development** và **testing** do chi phí thấp hơn
* **Multi-AZ Cluster** được khuyến nghị cho môi trường **production**
{% endhint %}

***

## Điều kiện tiên quyết (Prerequisites) <a href="#multi-az-control-plane-prerequisites" id="multi-az-control-plane-prerequisites"></a>

Để tạo Multi-AZ Cluster, bạn cần đảm bảo các điều kiện sau:

### 1. VPC phải bật DNS

{% hint style="warning" %}
**Quan trọng:**

Multi-AZ Control Plane **chỉ hỗ trợ VPC đã bật DNS**. Nếu VPC chưa bật DNS, VPC đó sẽ **không hiển thị** trong dropdown khi tạo Multi-AZ Cluster.
{% endhint %}

Để bật DNS cho VPC, vui lòng thực hiện tại portal vServer theo hướng dẫn tại [đây](../../vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc/).

### 2. Chuẩn bị Subnets

* **Tối thiểu 2 subnets** từ **2 Availability Zone khác nhau**
* Tất cả subnets phải thuộc **cùng một VPC**
* Các subnets phải ở trạng thái **ACTIVE**

Ví dụ cấu hình subnets hợp lệ:

| Subnet Name | AZ | CIDR | Hợp lệ? |
| --- | --- | --- | --- |
| sub-1A | HCM-1A | 10.60.0.0/24 | ✅ |
| sub-1B | HCM-1B | 10.60.1.0/24 | ✅ |

Ví dụ cấu hình subnets **không** hợp lệ:

| Subnet Name | AZ | CIDR | Lý do không hợp lệ |
| --- | --- | --- | --- |
| sub-1A | HCM-1A | 10.60.0.0/24 | ❌ Cùng AZ |
| sub-2A | HCM-1A | 10.60.3.0/24 | ❌ Cùng AZ |

### 3. Các điều kiện khác

* Có ít nhất 1 **SSH key** đang ở trạng thái **ACTIVE**. Nếu bạn chưa có SSH key, vui lòng khởi tạo theo hướng dẫn tại [đây](../../vserver/compute-hcm03-1a/security/ssh-key-bo-khoa.md).
* Đã cài đặt và cấu hình **kubectl** trên thiết bị của bạn. Vui lòng tham khảo tại [đây](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) nếu bạn chưa rõ cách cài đặt.

***

## Tạo Multi-AZ Cluster <a href="#multi-az-control-plane-taocluster" id="multi-az-control-plane-taocluster"></a>

Để tạo một Multi-AZ Cluster, hãy làm theo các bước bên dưới:

### Bước 1: Truy cập VKS Console

Truy cập vào [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

### Bước 2: Khởi tạo Cluster

Tại màn hình **Overview**, chọn **Create a Cluster**.

### Bước 3: Cấu hình Cluster Information

Tại phần **Cluster Configuration**, nhập các thông tin cơ bản:

* **Cluster Name**: Tên cho cluster của bạn (3-63 ký tự, chỉ bao gồm chữ, số và dấu gạch ngang)
* **Kubernetes Version**: Chọn phiên bản Kubernetes mong muốn
* **Description**: Mô tả cho cluster (tùy chọn)

### Bước 4: Cấu hình Network Setting - Chọn Control Plane Availability

Đây là bước quan trọng để tạo Multi-AZ Cluster:

**4.1. Chọn Control Plane Availability**

Tại phần **Network Setting**, bạn sẽ thấy trường **Control Plane Availability** với badge **[NEW]**:

<!-- TODO: Chèn hình ảnh Control Plane Availability dropdown -->
<figure><img src="../../.gitbook/assets/[PLACEHOLDER-control-plane-availability-dropdown].png" alt=""><figcaption><p>Control Plane Availability selection</p></figcaption></figure>

Có 2 lựa chọn:

| Option | Mô tả |
| --- | --- |
| **Single-AZ** | Triển khai cluster trong một Availability Zone. Phù hợp cho môi trường development và testing. |
| **Multi-AZ** | Triển khai cluster trên nhiều Availability Zones để đảm bảo High Availability. |

Chọn **Multi-AZ** để tạo cluster với Control Plane phân bổ trên nhiều AZ.

**4.2. Chọn VPC**

* Chọn VPC đã **bật DNS** từ dropdown
* Lưu ý: Chỉ các VPC đã bật DNS mới hiển thị khi chọn Multi-AZ

<!-- TODO: Chèn hình ảnh VPC dropdown khi chọn Multi-AZ -->
<figure><img src="../../.gitbook/assets/[PLACEHOLDER-vpc-dropdown-multi-az].png" alt=""><figcaption><p>VPC selection for Multi-AZ Cluster</p></figcaption></figure>

**4.3. Chọn Subnets cho Control Plane**

Khi chọn **Multi-AZ**, trường **Subnets** sẽ hiển thị dạng **multi-select dropdown**:

<!-- TODO: Chèn hình ảnh Subnets multi-select dropdown -->
<figure><img src="../../.gitbook/assets/[PLACEHOLDER-subnets-multi-select].png" alt=""><figcaption><p>Subnets multi-select for Multi-AZ Cluster</p></figcaption></figure>

**Behavior mặc định:**
* Hệ thống sẽ **tự động chọn sẵn 1 subnet đầu tiên của mỗi AZ** có trong VPC
* Ví dụ: Nếu VPC có subnets ở HCM-1A, HCM-1B, HCM-1C → Mặc định chọn sẵn 3 subnets (1 subnet/zone)

**Các subnet đã chọn hiển thị dạng chip/tag:**

```
[sub-1A 10.60.0.0/24 • HCM-1A] [x]  [sub-1B 10.60.1.0/24 • HCM-1B] [x]
```

* Click nút **(x)** trên chip để xóa subnet khỏi danh sách đã chọn
* Bạn có thể thêm/bớt subnet nhưng phải đảm bảo **tối thiểu 2 subnets từ 2 AZ khác nhau**

<!-- TODO: Chèn hình ảnh subnet chips đã chọn -->
<figure><img src="../../.gitbook/assets/[PLACEHOLDER-subnet-chips].png" alt=""><figcaption><p>Selected subnets displayed as chips</p></figcaption></figure>

{% hint style="info" %}
**Validation Rules:**

* Tối thiểu **2 subnets** phải được chọn
* Các subnets phải thuộc **ít nhất 2 AZ khác nhau**
* Nếu chọn 2 subnet cùng AZ, hệ thống sẽ hiển thị lỗi: *"Các subnet phải thuộc ít nhất 2 Availability Zone khác nhau"*
{% endhint %}

### Bước 5: Cấu hình Node Group Network Setting

Tại phần **Node group network setting**, bạn cần chọn subnet cho Node Group:

<!-- TODO: Chèn hình ảnh Node Group Network Setting section -->
<figure><img src="../../.gitbook/assets/[PLACEHOLDER-node-group-network-setting].png" alt=""><figcaption><p>Node Group Network Setting for Multi-AZ Cluster</p></figcaption></figure>

| Field | Mô tả |
| --- | --- |
| **VPC** | Kế thừa từ Network Configuration (read-only, không thể thay đổi) |
| **Subnet** | Dropdown single-select, chỉ hiển thị các subnets đã chọn cho cluster ở bước trước |

**Lưu ý quan trọng:**

* Mỗi Node Group chỉ được chọn **1 subnet** (tương ứng với 1 AZ)
* AZ của Node Group được xác định tự động dựa trên subnet đã chọn
* Bạn có thể tạo thêm Node Group ở các AZ khác sau khi cluster được tạo

{% hint style="info" %}
**Tip:**

Để đảm bảo High Availability cho workloads, bạn nên tạo nhiều Node Group ở các AZ khác nhau. Điều này giúp phân bổ worker nodes trên nhiều AZ, tăng khả năng chịu lỗi cho ứng dụng.
{% endhint %}

### Bước 6: Cấu hình các phần còn lại

Hoàn tất cấu hình các phần sau (tương tự như tạo Single-AZ Cluster):

* **Default Node Group Configuration**: Node Group Information, Automation Setting, Instance type, Volume Setting, Security Setting
* **Plugin**: Enable BlockStore Persistent Disk CSI Driver, Enable vLB Native Integration Driver

### Bước 7: Tạo Cluster

Chọn **Create Kubernetes cluster**. Hãy chờ vài phút để hệ thống khởi tạo cluster, trạng thái lúc này là **Creating**.

<!-- TODO: Chèn hình ảnh cluster đang Creating -->
<figure><img src="../../.gitbook/assets/[PLACEHOLDER-cluster-creating].png" alt=""><figcaption><p>Cluster đang được khởi tạo</p></figcaption></figure>

Khi trạng thái chuyển sang **Active**, cluster của bạn đã sẵn sàng sử dụng.

***

## Quản lý Multi-AZ Cluster <a href="#multi-az-control-plane-quanly" id="multi-az-control-plane-quanly"></a>

### Xem thông tin Cluster trên trang danh sách

Tại trang danh sách Kubernetes Cluster, bạn có thể nhận biết Multi-AZ Cluster thông qua cột **Control Plane Availability**:

<!-- TODO: Chèn hình ảnh trang danh sách cluster với cột Control Plane Availability -->
<figure><img src="../../.gitbook/assets/[PLACEHOLDER-cluster-list-page].png" alt=""><figcaption><p>Cluster List Page với cột Control Plane Availability</p></figcaption></figure>

| Badge | Ý nghĩa |
| --- | --- |
| **Single-AZ** (badge màu xám) | Control Plane nằm trong 1 AZ |
| **Multi-AZ** (badge màu xanh đậm) | Control Plane phân bổ trên nhiều AZ |

### Xem chi tiết Cluster

Khi truy cập vào trang chi tiết của Multi-AZ Cluster:

**1. General Information**

Hiển thị thêm trường **Control Plane Availability** với giá trị **Multi-AZ** (badge màu xanh đậm)

<!-- TODO: Chèn hình ảnh General Information section với Control Plane Availability -->
<figure><img src="../../.gitbook/assets/[PLACEHOLDER-cluster-detail-general-info].png" alt=""><figcaption><p>General Information với Control Plane Availability</p></figcaption></figure>

**2. Network Section**

Hiển thị danh sách **Subnets** đang sử dụng với thông tin chi tiết:

```
Subnets (2)
├── sub-85ba01f6-02ec-4dfc-8884-ee0036c68a5b
│   Name: sub-1A (10.60.0.0/24) | AZ: HCM-1A
└── sub-12345678-abcd-efgh-ijkl-mnopqrstuvwx
    Name: sub-1B (10.60.1.0/24) | AZ: HCM-1B
```

* Click vào icon **copy** bên cạnh Subnet ID để copy vào clipboard

<!-- TODO: Chèn hình ảnh Network section với danh sách Subnets -->
<figure><img src="../../.gitbook/assets/[PLACEHOLDER-cluster-detail-network].png" alt=""><figcaption><p>Network section với danh sách Subnets</p></figcaption></figure>

**3. Node Group Tab**

Bảng Node Group hiển thị thêm cột **Availability Zone** để biết Node Group đang ở AZ nào:

<!-- TODO: Chèn hình ảnh Node Group tab với cột AZ -->
<figure><img src="../../.gitbook/assets/[PLACEHOLDER-node-group-tab-az].png" alt=""><figcaption><p>Node Group tab với cột Availability Zone</p></figcaption></figure>

### Upgrade Control Plane

Quy trình upgrade Control Plane cho Multi-AZ Cluster **không khác biệt** so với Single-AZ Cluster:

1. Truy cập vào trang chi tiết cluster
2. Thực hiện upgrade Control Plane lên version mới theo hướng dẫn tại [đây](upgrading-control-plane-version.md)

{% hint style="info" %}
**Đặc điểm upgrade Multi-AZ Cluster:**

* Hệ thống thực hiện **rolling upgrade** trên tất cả các AZ
* Cluster vẫn **available** trong quá trình upgrade
* Các workload hiện có **không bị gián đoạn**
* Nếu upgrade thất bại, hệ thống tự động **rollback** về version trước đó
{% endhint %}

### Xóa Cluster

Quy trình xóa Multi-AZ Cluster **tương tự** như Single-AZ Cluster:

1. Truy cập vào [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console.vngcloud.vn/k8s-cluster)
2. Chọn cluster muốn xóa và chọn **Delete**
3. Xác nhận xóa

{% hint style="warning" %}
**Lưu ý khi xóa Multi-AZ Cluster:**

Khi xóa cluster, hệ thống sẽ:
* Xóa tất cả **Control Plane components** trên **mọi AZ**
* Xóa tất cả **Node Groups** và **Worker Nodes**
* Giải phóng **network resources** (subnets vẫn còn trong VPC)
* Xóa **Security Group** mặc định của cluster
* Xóa **Load Balancer** mặc định của cluster

Các tài nguyên sau **có thể không bị xóa tự động**:
* Load Balancer được integrate vào cluster bởi bạn
* Persistent Volume được integrate vào cluster bởi bạn
{% endhint %}

***

## Kiến trúc Multi-AZ Control Plane <a href="#multi-az-control-plane-kientruc" id="multi-az-control-plane-kientruc"></a>

Sơ đồ dưới đây minh họa kiến trúc của Multi-AZ Cluster:

```
                    ┌─────────────────────────────────────────┐
                    │              VPC (10.60.0.0/16)         │
                    │                                         │
┌───────────────────┼─────────────────────────────────────────┼───────────────────┐
│                   │                                         │                   │
│   ┌───────────────┴───────────────┐   ┌───────────────────┴───────────────┐   │
│   │         AZ: HCM-1A            │   │         AZ: HCM-1B                │   │
│   │    Subnet: 10.60.0.0/24       │   │    Subnet: 10.60.1.0/24           │   │
│   │                               │   │                                   │   │
│   │   ┌─────────────────────┐     │   │   ┌─────────────────────┐         │   │
│   │   │   Control Plane     │     │   │   │   Control Plane     │         │   │
│   │   │   (API Server)      │     │   │   │   (API Server)      │         │   │
│   │   └─────────────────────┘     │   │   └─────────────────────┘         │   │
│   │                               │   │                                   │   │
│   │   ┌─────────────────────┐     │   │   ┌─────────────────────┐         │   │
│   │   │   Worker Nodes      │     │   │   │   Worker Nodes      │         │   │
│   │   │   (Node Group 1)    │     │   │   │   (Node Group 2)    │         │   │
│   │   └─────────────────────┘     │   │   └─────────────────────┘         │   │
│   │                               │   │                                   │   │
│   └───────────────────────────────┘   └───────────────────────────────────┘   │
│                                                                               │
│                        ┌─────────────────────┐                                │
│                        │   vLB Multi-AZ      │                                │
│                        │   (Load Balancer)   │                                │
│                        └─────────────────────┘                                │
│                                                                               │
└───────────────────────────────────────────────────────────────────────────────┘
```

**Các thành phần chính:**

* **Control Plane**: Được phân bổ trên nhiều AZ, bao gồm API Server, Controller Manager, Scheduler, etcd
* **etcd cluster**: Được replicate across AZs để đảm bảo data consistency
* **vLB Multi-AZ**: Load Balancer phân phối traffic đến Control Plane nodes trên các AZ
* **Node Groups**: Mỗi Node Group chỉ triển khai trong 1 subnet (1 AZ), người dùng có thể tạo nhiều Node Group ở các AZ khác nhau

***

## Giới hạn và Lưu ý <a href="#multi-az-control-plane-gioihan" id="multi-az-control-plane-gioihan"></a>

### Giới hạn hiện tại

| Giới hạn | Mô tả |
| --- | --- |
| **Không thể chuyển đổi** | Không thể chuyển đổi cluster từ Single-AZ sang Multi-AZ (hoặc ngược lại) sau khi đã tạo |
| **Không thể thay đổi subnets** | Không thể thêm/bớt subnet sau khi đã tạo Multi-AZ cluster |
| **Node Group vẫn Single-AZ** | Mỗi Node Group chỉ hỗ trợ triển khai trong 1 subnet (1 AZ) |
| **VPC DNS bắt buộc** | VPC phải bật DNS để tạo Multi-AZ Cluster |

### Lưu ý quan trọng

{% hint style="warning" %}
**Về chi phí:**

Multi-AZ Cluster có chi phí **cao hơn** so với Single-AZ do Control Plane được triển khai trên nhiều AZ. Hãy cân nhắc kỹ nhu cầu sử dụng trước khi lựa chọn.
{% endhint %}

{% hint style="info" %}
**Về Node Group:**

* Khi tạo cluster, Node Group đầu tiên chỉ có thể chọn 1 subnet từ danh sách subnets đã cấu hình cho cluster
* Để đảm bảo HA cho workloads, bạn nên tạo thêm Node Group ở các AZ khác sau khi cluster được tạo
{% endhint %}

{% hint style="info" %}
**Về cross-AZ latency:**

Traffic giữa các AZ có thể có độ trễ cao hơn một chút so với traffic trong cùng AZ. Điều này là bình thường và được chấp nhận để đổi lấy khả năng High Availability.
{% endhint %}

***

## FAQ <a href="#multi-az-control-plane-faq" id="multi-az-control-plane-faq"></a>

### 1. Tôi có thể chuyển cluster từ Single-AZ sang Multi-AZ không?

**Không.** Hiện tại VKS không hỗ trợ chuyển đổi Control Plane Availability sau khi cluster đã được tạo. Bạn cần tạo mới cluster với cấu hình Multi-AZ.

### 2. Node Group của tôi có tự động phân bổ trên nhiều AZ không?

**Không.** Mỗi Node Group chỉ triển khai trong 1 AZ (1 subnet). Để phân bổ workloads trên nhiều AZ, bạn cần tạo nhiều Node Group ở các AZ khác nhau.

### 3. Điều gì xảy ra khi một AZ gặp sự cố?

Khi 1 AZ gặp sự cố:
* **Control Plane** vẫn hoạt động bình thường từ các AZ còn lại
* **Node Groups** ở AZ đó sẽ không available
* Kubernetes sẽ tự động reschedule các pods sang các nodes ở AZ khác (nếu có Node Group ở các AZ khác)

### 4. Tại sao VPC của tôi không hiển thị khi tạo Multi-AZ Cluster?

VPC của bạn chưa bật **DNS**. Vui lòng bật DNS cho VPC tại portal vServer trước khi tạo Multi-AZ Cluster.

### 5. Tôi có thể chọn nhiều subnet cùng AZ cho Multi-AZ Cluster không?

Bạn có thể chọn nhiều subnet, nhưng phải đảm bảo các subnet thuộc **ít nhất 2 AZ khác nhau**. Nếu tất cả subnet đều thuộc cùng 1 AZ, hệ thống sẽ báo lỗi validation.

### 6. Chi phí Multi-AZ Cluster như thế nào?

Multi-AZ Cluster có chi phí cao hơn Single-AZ do Control Plane được triển khai trên nhiều AZ. Vui lòng tham khảo trang [Cách tính giá](../cach-tinh-gia.md) để biết chi tiết.
