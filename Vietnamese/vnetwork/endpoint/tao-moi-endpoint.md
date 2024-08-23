# Tạo mới Endpoint

* Người dùng login vào [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/) với region = HCM
* Chọn menu “**Endpoint**” tại thanh menu bên trái màn hình
* Chọn chức năng “**Create an Endpoint**”
* Nhập thông tin **Endpoint** theo yêu cầu gồm:

&#x20;         \- **Tên Endpoint**: Tên Endpoint

&#x20;         \- **Chọn dịch vụ**: Chọn một dịch vụ của VNG Cloud mà Endpoint kết nối đến trong danh sách các dịch vụ vServer, vStorage, vMonitor, vCR, IAM.     &#x20;

&#x20;         \- **Service Package**: Gói dịch vụ Endpoint cung cấp mặc định cấu hình 1 gói Standard, người dùng không cần chọn gói dịch vụ

* Chọn VPC, Subnet muốn kết nối với các dịch vụ của VNG Cloud qua service endpoint
* Kiểm tra thông tin giá dịch vụ tại “**Summary**”
* Nhấn “**CREATE ENDPOINT**”

&#x20;Người dùng sẽ chờ hệ thống tạo Endpoint cho đến khi hoàn tất. Khi Endpoint được tạo thành công, trên màn hình danh sách Endpoint, người dùng thấy Endpoint xuất hiện tại đây.

_<mark style="color:blue;">Lưu ý</mark>_<mark style="color:blue;">:</mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">tại cùng một region, tương ứng với một VPC người dùng chỉ được tạo một Endpoint kết nối đến một dịch vụ của VNG Cloud xác định (vd: vStorage)</mark>_
