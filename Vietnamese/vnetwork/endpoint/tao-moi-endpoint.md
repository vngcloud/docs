---
description: VNG Cloud Endpoint là điểm kết nối giữa VPC với các dịch vụ của VNG Cloud
---

# Tạo mới Endpoint

## Làm thế nào để tạo

{% hint style="danger" %}
**Lưu ý quan trọng:**

* Trong cùng một **Region**, người dùng có thể tạo nhiều **Endpoint** trong một **VPC**.
* Nếu **VPC hỗ trợ DNS** và **“Bật tên DNS riêng”** được bật, **không cần cấu hình host** thủ công.
* DNS nội bộ sẽ tự động phân giải tên miền dịch vụ đến IP nội bộ của Endpoint.
* Nếu **không bật** tùy chọn này hoặc **VPC không hỗ trợ DNS**, cần **thêm bản ghi host thủ công**.
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

### **1/ Đối với Endpoint được tạo mà VPC không có hỗ trợ DNS**

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

Thêm bản ghi host trên các máy chủ cần truy cập dịch vụ qua  Endpoint Service

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FH7ovuNeYajOMMFAW87q3%252Fimage.png%3Falt%3Dmedia%26token%3Da1f68119-95fc-46aa-b0db-c9ae80d2ba14&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1e34008f&#x26;sv=2" alt=""><figcaption><p>Add host</p></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FedY062hUCSIow53Eb8lO%252Fimage.png%3Falt%3Dmedia%26token%3D2c362fdd-1732-4715-a0fd-2fd07c668c02&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4c94202b&#x26;sv=2" alt=""><figcaption><p>Result</p></figcaption></figure>

### **2/ Đối với Endpoint được tạo mà VPC có hỗ trợ DNS**

Khi sử dụng Private Endpoint, khách hàng có thể truy cập các dịch vụ của VNG Cloud thông qua mạng riêng thay vì qua Internet công cộng. Đặc biệt, nếu Private Endpoint được **hỗ trợ DNS**, việc truy cập trở nên đơn giản và liền mạch hơn nhờ khả năng **ghi đè bản ghi DNS (A record)**.

#### Cơ chế hoạt động DNS với Private Endpoint

_**a. Tên miền riêng cho từng Endpoint**_

Khi một Private Endpoint được tạo ra với **hỗ trợ DNS**, hệ thống sẽ cấp phát cho endpoint đó **một tên miền riêng (unique domain)**. Tên miền này có thể được dùng để truy cập trực tiếp đến dịch vụ thông qua IP riêng của endpoint.

Ví dụ: tên miền riêng cho dịch vụ vStorage HCM03

> [https://enp-ccd7fa25-a617-4e87-a929-97a7c933c19c-vstorage-hcm03.vpce.vngcloud.vn](https://enp-ccd7fa25-a617-4e87-a929-97a7c933c19c-vstorage-hcm03.vpce.vngcloud.vn)

_**b. Tùy chọn "Bật tên DNS riêng"**_

Khi cấu hình Endpoint, nếu bật tùy chọn **"Bật tên DNS riêng"**, bạn có thêm một cách truy cập dịch vụ:

* Có thể sử dụng **domain chính của dịch vụ** như thông thường.
* Tuy nhiên, trong môi trường mạng có hỗ trợ DNS override (ví dụ: VPC có tích hợp DNS nội bộ), bản ghi **A record** của domain chính sẽ được **ghi đè (override)** và trỏ về **IP nội bộ của Private Endpoint** thay vì IP công cộng.
* Trong mỗi VPC, người dùng chỉ được phép tạo **một Endpoint duy nhất có bật tùy chọn "Tên DNS Riêng" (Enable Private DNS)** cho mỗi dịch vụ.

Ví dụ: tên miền chính truy cập dịch vụ vStorage HCM03

> [https://hcm03.vstorage.vngcloud.vn](https://hcm03.vstorage.vngcloud.vn)

Điều này giúp bạn **giữ nguyên tên miền dịch vụ** nhưng vẫn đảm bảo **toàn bộ lưu lượng đi qua đường riêng (private network)**.

**Danh sách các dịch vụ và domain chính**

<table><thead><tr><th width="231.5078125">Dịch vụ</th><th>Domain chính</th></tr></thead><tbody><tr><td>IAM</td><td>iamapis.vngcloud.vn</td></tr><tr><td>vMonitor</td><td>monitoring-agent.vngcloud.vn</td></tr><tr><td>vCR</td><td>vcr.vngcloud.vn</td></tr><tr><td>Veeam</td><td>veeam-gw.vngcloud.vn</td></tr><tr><td>vServer</td><td>hcm3.api.vngcloud.vn</td></tr><tr><td>vStrorge (HCM03)</td><td>hcm03.vstorage.vngcloud.vn</td></tr><tr><td>vStorage (HCM04)</td><td>hcm04.vstorage.vngcloud.vn</td></tr></tbody></table>

