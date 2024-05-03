---
description: Hướng dẫn cách thức provisioning tài nguyên của dịch vụ
---

# Bắt đầu với Veeam

#### Giới Thiệu

Hướng dẫn này nhằm mục đích hướng dẫn người quản trị về cách provisioning tài nguyên cho dịch vụ cloud của bạn, sử dụng tích hợp của Ceph, Veeam và tính năng Immutable S3. Việc này bao gồm các bước để tạo và cấu hình các tài nguyên cần thiết để sử dụng dịch vụ một cách hiệu quả và bảo mật.

#### Bước 1: Đăng Nhập vào Giao Diện Quản Trị

1. Truy cập vào giao diện quản trị của dịch vụ cloud của bạn thông qua trình duyệt web.
2. Sử dụng thông tin đăng nhập quản trị của bạn để đăng nhập vào hệ thống.

#### Bước 2: Chọn Loại Tài Nguyên

1. Trong giao diện quản trị, tìm và chọn phần "Provisioning" hoặc "Tài Nguyên".
2. Xem danh sách các loại tài nguyên có sẵn và chọn loại tài nguyên bạn muốn cấu hình (ví dụ: máy ảo, lưu trữ, băng thông, v.v.).

#### Bước 3: Cấu Hình Tài Nguyên

1. Điền thông tin yêu cầu cụ thể cho loại tài nguyên bạn đã chọn, bao gồm kích thước, dung lượng, v.v.
2. Chọn vị trí hoặc khu vực nơi tài nguyên sẽ được triển khai (nếu có).
3. Thiết lập các cấu hình bổ sung như cấu hình mạng, quyền truy cập, v.v. (nếu cần).

#### Bước 4: Sử Dụng Tính Năng Immutable S3

1. Kích hoạt tính năng Immutable S3 trên hệ thống lưu trữ Ceph của bạn.
2. Đảm bảo rằng tất cả các tài nguyên được triển khai sử dụng tính năng này để bảo vệ dữ liệu khỏi sự xóa hoặc sửa đổi không cần thiết.

#### Bước 5: Xác Nhận và Tạo Tài Nguyên

1. Xem lại các thông tin cấu hình để đảm bảo rằng chúng chính xác.
2. Xác nhận và gửi yêu cầu tạo tài nguyên.
3. Chờ đợi cho đến khi tài nguyên được triển khai và sẵn sàng sử dụng.

#### Bước 6: Kiểm Tra và Quản Lý Tài Nguyên

1. Sau khi tài nguyên được tạo, kiểm tra rằng chúng đã hoạt động đúng cách và đáp ứng yêu cầu của bạn.
2. Quản lý tài nguyên bằng cách sử dụng các công cụ quản lý được cung cấp, bao gồm việc mở rộng, giảm kích thước, sao lưu, v.v.

#### Bước 7: Hỗ Trợ và Bảo Trì

1. Hỗ trợ: Nếu gặp vấn đề hoặc cần trợ giúp, liên hệ với bộ phận hỗ trợ của chúng tôi để được giúp đỡ.
2. Bảo trì: Đảm bảo rằng tất cả các tài nguyên được duy trì và cập nhật thường xuyên để đảm bảo tính ổn định và hiệu suất của hệ thống.

#### Kết Luận

Việc provisioning tài nguyên là một phần quan trọng của việc sử dụng dịch vụ cloud của chúng tôi. Bằng cách tuân thủ các bước trong hướng dẫn này, bạn có thể tạo và cấu hình các tài nguyên một cách dễ dàng và hiệu quả, giúp tối ưu hóa việc sử dụng dịch vụ và đáp ứng nhu cầu của bạn.
