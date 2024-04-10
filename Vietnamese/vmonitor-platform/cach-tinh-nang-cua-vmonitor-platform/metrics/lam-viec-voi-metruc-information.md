# Làm việc với Metric Information

### Xem danh sách các metrics đang tồn tại

Sau khi bạn thiết lập thành công Metric Agent trên Server hoặc bạn đã sử dụng các Product Metric khác, lúc này bạn có thể xem thông tin các thông số metrics được đẩy về hệ thống vMonitor Platform bằng cách:

1. Đăng nhập vào [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). Nếu bạn chưa có tài khoản, đăng ký miễn phí tại [tại đây](https://register.vngcloud.vn/signup).
2. Chọn thư mục **Metric.**
3. Chọn **Information**.
4. Hệ thống hiển thị danh sách các **metrics** được đẩy về trong đó:&#x20;

* Metric name: tên của metric được đẩy về.&#x20;
* Metric Unit: đơn vị tính của metric tương ứng.
* Description: mô tả ý nghĩa của metric tương ứng nếu có.

![](http://docs.vngcloud.vn/download/attachments/49651188/image2023-7-31\_13-28-15.png?version=1\&modificationDate=1690784897000\&api=v2)

***

### Xem thông tin chi tiết metric

Để xem thông tin chi tiết một metric được đẩy về vMonitor Platform, hãy làm theo hướng dẫn bên dưới:&#x20;

1. Đăng nhập vào [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). Nếu bạn chưa có tài khoản, đăng ký miễn phí tại [tại đây](https://register.vngcloud.vn/signup).
2. Chọn thư mục **Metric.**
3. Chọn **Information**.
4. Chọn vào **metric** mà bạn muốn xem thông tin chi tiết. Lúc này hệ thống sẽ hiển thị **Metadata** và **Dimensions** của metric này.&#x20;

<figure><img src="http://docs.vngcloud.vn/download/attachments/49651188/image2023-7-31_13-29-43.png?version=1&#x26;modificationDate=1690784984000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Trong đó**:**
  * **Metadata**
    * Unit: đơn vị số liệu của metric. Bạn có thể chỉnh sửa đơn vị tính này về một trong các giá trị mà chúng tôi cung cấp bao gồm: %, bytes, bytes/s, MB, ms, nanosecond, requests/s, seconds, short, short/ms.
    * Description: mô tả ý nghĩa hoặc đặc điểm của metric.
*
  * **Dimensions**: các thông tin về đặc điểm hoặc nguồn của metrics và được quản lý dưới dạng key-value.
    * Dimension key: khóa của dimension: dimension key là duy nhất trên một metric.
    * Dimension value: giá trị tương ứng của dimention key, 1 dimension key có thể có nhiều dimension value.

***

### Chỉnh sửa thông tin metric

Bạn có thể chỉnh sửa thông tin metadata của một metric bằng cách:&#x20;

1. Đăng nhập vào [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). Nếu bạn chưa có tài khoản, đăng ký miễn phí tại [tại đây](https://register.vngcloud.vn/signup).
2. Chọn thư mục **Metric.**
3. Chọn **Information.**
4. Chọn **Metric** bạn muốn chỉnh sửa.
5. Tại **Metric** mà bạn muốn chỉnh sửa, chọn ![](http://docs.vngcloud.vn/download/thumbnails/49651188/image2023-4-24\_13-59-30.png?version=1\&modificationDate=1690785247000\&api=v2).&#x20;
6. Chỉnh sửa **metadata** của metric mà bạn mong muốn. **Metadata** của metric bao gồm:

* **Unit**: đơn vị tính của metric, bạn có thể chọn 1 trong các giá trị %, bytes, bytes/s, MB, ms, nanosecond, requests/s, seconds, short, short/ms.
* **Description**: nhập mô tả ý nghĩa hoặc đặc điểm của metric.

7\. Chọn **Save.**

8\. Sau khi bạn đã thực hiện thay đổi thông số **metadata** của **metric**, bạn cũng có thể thực hiện khôi phục lại cấu hình **metadata** ban đầu bằng cách chọn ![](http://docs.vngcloud.vn/download/attachments/49651188/image2023-4-24\_13-59-30.png?version=1\&modificationDate=1690785247000\&api=v2)sau đó chọn ![](http://docs.vngcloud.vn/download/thumbnails/49651188/image2023-4-24\_14-20-7.png?version=1\&modificationDate=1690785248000\&api=v2)**.**

\
