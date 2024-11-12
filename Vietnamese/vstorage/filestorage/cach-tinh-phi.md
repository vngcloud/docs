# Cách tính phí

Dịch vụ File Storage cung cấp hai phương thức thanh toán để phục vụ các mục tiêu và chiến lược tài chính khác nhau của từng khách hàng. Hai hình thức thanh toán được triển khai cho dịch vụ File Storage tại VNG Cloud bao gồm:

* Phương thức thanh toán Trả Trước.
* Phương thức thanh toán Trả Sau.

## **Cách Tính Phí File Storage**

Cách tính phí File Storage áp dụng chung cho cả 2 hình thức thanh toán, bao gồm Trả Trước và Trả Sau.

* **Đầu tiên, bạn sẽ được miễn phí sử dụng 50 GB/ 1 File Storage/ 1 Tháng.**
* **Tiếp theo, chi phí của việc sử dụng File Storage được tính dựa trên usage thực tế mà người dùng sử dụng trên File Storage đó.**
* **Giá trị Usage nhỏ nhất hệ thống ghi nhận là 1 TB, nếu cuối tháng, Usage của bạn sau khi đã trừ đi 50 GB Free có giá trị < 1 TB, hệ thống sẽ ghi nhận usage này là 1 TB và tính toán hóa đơn trên giá trị này.**

_<mark style="background-color:green;">Ví dụ: Bạn là KH sử dụng File Storage, bạn đã khởi tạo 3 file storage và sử dụng trong tháng với thông số:</mark>_&#x20;

* _<mark style="background-color:green;">File Storage A: Max quota = 1 TB, Usage trong toàn tháng = 48 GB => Do Usage trong tháng < 50 GB nên bạn sẽ không phát sinh chi phí trên file storage này.</mark>_
* _<mark style="background-color:green;">File Storage B: Max quota = 1 TB, Usage trong toàn tháng = 60 GB => Do ngoài 50 GB miễn phí, KH đã sử dụng 60 - 50 = 10 GB nên mức Usage hệ thống ghi nhận để tính toán là 1 TB (1024 GB).</mark>_
* _<mark style="background-color:green;">File Storage C: Max quota = 2 GB, Usage trong toàn tháng = 1100 GB => Do ngoài 50 GB miễn phí, KH đã sử dụng 1100 - 50 = 1050 GB nên mức Usage hệ thống ghi nhận để tính toán là 1050 GB.</mark>_

### **Phương thức thanh toán trả trước**

Đối với người dùng Trả Trước, VNG Cloud áp dụng hình thức Hold Credit - Tạm giữ Credit để hỗ trợ việc sử dụng cũng như tính chi phí cho dịch vụ File Storage. Tìm hiểu thêm về Hold Credit tại [Tạm giữ Credit](https://docs.vngcloud.vn/vng-cloud-document/vn/quan-ly-hoa-don-chi-phi-and-tai-nguyen-tren-vng-cloud/trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/thanh-toan/tam-giu-credit).

* **Hình thức**: Dưới phương thức Tạm giữ Credit, người dùng phải duy trì số dư trả trước đủ để chi trả phần sử dụng dịch vụ trong tài khoản của họ.
* **Quản lý số dư**: Người dùng có trách nhiệm quản lý số dư trả trước của họ để đảm bảo đủ để chi trả cho việc sử dụng file storage thep kế hoạch dự kiến, phần số dư này phải đủ để bao phủ cho việc sử dụng dịch vụ đến thời điểm hiện tại và 3 ngày tiếp theo đó. Chi tiết tham khảo tại [Tạm giữ Credit](https://docs.vngcloud.vn/vng-cloud-document/vn/quan-ly-hoa-don-chi-phi-and-tai-nguyen-tren-vng-cloud/trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/thanh-toan/tam-giu-credit).
* **Thông báo số dư thấp**: Để tránh gián đoạn dịch vụ, hệ thống sẽ gửi thông báo khi số dư trả trước giảm xuống dưới một ngưỡng cụ thể, khuyến nghị người dùng nạp thêm tiền. Trường hợp đã được nhắc nhở nhiều lần, nhưng số dư vẫn liên tục không đảm bảo, VNG Cloud sẽ tạm thời dừng cung cấp dịch vụ File storage đến người dùng.

### **Phương Thức Thanh Toán Trả Sau**

Đối với người dùng trả sau, VNG Cloud áp dụng hình thức sử dụng trước - trả tiền sau, tương tự các dịch vụ khác

* **Chu kỳ thanh toán**: Người dùng sử dụng phương thức thanh toán trả sau không cần duy trì số dư trả trước. Thay vào đó, các khoản phí dịch vụ File Storage được tính vào cuối mỗi chu kỳ thanh toán hàng tháng.
* **Tính linh hoạt trong việc sử dụng File Storage**: Với thanh toán trả sau, người dùng có thể kích hoạt & tạo file storage khi cần mà không cần quan tâm đến số dư khả dụng, cung cấp tính linh hoạt lớn hơn.
* **Hóa đơn thanh toán hàng tháng**: Các khoản phí dịch vụ file storage được liệt kê trên bảng kê thanh toán hàng tháng, cung cấp cho người dùng một bản tóm tắt rõ ràng về các chi phí liên quan đến bản file storage.
* **Thanh toán đúng hạn**: Thanh toán đúng hạn hóa đơn hàng tháng là rất quan trọng để đảm bảo truy cập liên tục vào dịch vụ file storage.
* **Theo dõi sử dụng**: Người dùng có thể theo dõi việc sử dụng file storage của mình thông qua cổng thanh toán, giúp họ nắm bắt chi phí và việc sử dụng tài nguyên.
