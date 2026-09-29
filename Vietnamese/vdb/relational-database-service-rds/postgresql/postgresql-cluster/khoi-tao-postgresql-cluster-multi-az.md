# Khởi tạo PostgreSQL Cluster Multi-AZ

Hướng dẫn này giúp bạn tạo một PostgreSQL Cluster có các Node trải trên nhiều Availability Zone tại region Hồ Chí Minh, để cluster vẫn phục vụ được khi một Availability Zone gặp sự cố.

---

## Multi-AZ là gì

PostgreSQL Cluster trên vDB có hai chế độ triển khai, chọn tại trường **Availability & Durability**:

* **Single-AZ** — toàn bộ Node nằm trong một Availability Zone.
* **Multi-AZ** — Node được trải trên từ hai Availability Zone trở lên. Khi một Availability Zone mất kết nối, một Replica ở Availability Zone còn lại được promote thành Primary và cluster tiếp tục hoạt động.

```
   HCM03-1A                            HCM03-1B
┌──────────────────┐                ┌──────────────────┐
│ Primary (Writer) │ ─────────────→ │ Replica (Reader) │
│   Read / Write   │   Streaming    │ Read / Failover  │
└──────────────────┘   Replication  └──────────────────┘
```

| Tiêu chí | Single-AZ | Multi-AZ |
|---|---|---|
| Phân bố Node | Toàn bộ Node trong một Availability Zone | Node trải trên từ hai Availability Zone trở lên |
| Chịu lỗi ở mức Availability Zone | Không | Có |
| Nơi chọn zone | Bước **Basic configuration** | Bước **Network & Security**, cùng chỗ với Subnet |
| Yêu cầu với VPC | Không | VPC phải bật **DNS** |
| Region khả dụng | HCM, HAN | Chỉ HCM |
| Số Subnet cần chọn | 1 | Mỗi zone một Subnet — tối thiểu 2 zone, nên tối thiểu 2 Subnet |

---

## Điều kiện cần

* Đã có tài khoản GreenNode và truy cập được dịch vụ vDB.
* Làm việc ở region **HCM** — Multi-AZ hiện chỉ khả dụng tại Hồ Chí Minh.
* Đã có một VPC tại HCM **đã bật DNS**.
* VPC đó có Subnet ở **ít nhất hai Availability Zone** khác nhau.
* Đã có **Backup Policy** và **Backup Location** ở trạng thái **Available** trên Backup Center — Backup Settings là bắt buộc khi tạo PostgreSQL Cluster.

{% hint style="info" %}
Dropdown **VPC** ở bước **Network & Security** **chỉ liệt kê những VPC đã bật DNS**. Nếu không thấy VPC của bạn trong danh sách, nhiều khả năng VPC đó chưa bật DNS.
{% endhint %}

---

## Khởi tạo Cluster Multi-AZ

### Bước 1: Chọn chế độ Multi-AZ

