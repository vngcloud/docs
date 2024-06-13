# Tạo mới Public NAT

* Người dùng login vào [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/) với region = HCM
* Chọn menu “Public NAT Instance” tại thanh menu bên trái màn hình
* Chọn chức năng “Create a Public NAT”
* Nhập thông tin NAT theo yêu cầu gồm:
  * [ ] Tên NAT
  * [ ] Instance (Flavor)
  * [ ] Volume attach nếu có
  * [ ] VPC, Subnet
  * [ ] External Interface
* Kiểm tra thông tin giá dịch vụ tại phần “**Summary**”
* &#x20;Nhấn “**TẠO PUBLIC NAT**”

Khi NAT được tạo thành công, người dùng sẽ thấy NAT xuất hiện trên màn hình danh sách NAT.

Người dùng cần thực hiện bước cấu hình các VM nào sẽ đi qua NAT ra internet theo hướng dẫn trên màn hình chi tiết NAT.

_<mark style="color:blue;">Lưu ý:</mark>_ &#x20;

* _<mark style="color:blue;">Người dùng có thể vào danh sách Server tại trang “Server” để thực hiện các chức năng hỗ trợ cho server trên NAT.</mark>_ &#x20;
* _<mark style="color:blue;">Khi detach External Interface của NAT, các kết nối ra internet sẽ không hoạt động.</mark>_
* _<mark style="color:blue;">Khi detach External Interface hiện hành của NAT và Attach một</mark>_ _<mark style="color:blue;">External Interface mới vào NAT, Bạn phải re-config lại VPC/ VM theo IP của external interface mới vừa được attach vào.</mark>_
* _<mark style="color:blue;">Khi người dùng thay đổi vNetwork Image một cách có chủ đích, NAT sẽ không còn hoạt động.</mark>_
