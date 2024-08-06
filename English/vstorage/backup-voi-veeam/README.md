# Backup with Veeam

## Overview

**Veeam** provides cloud data management, backup, disaster recovery, and data protection solutions for virtualized and physical environments. Famous for products like Veeam Backup & Replication, it enables users to efficiently and quickly backup, restore, and replicate data in a virtualized environment.&#x20;

**Veeam** supports various virtualization platforms, as well as multiple data storage and cloud computing platforms. Veeam's strengths include high integration capability, ease of management, and the ability to quickly recover data to ensure business continuity.&#x20;

**VNG Cloud**'s storage system is also a service widely used by businesses for data backup, especially when integrating data backup with Veeam. Thus, the VNG Cloud system provides feature support to help customers backup data in the most secure and safe manner.

***

## VNG Cloud hỗ trợ tính năng sao lưu

Như đã nói, hệ thống VNG Cloud đem đến cho khách hàng những tính năng hỗ trợ việc sao lưu dữ liệu:

<table><thead><tr><th width="81">STT</th><th width="185">Tính năng hỗ trợ</th><th>Mô tả</th></tr></thead><tbody><tr><td>1</td><td><strong>Object Lock</strong></td><td>Hệ thống lưu trữ sẽ làm việc và thiết lập Object Lock. Đây là tính năng quan trọng vì sẽ kích hoạt được chức năng Immutable trên Veeam, chống lại việc xóa hay thay đổi dữ liệu sao lưu từ các tác nhân độc hại như ransomware.</td></tr><tr><td>2</td><td><strong>Object Tag</strong></td><td>Tính năng gắn tag vào Object, cho phép người dùng xem/tạo/xóa Tag lên Object.</td></tr><tr><td>3</td><td><strong>Bucket Tag</strong></td><td>Tính năng gắn tag vào Bucket (Container), cho phép người dùng xem/tạo/xóa Tag lên Bucket (Container).</td></tr><tr><td>4</td><td><strong>Bucket Replication</strong></td><td>Tính năng lưu trữ tương thích S3, cho phép việc tự đồng sao chép dữ liệu từ 1 bucket (nguồn) sag một bucket khác (đích), tính năng này đảm bảo độ bền, tính sẵn sàng và dự phòng của dữ liệu. Hỗ trợ sao chép các phiên bản (Versioning) để đảm bảo tất cả các phiên bản của một đối tượng đều được sao chéo sang bucket đích.</td></tr><tr><td>5</td><td><strong>Bucket Lifecycle</strong></td><td>Tính năng trong S3, cho phép người dùng định nghĩa các quy tắc (rules) để thực hiện các hành động như chuyển (transit) dự liệu sang nơi khác hoặc xóa dự liệu sau khoản thời gian xác định (expiration).</td></tr><tr><td>6</td><td><strong>Bucket Notifications</strong></td><td>Cho phép người dùng thiết lập cấu hình các thông báo tự động khi có những sự kiện (events) xảy ra trên bucket như: tạo Object, xóa Object, phục hồi Object...</td></tr><tr><td>7</td><td><strong>Bucket Policies</strong></td><td>Cho phép người dùng quản lý kiểm soát quyền truy cập vào các bucket và các Object trong bucket đó.</td></tr></tbody></table>

***

## Lợi ích khi sao lưu với Veeam

Sử dụng Veeam mang lại nhiều lợi ích cho các tổ chức và doanh nghiệp, đặc biệt trong việc quản lý và bảo vệ dữ liệu quan trọng. Dưới đây là một số lợi ích chính khi sử dụng Veeam:

1. **Bảo vệ Dữ liệu Toàn diện**: Veeam cung cấp các giải pháp sao lưu, phục hồi và bảo vệ dữ liệu cho các môi trường ảo, vật lý và đám mây. Điều này giúp doanh nghiệp có thể phục hồi dữ liệu nhanh chóng và hiệu quả sau các sự cố như mất điện, lỗi phần cứng, hoặc tấn công mạng.
2. **Phục hồi Nhanh chóng**: Veeam nổi tiếng với khả năng phục hồi dữ liệu nhanh chóng, giúp giảm thiểu thời gian ngừng hoạt động và đảm bảo hoạt động kinh doanh liên tục.
3. **Quản lý Dễ dàng**: Veeam cung cấp một giao diện trực quan và thân thiện với người dùng, giúp việc quản lý sao lưu, theo dõi và báo cáo trở nên đơn giản hơn.
4. **Tích hợp và Linh hoạt**: Veeam hỗ trợ nhiều nền tảng công nghệ và có thể tích hợp với nhiều hệ thống lưu trữ dữ liệu và điện toán đám mây, cho phép doanh nghiệp tùy biến giải pháp theo nhu cầu cụ thể.
5. **Bảo mật Dữ liệu**: Veeam cung cấp các tính năng bảo mật mạnh mẽ, bao gồm mã hóa dữ liệu và cách ly dữ liệu sao lưu để bảo vệ chống lại các mối đe dọa an ninh mạng.

Các lợi ích này làm cho Veeam trở thành một lựa chọn phổ biến cho nhiều doanh nghiệp đang tìm kiếm giải pháp sao lưu và phục hồi dữ liệu tin cậy và hiệu quả.
