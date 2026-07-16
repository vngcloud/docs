# Xóa NAT

1. Đăng nhập vào [https://hcm-3-vnetwork.console.greennode.ai/nat/list](https://hcm-3-vnetwork.console.greennode.ai/nat/list) với region là HCM.
2. Trong menu **"**&#x50;ublic NAT Instanc&#x65;**"**, tìm và chọn NAT bạn muốn xóa.
3. Nhấn chuột phải và chọn mục **"**&#x44;elet&#x65;**"**.
4. Một màn hình cảnh báo sẽ hiện ra với nội dung "Deleting NAT may have some consequences for the user." Nhấn **"**&#x44;elet&#x65;**"** để xác nhận xóa NAT.

{% hint style="danger" %}
Khi một NAT V2 bị xóa, route mặc định ra internet đã được tự động thêm vào route table của VPC lúc tạo NAT cũng sẽ bị gỡ bỏ. Sau khi xóa, các máy ảo trong subnet sẽ không còn ra internet qua NAT này nữa.
{% endhint %}

