---
description: >-
  Cam kết tính sẵn sàng của hệ thống (SLA) áp dụng cho GreenNode MaaS, gồm tỷ lệ
  uptime cam kết hàng tháng, định nghĩa Downtime, công thức tính và các trường
  hợp được loại trừ.
---

# Cam kết SLA

## Tỷ lệ uptime cam kết hàng tháng

| Tỷ lệ cam kết | Đơn vị tính | Tương đương Downtime |
|---|---|---|
| **99,9%** | Thời gian không phản hồi các API request (server ngừng hoạt động) | Không vượt quá 43 phút 50 giây một tháng |

## Định nghĩa

| Thuật ngữ | Định nghĩa |
|---|---|
| **Thời Gian Uptime Hàng Tháng** | Tổng số phút trong tháng trừ đi tổng số phút trong tháng mà hệ thống Dịch Vụ ở Trạng Thái Không Sẵn Sàng do lỗi của Bên A, không bao gồm các khoảng thời gian bảo trì, thời gian ngưng Dịch Vụ do Sự Kiện Bất Khả Kháng và các trường hợp khác được loại trừ |
| **Trạng Thái Không Sẵn Sàng** (Downtime) | Trạng thái khi xảy ra một hoặc nhiều trường hợp nêu tại mục Trạng Thái Không Sẵn Sàng bên dưới |
| **Tỷ Lệ Uptime Hàng Tháng** | 100% trừ đi Tỷ Lệ Downtime Hàng Tháng |
| **Tỷ Lệ Downtime Hàng Tháng** | Tổng thời gian trong tháng hệ thống rơi vào Trạng Thái Không Sẵn Sàng, chia cho tổng số thời gian trong tháng, nhân với 100 |

## Trạng Thái Không Sẵn Sàng (Downtime)

Hệ thống ở Trạng Thái Không Sẵn Sàng khi xảy ra một hoặc nhiều trường hợp sau:

| Trường hợp | Mô tả |
|---|---|
| a | Hệ thống dừng phản hồi |
| b | Thời gian server down |

## Công thức tính

| Chỉ số | Công thức |
|---|---|
| Tỷ Lệ Downtime Hàng Tháng | (Tổng thời gian ở Trạng Thái Không Sẵn Sàng trong tháng ÷ Tổng thời gian trong tháng) × 100 |
| Tỷ Lệ Uptime Hàng Tháng | 100% − Tỷ Lệ Downtime Hàng Tháng |
| Thời Gian Uptime Hàng Tháng | Tổng số phút trong tháng − Tổng số phút ở Trạng Thái Không Sẵn Sàng do lỗi của Bên A |

## Trường hợp loại trừ khỏi Downtime

| Trường hợp loại trừ | Mô tả |
|---|---|
| Thời gian bảo trì | Các khoảng thời gian bảo trì hệ thống |
| Sự Kiện Bất Khả Kháng | Thời gian ngưng Dịch Vụ do Sự Kiện Bất Khả Kháng |
| Nguyên nhân ngoài lỗi của Bên A | Downtime chỉ được tính khi Trạng Thái Không Sẵn Sàng phát sinh do lỗi của Bên A |
| Trường hợp khác | Các trường hợp khác được loại trừ theo quy định tại hợp đồng dịch vụ |

{% hint style="info" %}
Các thuật ngữ viết hoa trên trang này (Trạng Thái Không Sẵn Sàng, Sự Kiện Bất Khả Kháng, Bên A) được định nghĩa tại hợp đồng dịch vụ. Để biết điều khoản đầy đủ, liên hệ [support@greennode.ai](mailto:support@greennode.ai), hotline **19001549** hoặc [Trung tâm hỗ trợ](https://helpdesk.greennode.ai/portal/vi/home).
{% endhint %}
