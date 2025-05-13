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

<table><thead><tr><th>Loại Flavor</th><th>Mô tả</th><th width="281">Ví dụ Flavor Name</th><th>CPU / RAM</th><th>NIC</th></tr></thead><tbody><tr><td>General Purpose</td><td>Cân bằng CPU/RAM</td><td><code>s-general</code>, <code>a-general</code>, <code>a1-standard</code>, <code>s1-standard</code></td><td> 1 -> 48 / 1 -> 192</td><td>Up to 10 Gbps</td></tr><tr><td>Compute Optimized</td><td>Tối ưu CPU, phù hợp xử lý song song</td><td><code>a1-highcpu</code>, <code>s1-highcpu</code></td><td>2 -> 32 / 2 -> 64</td><td>Up to 10 Gbps</td></tr><tr><td>Memory Optimized</td><td>Tối ưu RAM, phù hợp in-memory workload</td><td><code>s1-highmem</code>, <code>a1-highmem</code></td><td>2 -> 32 / 16 -> 256</td><td>Up to 10 Gbps</td></tr></tbody></table>

> Các flavor có hậu tố `-a`, `-s` biểu thị các phân nhóm phần cứng riêng biệt theo nhu cầu đặc thù.

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

> ✅ GPU hỗ trợ đa dạng nhu cầu từ inference (RTX 2080 Ti) đến training mạnh (A40, H100, RTX 4090).
