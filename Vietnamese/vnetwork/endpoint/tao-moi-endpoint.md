---
description: VNG Cloud Endpoint là điểm kết nối giữa VPC với các dịch vụ của VNG Cloud
---

# Tạo mới Endpoint

## Làm thế nào để tạo

{% hint style="danger" %}
**Lưu ý quan trọng:**

_Trong cùng một region, người dùng có thể tạo nhiều Endpoint trong một VPC. Nếu **"Bật tên DNS riêng"** được bật khi tạo Endpoint, không cần add host. Ngược lại, phải add host thủ công để sử dụng Endpoint_
{% endhint %}

* Người dùng login vào  [https://hcm-3-vnetwork.console.vngcloud.vn/endpoint/list](https://hcm-3-vnetwork.console.vngcloud.vn/endpoint/list)  với region = HCM
* Chọn menu “**Endpoint**” tại thanh menu bên trái màn hình
* Chọn chức năng “**Create an Endpoint**”
* Nhập thông tin **Endpoint** theo yêu cầu gồm:

&#x20;         \- **Tên Endpoint**: Tên Endpoint

&#x20;         \- **Chọn Region/Zone**: Chọn region và Zone tương ứng (vd: HCM-1A, HCM-1B, ...)

&#x20;         \- **Chọn dịch vụ**: Chọn một dịch vụ của VNG Cloud mà Endpoint kết nối đến trong danh sách các dịch vụ vServer, vStorage, vMonitor, vCR, IAM.     &#x20;

&#x20;         \- **Service Package**: Gói dịch vụ Endpoint cung cấp mặc định cấu hình 1 gói Standard, người dùng không cần chọn gói dịch vụ

* Chọn VPC, Subnet muốn kết nối với các dịch vụ của VNG Cloud qua service endpoint
* Nếu VPC có hỗ trợ DNS, tùy chọn "Bật tên DNS riêng" sẽ bật để chọn. Nếu bật tùy chọn này thì khi truy cập dịch vụ không cần phải addhost, domain sẽ tự phân giải bởi dịch vụ DNS.
* Nếu VPC không hỗ trợ DNS, tùy chọn "Bật tên DNS riêng" sẽ mặc định tắt. Cần phải addhost để có thể truy cập được dịch vụ.
* Kiểm tra thông tin giá dịch vụ tại “**Summary**”
* Nhấn “**CREATE ENDPOINT**”

&#x20;Người dùng sẽ chờ hệ thống tạo Endpoint cho đến khi hoàn tất. Khi Endpoint được tạo thành công, trên màn hình danh sách Endpoint, người dùng thấy Endpoint xuất hiện tại đây.

## Cách sử dụng <a href="#how-to-use" id="how-to-use"></a>

**Đối với Endpoint được tạo mà VPC không có hỗ trợ DNS**

Trong trường hợp VPC không được cấu hình hỗ trợ dịch vụ DNS, tùy chọn **“Bật tên DNS riêng” (Enable Private DNS)** sẽ **không khả dụng** khi tạo Endpoint. Điều này dẫn đến việc **phân giải tên miền tự động thông qua DNS sẽ không được thực hiện**, và người dùng sẽ **không thể truy cập Endpoint Service ngay sau khi tạo Endpoint**.

Hướng dẫn cấu hình thủ công để truy cập Endpoint Service:

Để thiết lập quyền truy cập riêng tư từ máy chủ của bạn đến Endpoint Service trong trường hợp này, vui lòng thực hiện các bước sau:

1. **Truy cập trang quản lý Endpoint**
   * Điều hướng đến danh sách Endpoint đã tạo.
   * Chọn Endpoint tương ứng mà bạn muốn cấu hình.
2. **Xác định thông tin cần thiết**\
   Tại trang chi tiết Endpoint, hệ thống sẽ hiển thị hai thông tin quan trọng:
   * **Endpoint URL**: Đây là tên miền dịch vụ công khai dùng để truy cập thông qua Endpoint Service.
   * **Endpoint IP**: Là địa chỉ IP nội bộ được gán cho Endpoint Service.
3. **Cấu hình bản ghi host trên máy chủ**
   * Trên máy chủ cần truy cập dịch vụ, thêm một bản ghi vào tệp `/etc/hosts` (Linux/macOS) hoặc `C:\Windows\System32\drivers\etc\hosts` (Windows).
   *   Bản ghi có định dạng:

       ```
       <Endpoint IP>    <Endpoint URL>
       ```

       Ví dụ:

       ```
       10.0.5.123    service.example.internal
       ```
   * Lưu thay đổi và xác minh rằng truy vấn đến tên miền dịch vụ hiện đã được định tuyến đúng qua Endpoint IP.

> ✅ **Lưu ý:** Việc thêm bản ghi host chỉ cần thực hiện trên các máy chủ nằm trong cùng VPC hoặc có định tuyến mạng phù hợp đến Endpoint Service.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FMmsmN65yCpwVKxtPZwUL%252Fimage.png%3Falt%3Dmedia%26token%3Dd2b58bd9-7cad-4166-8c77-bed404188907&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c2e20add&#x26;sv=2" alt=""><figcaption><p>Endpoint List</p></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fk9wUuwK8MUUV9Hw4gq1k%252Fimage.png%3Falt%3Dmedia%26token%3Da9294a84-308a-40d3-b0c4-0afa2acbdf03&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=a45880d0&#x26;sv=2" alt=""><figcaption><p>Endpoint Detail</p></figcaption></figure>

\=

Thêm bản ghi host trên các máy chủ cần truy cập dịch vụ qua  Endpoint Service

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FH7ovuNeYajOMMFAW87q3%252Fimage.png%3Falt%3Dmedia%26token%3Da1f68119-95fc-46aa-b0db-c9ae80d2ba14&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1e34008f&#x26;sv=2" alt=""><figcaption><p>Add host</p></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FedY062hUCSIow53Eb8lO%252Fimage.png%3Falt%3Dmedia%26token%3D2c362fdd-1732-4715-a0fd-2fd07c668c02&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4c94202b&#x26;sv=2" alt=""><figcaption><p>Result</p></figcaption></figure>

**Đối với Endpoint được tạo có bật tùy chọn "Bật tên DNS riêng"**

Khi sử dụng Endpoint Service, khách hàng **không cần cấu hình thủ công các bản ghi `host` trên máy chủ** để truy cập dịch vụ. Hệ thống DNS sẽ tự động thực hiện phân giải tên miền, đảm bảo việc truy cập được liền mạch và đơn giản hóa quá trình cấu hình.

Trong mỗi VPC, người dùng chỉ được phép tạo **một Endpoint duy nhất có bật tùy chọn "Tên DNS Riêng" (Enable Private DNS)** cho mỗi dịch vụ. Khi tùy chọn này được kích hoạt:

* Hệ thống sẽ **tự động ghi đè bản ghi DNS công khai** của tên miền dịch vụ bằng địa chỉ IP nội bộ tương ứng trong VPC.
* Nhờ đó, các truy vấn DNS từ các tài nguyên trong VPC đến tên miền dịch vụ sẽ được **định tuyến qua Endpoint nội bộ**, thay vì sử dụng địa chỉ IP công khai.

> ⚠️ **Lưu ý:** Cơ chế ghi đè DNS chỉ có hiệu lực **bên trong VPC** và **không ảnh hưởng đến các truy vấn DNS bên ngoài mạng nội bộ**.

Ngoài ra, trong trường hợp **không bật tùy chọn “Tên DNS Riêng”**, người dùng vẫn có thể tạo nhiều Endpoint cho cùng một dịch vụ. Mỗi Endpoint như vậy sẽ được gán một **tên miền truy cập riêng biệt**, do hệ thống tự động cấp phát, và có thể được sử dụng để truy cập dịch vụ thông qua địa chỉ cụ thể đó.