1. Truy cập vDB Relational tại [https://vdb.console.greennode.ai/relational/database](https://vdb.console.greennode.ai/relational/database), hoặc từ trang chủ GreenNode chọn dịch vụ **vServer** rồi chọn **vDB Relational**.
2. Chọn **Region** là **HCM** trên thanh điều hướng phía trên.
3. Nhấn **Create Database**.
4. Tại mục **Basic configuration**, chọn **ENGINE** là **PostgreSQL**.
5. Chọn **Deployment type** là **PostgreSQL Cluster**.
6. Điền **CLUSTER NAME**: độ dài 6–20 ký tự, bắt đầu bằng ký tự chữ cái, cho phép `a-z`, `A-Z`, `0-9`, `_`, `-`, `.`, `@` và khoảng trắng. Bỏ trống thì hệ thống tự sinh tên cho cluster.
7. Mở dropdown **Availability & Durability** và chọn **Multi-AZ**.

Sau khi chọn **Multi-AZ**, nhóm **Zone** không còn hiển thị ở mục **Basic configuration**. Với Multi-AZ, bạn chọn zone ở [Bước 3](#bước-3-chọn-vpc-và-subnet-theo-zone) — cùng chỗ với Subnet, vì mỗi zone phải đi kèm đúng một Subnet của VPC bạn chọn.

![Basic configuration với Availability & Durability đặt là Multi-AZ](../../../../.gitbook/assets/vdb-pg-multi-az-step1-mode.png)

{% hint style="warning" %}
Đổi **Availability & Durability** sẽ xoá toàn bộ zone và Subnet đã chọn, theo cả hai chiều và ở bất kỳ thời điểm nào, kể cả khi bạn đã điền xong phần **Network & Security**. Hãy chọn chế độ trước khi cấu hình mạng.
{% endhint %}

### Bước 2: Chọn số lượng Node

1. Tại mục **Cluster specification**, chọn **Engine license** và **Engine version**.
2. Điền **Number of nodes**: tối thiểu 2, tối đa 10.
3. Đối chiếu phần phân bổ vai trò hiển thị ngay cạnh trường này.

![Cluster specification với Number of nodes và phân bổ vai trò](../../../../.gitbook/assets/vdb-pg-multi-az-step2.png)

| Number of nodes | Phân bổ vai trò |
|---|---|
| 2 | 1 Primary (Writer) · 1 Replica (Reader) |
| 3 | 1 Primary (Writer) · 2 Replicas (Reader) |
| 5 | 1 Primary (Writer) · 4 Replicas (Reader) |
| 10 | 1 Primary (Writer) · 9 Replicas (Reader) |

{% hint style="info" %}
Mỗi cluster luôn có đúng một Primary (Writer) xử lý mọi thao tác ghi. Các Node còn lại là Replica (Reader), đồng bộ dữ liệu từ Primary qua Streaming Replication và sẵn sàng được promote khi Primary gặp sự cố. Các Node được phân bổ trên những Availability Zone bạn chọn ở Bước 3.
{% endhint %}

### Bước 3: Chọn VPC và Subnet theo zone

1. Cuộn tới mục **Network & Security**.
2. Chọn **VPC** cho cluster. Dropdown chỉ hiển thị những VPC đã bật DNS; nếu chưa có VPC phù hợp, nhấn link quản lý VPC ngay dưới trường này.
3. Tại bảng **Subnets**, tick chọn các zone muốn triển khai. Mặc định hệ thống tick sẵn **hai zone đầu tiên** trong danh sách — tại region HCM là **HCM03-1A** và **HCM03-1B**.
4. Với mỗi zone đã tick, chọn một **Subnet** ở cột bên phải.
5. Bật **Public accessibility** nếu muốn truy cập cluster từ Internet.

![Network & Security với bảng Subnets chọn zone](../../../../.gitbook/assets/vdb-pg-multi-az-step4-subnets.png)

| Ràng buộc | Chi tiết |
|---|---|
| Số zone tối thiểu | Phải tick ít nhất hai zone khác nhau |
| Subnet của mỗi zone | Mỗi zone đã tick phải chọn đúng một Subnet |
| Cùng một VPC | Mọi Subnet phải thuộc VPC đã chọn |
| Zone không có Subnet | Zone không có Subnet nào trong VPC sẽ bị vô hiệu hoá trong bảng |
| Zone không hỗ trợ Storage type | Zone không hỗ trợ **Storage type** bạn đã chọn ở mục **Cluster specification** cũng không dùng được. Hệ thống hiển thị cảnh báo ngay trên bảng **Subnets**, ví dụ `Zone HCM 1C: NVMe storage type not supported` |

{% hint style="warning" %}
Thiết lập **Public accessibility** chỉ được chọn một lần duy nhất tại thời điểm khởi tạo và không thể thay đổi sau đó.
{% endhint %}

### Bước 4: Hoàn tất các bước còn lại

Các mục còn lại của luồng khởi tạo không khác so với Single-AZ:

* **Cluster specification** — **Instance family**, **CPU Platform**, **Package** (Core, Ram, Free backup), **Storage type**, **Storage size**.
* **DB instance settings** — **Master username** và **Master password**. Lưu ý **Master username** không được trùng các username hệ thống đã dành riêng.
* **Database options** — **Database name** và **Configuration group** (tuỳ chọn).
* **Backup settings** — **Backup Policy** và **Backup Location**, bắt buộc với mọi PostgreSQL Cluster.

Chi tiết từng trường xem tại [Khởi tạo và Quản lý PostgreSQL Cluster](khoi-tao-va-quan-ly-postgresql-cluster.md).

Rà soát lại thông tin ở panel **Summary** bên phải, sau đó nhấn **CREATE DATABASE**.

---

## Kết quả

Cluster chuyển sang trạng thái **Building**, và sang **Active** khi khởi tạo hoàn tất. Mở trang chi tiết cluster để kiểm tra:

* Mục **General information** hiển thị **Availability & Durability** là **Multi-AZ**, kèm engine version và số Node của cluster.
* Tab **Connectivity & Security** hiển thị nhóm tab **Select zone**, mỗi Availability Zone của cluster là một tab.

---

## Kết nối tới Cluster Multi-AZ

Tại tab **Connectivity & Security**, mỗi tab zone hiển thị hai nhóm endpoint:

| Nhóm endpoint | Dùng cho |
|---|---|
| **PRIMARY ENDPOINT (READ/WRITE)** | Truy vấn đọc và ghi, trỏ tới Node Primary |
| **READER ENDPOINT (READ-ONLY, LOAD BALANCED)** | Truy vấn chỉ đọc, chia tải trên các Node Replica |

Mỗi nhóm gồm **Private Endpoint**, **Public Endpoint** và **Domain Endpoint**, đều có nút sao chép. Lấy **Port** hiển thị ngay tại nhóm endpoint bạn dùng.

GreenNode khuyến nghị dùng **Domain Endpoint** trong chuỗi kết nối của ứng dụng:

* Domain Endpoint là **một giá trị duy nhất cho cả cluster**, không thay đổi khi bạn chuyển sang tab zone khác.
* Domain Endpoint **không đổi khi xảy ra failover**, nên ứng dụng không phải sửa cấu hình sau mỗi lần Primary chuyển sang Node khác.
* Bạn có thể kiểm tra danh sách địa chỉ mà Domain Endpoint phân giải ra bằng lệnh:

```bash
dig A <domain-endpoint>
```

Địa chỉ **Private Endpoint** và **Public Endpoint** của từng zone dùng khi bạn cần khai báo địa chỉ cụ thể, ví dụ mở rule firewall hoặc cấu hình định tuyến.

Hướng dẫn cài client tool, chuỗi kết nối và tham số `sslmode=require`: [Kết nối tới RDS Instance](../../getting-started/ket-noi-toi-rds-instance/README.md).

---

## Giới hạn và lưu ý

| Mục | Giới hạn |
|---|---|
| Region | Chỉ HCM. Region HAN có PostgreSQL Cluster nhưng chưa hỗ trợ Multi-AZ |
| Số lượng Node | Tối thiểu 2, tối đa 10 |
| Số Availability Zone | Tối thiểu 2 |
| VPC | Phải bật DNS |
| Đổi chế độ sau khi tạo | Không hỗ trợ đổi giữa Single-AZ và Multi-AZ sau khi cluster đã được tạo. Cần tạo cluster mới |
| Configuration group | Configuration group gắn theo deployment type; group tạo cho Cluster không áp dụng được cho Single Node và ngược lại |
| Storage khi khôi phục từ backup | Cluster mới cần dung lượng lớn hơn dung lượng của bản backup. Hệ thống hiển thị mức tối thiểu ngay tại trường **Storage size** sau khi bạn chọn bản backup — nhập bằng hoặc lớn hơn mức đó |

---

## Xem thêm

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Tìm hiểu kiến trúc và khái niệm PostgreSQL Cluster | [PostgreSQL Cluster](README.md) |
| Quản lý cluster: backup, resize, đổi số Node | [Khởi tạo và Quản lý PostgreSQL Cluster](khoi-tao-va-quan-ly-postgresql-cluster.md) |
| Kết nối tới database bằng client tool | [Kết nối tới RDS Instance](../../getting-started/ket-noi-toi-rds-instance/README.md) |
| Cấu hình tham số cho cluster | [PostgreSQL Parameters cho Cluster](cau-hinh-tham-so-cho-cluster.md) |
