# Gói Bandwidth Share

Gói bandwidth Share là gói bandwidth với tốc độ cao được chia sẻ cho nhiều khách hàng cùng sử dụng. Tốc độ của gói này có thể khác nhau tại các thời điểm trong ngày. **Gói này phù hợp cho các doanh nghiệp nhỏ hoặc các dự án không yêu cầu băng thông lớn và ổn định liên tục**. Nếu bạn chỉ cần băng thông để duy trì các hoạt động cơ bản và không có yêu cầu cao về hiệu suất mạng, đây là lựa chọn hợp lý nhất cho bạn.

### Xem thông tin chi tiết gói

**Bước 1**: Đăng nhập vào tài khoản VNG Cloud của bạn và truy cập vào [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/)

**Bước 2**: Trên danh sách menu bên trái, tại mục **Network**, chọn **Bandwidth**.

**Bước 3**: Trên danh sách các gói bandwidth có sẵn, chọn vào gói **Share.**

**Bước 4**: Lúc này, bạn có thể xem chi tiết gói bandwidth này. Tại màn hình này, bạn có thể:

* Thêm IP cho gói: bằng cách chọn vào biểu tượng **Thêm IP**, bạn có thể lựa chọn IP mà bạn muốn thêm vào gói bandwidth này. Chi tiết bạn có thể tham khảo ở mục bên dưới.
* Thêm tag cho gói: bằng cách nhập **Key, Value** và chọn biểu tượng **Thêm**, bạn có thể thêm tag đánh dầu cho gói bandwidth này.

{% hint style="info" %}
**Chú ý:**

* Đây là gói bandwidth mặc định được chúng tôi tự động tạo và thêm sẵn vào gói dịch vụ cho bạn, bạn không thể thực hiện xóa gói này hoặc thay đổi cấu hình gói này.
{% endhint %}

***

### Thêm địa chỉ IP cho gói

{% hint style="info" %}
**Chú ý:**

* Các IP có trạng thái ATTACHED có ý nghĩa là các IP này đã được gán vào 1 gói bandwidth bất kỳ nào đó. Khi bạn thực hiện thêm các IP có trạng thái ATTACHED này vào gói bandwidth của bạn, các IP này sẽ được gỡ khỏi gói cũ và gán lại vào gói mới này. **Điều này nhằm đảm bảo tại một thời điểm, một địa chỉ IP chỉ có thể được gán vào một gói bandwidth.**
{% endhint %}

Để thêm địa chỉ IP cho gói, bạn có thể thực hiện theo các bước:&#x20;

**Bước 1**: Đăng nhập vào tài khoản VNG Cloud của bạn và truy cập vào [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/)

**Bước 2**: Trên danh sách menu bên trái, tại mục **Network**, chọn **Bandwidth**.

**Bước 3**: Trên danh sách các gói bandwidth có sẵn, chọn vào gói **Share** tùy theo nhu cầu sử dụng của bạn.

**Bước 4**: Chọn biểu tượng **Action** sau đó chọn **Thêm IP** hoặc ở màn hình chi tiết gói, tại mục **Danh sách IP**, chọn biểu tượng **Thêm IP.**&#x20;

**Bước 5:** Màn hình **Thêm IP** được hiển thị, bạn có thể lọc danh sách IP theo từng loại bằng cách chọn một trong các phương án tại ô **Loại resource**. Hiện tại chúng tôi đang cung cấp cho bạn các loại resource bao gồm: **K8S, Floating IP, External Interface, vLB.**

**Bước 6**: Chọn một hoặc nhiều IP bằng cách chọn biểu tượng **Checkbox** và chọn **Thêm**. tượng **Thêm IP.**&#x20;

***

### Bỏ chọn địa chỉ IP cho gói

Để thêm địa chỉ IP cho gói, bạn có thể thực hiện theo các bước:&#x20;

**Bước 1**: Đăng nhập vào tài khoản VNG Cloud của bạn và truy cập vào [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/)

**Bước 2**: Trên danh sách menu bên trái, tại mục **Network**, chọn **Bandwidth**.

**Bước 3**: Trên danh sách các gói bandwidth có sẵn, chọn vào gói **Share** tùy theo nhu cầu sử dụng của bạn.

**Bước 4**: Tại mục **Danh sách IP**, chọn biểu tượng **Checkbox** tại địa chỉ IP bạn muốn bỏ khỏi gói và chọn biểu tượng **Loại bỏ**.

**Bước 5:** Tại màn hình xác nhận xóa IP, chọn **Xóa**.

{% hint style="info" %}
**Chú ý:**

* Khi bạn xóa một địa chỉ IP khỏi gói Share, địa chỉ IP này sẽ được gán lại vào gói bandwidth mặc định miễn phí **VNG Dedicated**.
{% endhint %}
