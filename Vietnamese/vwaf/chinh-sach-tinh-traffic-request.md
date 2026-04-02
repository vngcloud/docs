# Chính sách tính Traffic / Request

### 1. Tổng quan

Tài liệu này mô tả:

* Cách cấp quota traffic và request
* Cách hệ thống cộng và trừ quota
* Điều kiện ngắt dịch vụ
* Cách tính phí cho khách hàng prepaid và postpaid

### 2. Mô hình quản lý quota (Traffic Pool & Request Pool)

Hệ thống sử dụng 2 pool độc lập:

<table><thead><tr><th width="279.46484375">Pool</th><th>Mô tả</th></tr></thead><tbody><tr><td>Traffic Pool</td><td>Tổng dung lượng traffic (GB)</td></tr><tr><td>Request Pool</td><td>Tổng số lượng request</td></tr></tbody></table>

#### Nguyên tắc hoạt động

* Mỗi khách hàng có:
  * 1 Traffic Pool
  * 1 Request Pool
* Các pool được dùng chung cho toàn bộ application
* Không có quota riêng cho từng application

#### Cách cộng quota vào pool

Quota được cộng trong các trường hợp:

1. Khi tạo application:
   * +300 GB traffic
   * +3,000,000 request
2. Khi hệ thống cộng quota định kỳ hàng tháng
3. Khi khách hàng mua thêm:
   * Traffic → Traffic Pool
   * Request → Request Pool

#### Cách sử dụng pool

* Tất cả application dùng chung pool
* Usage từ bất kỳ application nào đều trừ vào pool tương ứng

### 3. Khách hàng trả trước (Prepaid)

#### 3.1. Quota mặc định

Mỗi application khi được tạo mới sẽ được cấp:

<table><thead><tr><th width="255.7421875">Loại</th><th>Giá trị</th></tr></thead><tbody><tr><td>Traffic</td><td>300 GB</td></tr><tr><td>Request</td><td>3,000,000</td></tr></tbody></table>

Lưu ý:

* Quota được cấp theo từng application
* Tuy nhiên toàn bộ quota được cộng vào pool tổng
* Không có quota riêng cho từng application

#### 3.2. Cơ chế cộng quota định kỳ

Hệ thống tự động cộng quota miễn phí vào đầu mỗi tháng (ví dụ 00:05).

Chi tiết:

* Mỗi application (domain) còn ở trạng thái Active sẽ được cấp thêm:
  * 300 GB traffic
  * 3,000,000 request
* Quota được cấp theo từng application nhưng cộng vào pool tổng

Điều kiện:

1. Application ở trạng thái Active
2. Application đã tồn tại ≥ 15 ngày

Công thức:

Thời điểm cộng – Ngày tạo ≥ 15 ngày

Lưu ý:

* Application không đủ điều kiện sẽ không được cộng quota
* Nếu có nhiều application đủ điều kiện, quota được cộng tương ứng theo số lượng application

#### 3.3. Cơ chế trừ traffic / request

Chu kỳ kiểm tra: mỗi 10 phút

* Nếu traffic ≥ 10 MB:
  * Trừ ngay traffic và request
* Nếu traffic < 10 MB:
  * Cộng dồn và trừ vào đầu ngày hôm sau

#### 3.4. Xử lý khi hết quota

Khi một trong hai pool (traffic hoặc request) giảm về 0, hệ thống xử lý như sau:

**Trường hợp A – Có lịch sử sử dụng**

Điều kiện:

* Có dữ liệu usage tháng trước

Cơ chế:

* Không ngắt ngay
* Cho phép sử dụng vượt quota

Giới hạn vượt:

* Traffic: tối đa 50% traffic tháng trước
* Request: tối đa 50% request tháng trước

Nếu vượt một trong hai giới hạn:

* Ngắt toàn bộ application

**Trường hợp B – Không có lịch sử sử dụng**

Áp dụng cho:

* Khách hàng mới
* Không đủ dữ liệu

Ngưỡng:

* Traffic > 1000 GB
* Request > 10,000,000

Nếu vượt một trong hai ngưỡng:

* Ngắt toàn bộ application

#### 3.5. Xóa application sớm

Nếu application bị xóa trước 15 ngày:

* Thu hồi quota khỏi pool:
  * 300 GB traffic
  * 3,000,000 request

### 4. Khách hàng trả sau (Postpaid)

#### 4.1. Nguyên tắc

* Tính phí vào cuối tháng
* Gọi T là số application

Hệ thống tạo T hóa đơn (1 application = 1 bill)

#### 4.2. Tổng usage

* m1: tổng traffic trong tháng
* m2: tổng request trong tháng

#### 4.3. Quota miễn phí

<table><thead><tr><th width="240.6484375">Loại</th><th>Công thức</th></tr></thead><tbody><tr><td>Traffic</td><td>T × 300 GB</td></tr><tr><td>Request</td><td>T × 3,000,000</td></tr></tbody></table>

#### 4.4. Traffic vượt quota

N1 = m1 − (T × 300 GB)

* Nếu N1 ≤ 0: không tính phí
* Nếu N1 > 0:

Chi phí = N1 × đơn giá / GB

#### 4.5. Request vượt quota

N2 = m2 − (T × 3,000,000)

* Nếu N2 ≤ 0: không tính phí
* Nếu N2 > 0:

Chi phí = (N2 / 1,000,000) × đơn giá / 1 triệu request

#### 4.6. Đơn vị

* 1 KB = 1000 Bytes
* 1 MB = 1000 KB
* 1 GB = 1000 MB

### 5. Khuyến nghị

* Theo dõi pool thay vì từng application
* Tránh tạo/xóa application liên tục
* Dùng postpaid nếu traffic biến động
