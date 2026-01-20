# Hạn mức dịch vụ

### Tổng quan

Trang **Quota** hiển thị các hạn mức sử dụng áp dụng cho các tính năng của WAF trong tài khoản của bạn.\
Các hạn mức này giúp kiểm soát số lượng rule và tài nguyên có thể cấu hình, đảm bảo hệ thống vận hành ổn định và công bằng.

Tùy theo từng loại tài nguyên, quota có thể được áp dụng **theo từng application** hoặc **theo tổng số application**.

***

### Phạm vi áp dụng Quota

#### Quota theo Application

Các quota sau được áp dụng **riêng cho từng application**:

#### Rate Limit Rules

* **Tối đa 2 rule Rate Limiting cho mỗi application**
* Mỗi application có quota Rate Limiting độc lập
* Rule Rate Limiting của application này không ảnh hưởng đến application khác

***

#### Allow & Deny Rules

* **Tối đa 10 rule Allow & Deny cho mỗi application**
* Mỗi application có quota Allow & Deny riêng biệt
* Rule của application này không tiêu thụ quota của application khác

***

#### Quota chứng chỉ (Theo số lượng Application)

Quota chứng chỉ được tính **dựa trên số lượng application**.

Áp dụng cho:

* **Chứng chỉ upload**
* **Chứng chỉ miễn phí**

***

### Cách tính Quota chứng chỉ

Quota chứng chỉ hoạt động theo các nguyên tắc sau:

* Mỗi application có thể gắn **1 chứng chỉ**\
  (chứng chỉ upload hoặc chứng chỉ miễn phí)
* **Tổng số chứng chỉ** bạn có thể upload hoặc cấp miễn phí **bằng với số application đã tạo**
* Chứng chỉ upload và chứng chỉ miễn phí **dùng chung cùng một quota**, dựa trên số application

#### Ví dụ

Nếu bạn tạo **10 application**, bạn có thể:

* Upload tối đa **10 chứng chỉ**, hoặc
* Cấp tối đa **10 chứng chỉ miễn phí**, hoặc
* Kết hợp cả hai, miễn sao không vượt quá tổng số **10 chứng chỉ**

***

### Lưu ý

* Quota Rate Limiting: **2 rule / application**
* Quota Allow & Deny: **10 rule / application**
* Quota chứng chỉ được tính **trên toàn bộ application**
