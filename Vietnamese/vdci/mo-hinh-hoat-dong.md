# Mô hình hoạt động

Mô hình vDCI mang lại khả năng **tách biệt tài nguyên vật lý**, nhưng vẫn **liên kết linh hoạt** với các hạ tầng đám mây khác, phù hợp cho:

* Doanh nghiệp cần bảo mật cao
* Hệ thống yêu cầu tài nguyên ổn định
* Triển khai hybrid cloud hoặc multi-cloud

<figure><img src="../.gitbook/assets/image (2) (6).png" alt=""><figcaption></figcaption></figure>

## Các thành phần chính

**1. Network vDCI**

* Đây là mạng riêng chứa các máy chủ sử dụng dịch vụ **vDCI**.
* IP nội bộ (Internal): Ví dụ `10.201.0.50`
* IP public (External): Ví dụ `18.94.100`, IPv6: `2001:8a2e:0370:7334`
* Sử dụng **Network Gateway** để giao tiếp với các hệ thống khác.

**2. Interconnect Gateways**

* Là cầu nối trung tâm, giúp kết nối giữa:
  * **vDCI ↔ VPC Prod**
  * **vDCI ↔ On-premise**
  * **vDCI ↔ Other CSPs**
* Hỗ trợ nhiều kiểu kết nối khác nhau: Internet, Dedicated Interconnect, Direct Connect.

**3. VPC Prod**

* Là hệ thống Cloud VPC tiêu chuẩn của VNG Cloud, chứa các subnet như:
  * `Subnet 11` (CIDR: `10.1.1.0/24`)
  * `Subnet 12` (CIDR: `10.1.2.0/24`)
* Mỗi subnet có thể chứa nhiều máy chủ với IP nội bộ và IP public riêng biệt.
* Giao tiếp ra ngoài thông qua **VPC Gateway**.

**4. On-Premise**

* Là hệ thống nội bộ của doanh nghiệp (ví dụ văn phòng hoặc trung tâm dữ liệu).
* Sử dụng **Dedicated Interconnect** để kết nối riêng, an toàn và băng thông cao đến vDCI thông qua Gateway.

**5. Other CSPs (Cloud Service Providers)**

* Là các nhà cung cấp dịch vụ cloud khác như AWS, Azure, GCP,...
* Kết nối đến hệ thống vDCI thông qua **Direct Connect** hoặc Internet.

**6. Internet & External Bandwidth**

* Các IP public trên vDCI/VPC có thể truy cập Internet qua cổng băng thông ngoài.
* Lưu lượng truy cập Internet sẽ được tính phí dựa trên [chính sách bandwidth](https://docs.vngcloud.vn/vng-cloud-document/vn/vserver/compute-hcm03-1a/network/bandwidth-hcm-03).

## Lưu lượng và luồng dữ liệu

<table><thead><tr><th width="248">Luồng</th><th>Mô tả</th></tr></thead><tbody><tr><td><strong>vDCI ↔ VPC</strong></td><td>Thông qua Interconnect Gateway, máy chủ vDCI có thể giao tiếp nội bộ với VPC mà không cần qua Internet.</td></tr><tr><td><strong>vDCI ↔ On-premise</strong></td><td>Sử dụng đường <strong>Dedicated Interconnect</strong>, dữ liệu truyền nội bộ giữa văn phòng và vDCI với độ trễ thấp và bảo mật cao.</td></tr><tr><td><strong>vDCI ↔ Other CSPs</strong></td><td>Kết nối trực tiếp đến các CSP khác để triển khai giải pháp đa đám mây (multi-cloud).</td></tr><tr><td><strong>vDCI ↔ Internet</strong></td><td>Truy cập ra/vào Internet thông qua IP Public và băng thông được cấp.</td></tr></tbody></table>
