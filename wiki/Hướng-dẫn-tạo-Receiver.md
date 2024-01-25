Receiver là tính năng cho phép bạn Scale (IN / OUT) 1 Group bằng web hook.

 **Bước 1:**  Tại giao diện Auto-scaling group chọn 1 group bạn muốn dùng receiver

![](images/storage/image2019-5-24_0-4-53.png)

 **Bước 2**  Chọn receiver -> Create receiver

![](images/storage/image2019-5-24_0-5-4.png)

 **Bước 3:**  Nhập tên receiver và Loại Acion. Hiện tại có 2 Action là

-          CLUSTER_SCALE_IN : Giảm instance, mỗi lần giảm 1 nếu không có gắn scaling policy

-          CLUSTER_SCALE_OUT: Tăng instance, mỗi lần tăng 1 nếu không có gắn scaling policy

![](images/storage/image2019-5-24_0-5-18.png)

Chọn receiver để tạo, sau khi tạo thành công bạn sẽ thấy Receiver như hình dưới.

![](images/storage/image2019-5-24_0-5-32.png)

Để có thể kích hoạt (trigger) được webhook url này bạn cần những thông tin sau:

 + Web hook url: thông tin đường dẫn để bạn gọi vào, bạn lấy bằng cách nhấn vào “Copy channel”

 + User_id: thông tin định danh account, bạn lấy bằng cách truy cập vào [https://portal.vngcloud.vn/account.html](https://portal.vngcloud.vn/account.html) tại trường Account id.

 + Access key: thông tin xác thực, bạn liên hệ với chúng tôi để được cung cấp

 Ví dụ bạn có những thông tin như dưới đây:

 + Web hook url: [https://example.vinadata.vn/v1/example/6e88c3f851dc4f48b11276c79a847d1c/receiver/81935b94-fc5c-4d06-869f-61aaaa4797e6/scale?backend=4](https://sdn-vsr-api.vinadata.vn/v1/senlin/6e88c3f851dc4f48b11276c79a847d1c/receiver/81935b94-fc5c-4d06-869f-61aaaa4797e6/scale?backend=4)

 + user_id: 47777

 + access_key: 89fa022b-6c44-43f2-b51c-3b332fbbf462

Bạn có thể sử dụng curl để kích hoạt mở rộng

curl -H 'Content-type: application/json' -H 'user_id:46677-H 'access_key: 89fa3452b-6345-43f2-0000-3b332fbbf462' -XPOST '[https://example.vinadata.vn/v1/example/6e88c3f851dc4f48b11276c79a847d1c/receiver/81935b94-fc5c-4d06-869f-61aaaa4797e6/scale?backend=4](https://sdn-vsr-api.vinadata.vn/v1/senlin/6e88c3f851dc4f48b11276c79a847d1c/receiver/81935b94-fc5c-4d06-869f-61aaaa4797e6/scale?backend=4)'







*****

[[category.storage-team]] 
[[category.confluence]] 
