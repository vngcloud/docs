Tại giao diện Policy management, chọn create Policy

![](images/storage/image2019-5-23_23-58-51.png)

 **Bước 1:**  Tại Policy configuration, nhập các thông tin cần thiết

![](images/storage/image2019-5-23_23-59-5.png)

-           **Policy name:** cho phép đặt các ký tự (a-z, A-Z, 0-9, '_'), bắt đầu với chữ và giới hạn từ 6-20 ký tự

-           **Policy description** : Nhập mô tả policy, phần mô tả này tùy theo nhu cầu quản lý policy của bạn, không ảnh hưởng đến cách thức hoạt động của policy.

-           **Policy type** : Có 2 dạng policy là


*  **Load balancer policy** : Policy này giúp bạn define các giá trị của load balancer và tự động thêm các instance được tạo ra vào pool tương ứng.

![](images/storage/image2020-6-30_10-0-17.png)


* Bạn sẽ cần chọn Load Balancer policy thuộc Network nào, sau đó hệ thống sẽ tự động liệt kê ra tất cả Load Balancers thuộc Network đó và tất cả Pool ID của Load Balancer vừa chọn
*  **Policy scaling:** Thiết lập các đặc tính của hành động scale instance. Hiện scaling type chỉ hỗ trợ dạng Change_In_Capacity (thay đổi số lượng instance) với 2 dạng Event là
    * CLUSTER_SCALE_IN: Giảm số lượng Instance trong Group

    

CLUSTER_SCALE_OUT: Tăng số lượng Instance trong Group

![](images/storage/image2019-5-23_23-59-32.png)

-           **Number:**  Số instance scale mỗi lần

-           **Cooldown:**  Đơn vị tính là giây (S), đây là thời gian ngắt quãng giữa mỗi lần scale.

Sau khi thiết lập xong, nhấn NEXT để tiếp tục

 **Bước 2 Summary** . Kiểm tra lại các thông tin của policy. Lưu ý các cấu hình của Policy sẽ không thể edit sau này.

Nhấn configure policy để tạo policy

![](images/storage/image2019-5-23_23-59-55.png)

Sau khi tạo thành công, bạn sẽ thấy policy vừa tạo xuất hiện ở giao diện quản lý

![](images/storage/image2019-5-24_0-0-5.png)



*****

[[category.storage-team]] 
[[category.confluence]] 
