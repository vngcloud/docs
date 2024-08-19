# Bắt đầu với Kafka Cluster

Với vDB Kafka Cluster, bạn có thể nhanh chóng triển khai và quản lý cụm Kafka một cách hiệu quả, tập trung vào phát triển ứng dụng và khai thác sức mạnh của xử lý luồng sự kiện theo thời gian thực. Làm theo hướng dẫn dưới đây để bắt đầu sử dụng dịch vụ Kafka Cluster.

## Bước 1: Truy cập và Đăng nhập

1. Mở trình duyệt web và truy cập vào giao diện vDB Kafka Cluster theo đường dẫn tại đây:
2. Nếu bạn đã có tài khoản, hãy nhập thông tin đăng nhập của bạn.

Tham khảo hướng dẫn đăng nhập vào VNG Cloud [tại đây](../../identity-and-access-management-iam/cac-loai-dinh-danh-iam/tai-khoan-user-accounts/cach-dang-nhap-vao-vng-cloud.md).

## Bước 2: Tạo Cụm Kafka

1. Nhấp vào nút "Tạo Cụm Kafka" hoặc tương tự.
2. Điền thông tin sau:
   * **Tên:** Đặt tên cho cụm Kafka của bạn để dễ nhận biết và quản lý.
   * **Kafka Version:** Chọn phiên bản Kafka phù hợp với nhu cầu của bạn. Các phiên bản khác nhau có thể có tính năng và hiệu suất khác nhau.
   * **Flavor (CPU, RAM):** Chọn cấu hình phần cứng (CPU và RAM) cho các broker trong cụm Kafka. Cấu hình này ảnh hưởng đến khả năng xử lý và hiệu suất của cụm.
   * **Số lượng Broker:** Xác định số lượng broker trong cụm Kafka. Số lượng broker ảnh hưởng đến khả năng chịu lỗi và khả năng mở rộng của cụm.
   * **Storage từng Broker (IOPS và Dung lượng):** Chọn dung lượng lưu trữ và IOPS (Số lượng hoạt động nhập/xuất mỗi giây) cho mỗi broker. Điều này ảnh hưởng đến khả năng lưu trữ dữ liệu và hiệu suất đọc/ghi của cụm.
   * **Network (VPC, Subnet):** Chọn mạng ảo (VPC) và subnet mà cụm Kafka sẽ được triển khai. Khi khởi tạo, cụm Kafka sẽ ở chế độ private (chỉ truy cập được từ trong VPC). Sau khi khởi tạo thành công, bạn có thể mở truy cập public nếu cần.
   * **Access Method Control (mTLS, SASL):** Chọn phương thức xác thực và ủy quyền cho client kết nối đến cụm Kafka. mTLS sử dụng chứng chỉ client và server, SASL sử dụng tên người dùng và mật khẩu.
   * **Encryption Mode:** Chọn chế độ mã hóa dữ liệu. Mặc định, mã hóa in transit (dữ liệu được mã hóa khi truyền giữa client và broker) và within cluster (dữ liệu được mã hóa khi lưu trữ trên các broker) được bật.
   * **Config Group:** Chọn nhóm cấu hình áp dụng cho cụm Kafka. Nhóm cấu hình chứa các thiết lập chi tiết về hoạt động của Kafka.
3. Nhấp vào nút "Tạo" để bắt đầu quá trình tạo cụm Kafka.

## Bước 3: Tạo Topic

1. Sau khi cụm Kafka được tạo thành công, truy cập vào trang quản lý cụm Kafka đó.
2. Tìm và nhấp vào phần "Tạo Topic".
3. Điền thông tin sau:
   * **Tên:** Đặt tên cho topic. Lưu ý rằng tên này sẽ không thể thay đổi sau khi khởi tạo.
   * **Partition Count:** Xác định số lượng phân vùng cho topic. Số lượng phân vùng ảnh hưởng đến khả năng mở rộng và song song của topic.
   * **Replication Factor:** Xác định số lượng bản sao của mỗi phân vùng. Điều này ảnh hưởng đến khả năng chịu lỗi của topic.
   * **Retention Hour/Byte:** Xác định thời gian hoặc dung lượng lưu trữ tối đa cho dữ liệu trong topic.
4. Nhấp vào nút "Tạo" để tạo topic.

## Bước 4: Tạo Kafka User và Phân Quyền

1. Trong trang quản lý cụm Kafka, tìm và nhấp vào phần "Tạo Kafka User".
2. Điền thông tin sau:
   * **Tên:** Đặt tên cho Kafka user.
   * **Phân quyền:** Chọn các quyền Produce (ghi dữ liệu vào topic) và Consume (đọc dữ liệu từ topic) cho từng topic mà user này cần truy cập.
   * **Phương thức Truy cập:** Chọn phương thức truy cập cho Kafka user (mTLS hoặc SASL) tùy thuộc vào phương thức được bật cho cụm Kafka.
3. Nhấp vào nút "Tạo" để tạo Kafka user.

## Bước 5: Chỉnh sửa Truy cập

1. Trong trang quản lý cụm Kafka, tìm và nhấp vào phần "Truy cập Công khai" hoặc "Whitelist IP" thông qua Security Group.
2. **Truy cập Công khai:** Nếu bạn muốn cho phép truy cập từ bất kỳ đâu, hãy bật "Truy cập Công khai".
3. **Whitelist IP:** Nếu bạn muốn giới hạn truy cập chỉ từ các địa chỉ IP cụ thể, hãy thêm các địa chỉ IP đó vào danh sách whitelist. Bạn có thể cần sử dụng Security Group để định nghĩa các quy tắc truy cập chi tiết hơn (IP Protocol, Port, Remote IP Prefix).

## Bước 6: Xóa Cụm Kafka

1. Khi bạn không còn nhu cầu sử dụng cụm Kafka, hãy truy cập vào trang quản lý cụm Kafka.
2. Tìm và nhấp vào nút "Xóa Cụm Kafka".
3. Xác nhận việc xóa cụm Kafka để tránh mất dữ liệu và chi phí không cần thiết.

