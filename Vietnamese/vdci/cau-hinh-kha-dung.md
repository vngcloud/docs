# Cấu hình khả dụng

Dịch vụ **VNG Dedicated Cloud Instance (vDCI)** cung cấp hạ tầng máy chủ ảo chuyên dụng, được tối ưu cho hiệu năng cao và các nhu cầu tính toán đặc thù như AI/ML, Big Data, hoặc dịch vụ hệ thống lõi. Dưới đây là các thông tin tham khảo quan trọng về môi trường triển khai hiện tại:

## Region (Vùng địa lý triển khai)

| Region ID | Vị trí  | Ghi chú                            |
| --------- | ------- | ---------------------------------- |
| `hcm`     | TP. HCM | Hiện đang hỗ trợ chính thức        |
| `han`     | Hà Nội  | **Sắp ra mắt** trong thời gian tới |

## OS Image (Hệ điều hành hỗ trợ)

| OS     | Phiên bản      | Ghi chú                                              |
| ------ | -------------- | ---------------------------------------------------- |
| Ubuntu | 22.04x64       | Hỗ trợ mặc định                                      |
| CentOS | 7.9x64, 8.4x64 | Hỗ trợ mặc định                                      |
| Khác   | Theo yêu cầu   | Liên hệ kỹ thuật để hỗ trợ upload custom image riêng |

> Người dùng có thể yêu cầu preload image tùy chỉnh theo nhu cầu (ví dụ: Windows Server, Red Hat, Debian...)

## Cấu hình phần cứng (Flavor Types)

### CPU Instance (Không có GPU)

Hệ thống cung cấp nhiều loại flavor tùy theo nhóm workload:

<table><thead><tr><th>Loại CPU</th><th width="144">Tổng RAM</th><th width="111">Tổng vCPUs</th><th>Ghi chú</th></tr></thead><tbody><tr><td>Intel Xeon Gold 6242 @ 2.80GHz</td><td>Up to 1 TB</td><td>64</td><td>Hiệu năng cao, phổ biến trong doanh nghiệp</td></tr><tr><td>Intel Xeon Gold 6226R @ 2.90GHz</td><td>Up to 1 TB</td><td>64</td><td>Dành cho workload nhỏ và ổn định</td></tr><tr><td>Intel Xeon Gold 6342 @ 2.80GHz</td><td>Up to 1 TB</td><td>96</td><td>Cân bằng giữa hiệu năng và tiêu thụ điện</td></tr><tr><td>Intel Xeon Platinum 8358P @ 2.60GHz</td><td>Up to 1 TB</td><td>128</td><td>Phù hợp workload lớn, đa nhiệm</td></tr><tr><td>AMD EPYC 7543P 32-Core</td><td>Up to 1 TB</td><td>64</td><td>Nhiều nhân, tối ưu hóa chi phí hiệu năng</td></tr><tr><td>AMD EPYC 7702P / 7713P / 7763</td><td>Up to 1 TB</td><td>96 -> 128</td><td>Nhiều nhân, tối ưu hóa chi phí hiệu năng</td></tr></tbody></table>

### GPU Instance

#### Danh sách node GPU khả dụng

| Processor Version     | GPU Model          | Số GPU | Số CPU    | RAM (GB)    |
| --------------------- | ------------------ | ------ | --------- | ----------- |
| AMD EPYC 7713         | NVIDIA A40         | 8      | 64 -> 192 | 512 -> 2048 |
| Intel Xeon Gold 6442Y | NVIDIA RTX 4090    | 8      | 64 -> 192 | 512 -> 2048 |
| Xeon Platinum 8358P   | NVIDIA RTX 4090    | 7      | 64 -> 192 | 512 -> 2048 |
| Xeon E5-2687W v4      | NVIDIA RTX 2080 Ti | 8      | 64 -> 192 | 512 -> 2048 |
| Xeon E5-2667 v4       | NVIDIA RTX 2080 Ti | 8      | 64 -> 192 | 512 -> 2048 |
| Xeon Platinum 8480C   | NVIDIA H100        | 8      | 64 -> 192 | 512 -> 2048 |

> GPU hỗ trợ đa dạng nhu cầu từ inference (RTX 2080 Ti) đến training mạnh (A40, H100, RTX 4090).
