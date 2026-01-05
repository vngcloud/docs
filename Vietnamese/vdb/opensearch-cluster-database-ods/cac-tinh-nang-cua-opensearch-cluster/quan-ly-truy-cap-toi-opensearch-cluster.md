# Quản lý truy cập tới OpenSearch Cluster

Trong dịch vụ **vDB OpenSearch** của **GreenNode**, bạn có thể truy cập OpenSearch theo hai cách:

* **Đăng nhập vào OpenSearch Dashboard** để quản lý và phân tích dữ liệu.
* **Đẩy log vào OpenSearch Cluster** để lưu trữ và xử lý log.

Chúng tôi cung cấp **hai endpoint với các port khác nhau**, nhưng **dùng chung tài khoản Master User** để thực hiện cả hai tác vụ.

## Truy Cập OpenSearch Dashboard

Để đăng nhập vào giao diện quản lý OpenSearch, sử dụng thông tin sau:

* **Endpoint:** `https://your-cluster-name-hcm03.vdb-opensearch.vngcloud.vn`
* **Port:** `443`
* **Username:** `master-user`
* **Password:** (Mật khẩu bạn đã thiết lập)

Sử dụng trình duyệt để truy cập URL trên và đăng nhập bằng tài khoản Master User.

## Đẩy Log Vào OpenSearch Cluster

Để gửi log vào hệ thống OpenSearch, sử dụng thông tin sau:

* **Endpoint:** `https://your-cluster-name-hcm03.vdb-opensearch.vngcloud.vn`
* **Port:** `9200`
* **Username:** `master-user`
* **Password:** (Mật khẩu bạn đã thiết lập)

{% hint style="info" %}
**Chú ý:**

* Hiện tại, chúng tôi chỉ hỗ trợ **1 mode public endpoint**, có nghĩa là mặc định nếu bạn không thiết lập Allowed CIDRS thì **bất kỳ ai có thông tin tài khoản Master User** đều có thể truy cập cluster. Để giới hạn quyền truy cập, bạn có thể **cấu hình danh sách IP được phép (Allow CIDRs)** trên cluster theo hướng dẫn bên dưới.
{% endhint %}

## Kiểm soát truy cập vào OpenSearch Dashboard/ đẩy logs vào OpenSearch Cluster

Bạn có thể kiểm soát truy cập... bằng cách:

* Khi khởi tạo OpenSearch Cluster, tại mục Network setting, nhập CIDRs bạn mong muốn truy cập vào Dashboard hoặc đẩy log. Các CIDR có thể ngăn cách bằng dấu phẩy, ví dụ 10.192.168.8/16, 10.192.160.10/24
* Khi một OpenSearch Cluster đã được khởi tạo, bạn có thể chỉnh sửa bằng cách vào chi tiết một Cluster, tại mục Connectivity & Security chọn nút Edit tại ô Allowed CIDRs trên từng mục Dashboard hay Receive Logs

Dưới đây là phiên bản hướng dẫn hoàn chỉnh, bổ sung thông tin về cách kiểm soát truy cập OpenSearch một cách rõ ràng và dễ hiểu:

### **Thiết Lập CIDRs Khi Khởi Tạo Cluster**

Khi tạo mới OpenSearch Cluster, bạn có thể định cấu hình CIDRs bằng cách:

* Tại mục **Network Setting** trong giao diện khởi tạo cluste&#x72;**, Nhập danh sách CIDRs** mà bạn muốn cấp quyền truy cập vào **Dashboard** hoặc **Receive Logs**. Các CIDRs cách nhau bằng dấu phẩy (`,`). Ví dụ: `10.192.168.8/16, 10.192.160.10/24`.

**Hoàn tất quá trình tạo Cluster**, các CIDRs này sẽ được áp dụng ngay lập tức.

### **Chỉnh Sửa CIDRs Sau Khi Cluster Đã Được Khởi Tạo**

Nếu bạn muốn thay đổi danh sách CIDRs sau khi cluster đã khởi tạo:

**Bước 1: Truy cập** vào OpenSearch Cluster cần chỉnh sửa.

**Bước 2: Vào tab** `Connectivity & Security`.

**Bước 3: Trên mục Accessibility:**

* Chọn **Edit** tại ô **Dashboard** để chỉnh sửa CIDRs truy cập giao diện quản lý.
* Chọn **Edit** tại ô **Receive Logs** để chỉnh sửa CIDRs cho endpoint nhận log.

**Bước 4: Nhập CIDRs mới** theo định dạng hợp lệ. Các CIDRs cách nhau bằng dấu phẩy (`,`). Ví dụ: `10.192.168.8/16, 10.192.160.10/24`.

**Bước 5: Nhấn Save** để cập nhật thay đổi.
