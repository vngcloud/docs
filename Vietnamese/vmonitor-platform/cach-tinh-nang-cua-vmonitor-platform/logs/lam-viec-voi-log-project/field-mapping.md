# Field mapping

Nếu Log mapping mang ý nghĩa là quy định lại về định danh của một số field trong dữ liệu log thì Field mapping là tính năng mà chúng tôi cung cấp nhằm giúp bạn **điều chỉnh kiểu dữ liệu của các field từ log đổ về** hệ thống vMonitor Platform.&#x20;

Để thay đổi loại dữ liệu phù hợp với các field từ log đổ về, hãy làm theo hướng dẫn bên dưới:&#x20;

1. Đăng nhập vào [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). Nếu bạn chưa có tài khoản, đăng ký miễn phí tại [tại đây](https://register.vngcloud.vn/signup).
2. Chọn thư mục **Log**.
3. Chọn **Field mapping.**
4. Tại đây, nếu kiểu dữ liệu ban đầu của field log là Number hoặc Date thì bạn có thể chỉnh sửa định dạng dữ liệu field này về kiểu dữ liệu mà bạn mong muốn. Loại dữ liệu ban đầu mà hệ thống của chúng tôi ghi nhận từ log sẽ được hiển thị tại cột Type. Tiếp tục chọn Chọn Edit field. Lúc này, sẽ có 2 trường hợp xảy ra:
   1. **Trường hợp 1:** Nếu bạn chỉnh sửa trên field có loại dữ liệu **Number**, hệ thống hiển thị màn hình Chỉnh sửa field. Bạn có thể chọn định dạng dữ liệu phù hợp với field mà bạn đang chọn. Ví dụ: Ở đây mặc định dữ liệu lượng traffic là dạng Number, lúc này trên dashboard hiển thị lượng traffic với định dạng số. Khi bạn chọn lại Format dữ liệu thành Bytes, thì trên dashboard sẽ hiển thị lượng traffic theo các đơn vị hệ byte như Gigabyte (GB), terabyte (TB),...Điều này sẽ dễ dàng cho bạn trong việc theo dõi Dashboard hơn.&#x20;

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. **Trường hợp 2**: Nếu bạn chỉnh sửa trên field có loại dữ liệu **Date**, hệ thống hiển thị màn hình Chỉnh sửa field. Chọn Format và Date format pattern phù hợp với field mà bạn đang chọn.

<figure><img src="https://docs.vngcloud.vn/download/attachments/49650644/image2023-4-27_9-41-40.png?version=1&#x26;modificationDate=1682563300000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

7\. Chọn **Save**.
