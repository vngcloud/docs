# Xem Usage & Limits

> Trang **Usage & Limits** cho phép bạn theo dõi mức sử dụng tài nguyên hiện tại và giới hạn tài nguyên áp dụng cho tài khoản VKS. Nếu cần tăng giới hạn, bạn có thể gửi yêu cầu trực tiếp đến đội ngũ hỗ trợ 24/7.

---

## Điều kiện cần

- Đã có tài khoản VNG Cloud và đăng nhập vào [GreenNode Portal](https://console.vngcloud.vn).

---

## Xem Usage & Limits

**Bước 1: Mở trang Usage & Limits**

1. Trên thanh điều hướng trái, chọn **VKS**.
2. Nhấn **Usage & Limits**.

**Bước 2: Xem mức sử dụng hiện tại**

Khu vực **CURRENT USAGE** hiển thị:

| Tài nguyên | Ý nghĩa |
|---|---|
| **Kubernetes Clusters** | Số cluster đang dùng / tổng giới hạn. Ví dụ: `0 / 3` nghĩa là đang dùng 0, tối đa 3 cluster. |

Thanh phần trăm bên phải cho thấy tỷ lệ đã sử dụng. Dòng phía dưới hiển thị số lượng còn lại (ví dụ: *3 clusters remaining*).

**Bước 3: Xem giới hạn tài nguyên**

Khu vực **RESOURCE LIMITS** hiển thị các giới hạn áp dụng cho mỗi cluster:

| Giới hạn | Mô tả |
|---|---|
| **Node Groups / Cluster** | Số Node Group tối đa được tạo trong một cluster. |
| **Nodes / Node Group** | Số Node tối đa trong một Node Group. |

{% hint style="info" %}
Để xem đầy đủ giới hạn tài nguyên liên quan (vCPU, RAM, Disk...) trên vServer, nhấn liên kết **View resource limits on vServer ↗** ở góc phải khu vực **RESOURCE LIMITS**.
{% endhint %}

---

## Yêu cầu tăng giới hạn

Nếu giới hạn hiện tại chưa đáp ứng nhu cầu, bạn có thể gửi yêu cầu tăng limit:

**Bước 1: Mở form yêu cầu**

1. Trên trang **Usage & Limits**, nhấn nút **Request limit increase** ở góc trên bên phải.
2. Trình duyệt chuyển đến trang hỗ trợ GreenNode tại [https://helpdesk.vngcloud.vn/portal/en/home](https://helpdesk.vngcloud.vn/portal/en/home).

**Bước 2: Gửi yêu cầu**

1. Điền thông tin yêu cầu tăng giới hạn (loại tài nguyên, số lượng cần, lý do sử dụng).
2. Gửi yêu cầu — đội ngũ hỗ trợ 24/7 sẽ phản hồi trong thời gian sớm nhất.

---

## Kết quả

Sau khi hoàn thành, bạn có thể:

- Biết chính xác số cluster và tài nguyên còn có thể tạo.
- Theo dõi mức sử dụng để tránh vượt giới hạn khi scale hệ thống.
- Chủ động yêu cầu tăng limit trước khi triển khai workload lớn.

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Tạo cluster đầu tiên | [Bắt đầu với VKS](getting-started/README.md) |
| Xem giới hạn vServer đầy đủ | [vServer Limits](https://hcm-3.console.vngcloud.vn/vserver/limit) |
| Gửi yêu cầu hỗ trợ | [GreenNode Helpdesk](https://helpdesk.vngcloud.vn/portal/en/home) |
