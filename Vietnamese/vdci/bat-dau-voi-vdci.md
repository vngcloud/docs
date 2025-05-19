# Bắt đầu với vDCI

**vDCI** là dịch vụ cung cấp máy chủ ảo chạy trên hạ tầng vật lý chuyên biệt (dedicated host), cho phép người dùng:

* Toàn quyền kiểm soát tài nguyên ảo hóa
* Hiệu năng ổn định nhờ không chia sẻ tài nguyên
* Đáp ứng các yêu cầu khắt khe về bảo mật, compliance hoặc license chuyên dụng (VDI, Windows Server v.v.)

## Hướng dẫn sử dụng dịch vụ vDCI

### **Bước 1: Liên hệ bộ phận kỹ thuật để cấp phát hạ tầng**

Để bắt đầu sử dụng dịch vụ vDCI, người dùng cần thực hiện bước chuẩn bị ban đầu như sau:

1. **Liên hệ bộ phận kỹ thuật hoặc Customer Success** để gửi yêu cầu sử dụng dịch vụ vDCI[ tại đây](https://helpdesk.vngcloud.vn/portal/en/home).
2. Trong yêu cầu cần nêu rõ:
   * Dự kiến số lượng máy ảo cần sử dụng
   * Yêu cầu cấu hình (vCPU, RAM, Disk, GPU nếu có)
   * Mục đích sử dụng (VDI, Dev/Test, Production, v.v.)
3. Bộ phận kỹ thuật sẽ:
   * Cấp phát Dedicated Host tương ứng
   * Cấu hình mạng nội bộ (Priavte Network) và CIDR tương ứng
   * Cấp quyền truy cập vào Portal theo tài khoản cụ thể
4. Sau khi hạ tầng đã sẵn sàng, người dùng sẽ nhận thông báo và có thể bắt đầu sử dụng thông qua Portal.

> Lý do cần liên hệ trước: vDCI chạy trên tài nguyên **dedicated vật lý**, cần được cấp phát và cấu hình theo nhu cầu riêng biệt, không hoạt động theo mô hình self-service 100%.

### **Bước 2: Đăng nhập Portal và Kiểm tra tài nguyên**

Sau khi được cấp quyền, người dùng đăng nhập vào Portal và kiểm tra các cấu hình phần cứng theo thông tin dưới đây:

* Truy cập vDCI Portal tại đây: [https://vdci.console.vngcloud.vn/overview](https://vdci.console.vngcloud.vn/overview)
* Tại mục Dedicated Cloud Instance bên menu bên trái, chọn mục Flavor để kiểm tra danh sách cấu hình phần cứng được cấp phát tại đây: [https://vdci.console.vngcloud.vn/dedicated-cloud-instance/flavor](https://vdci.console.vngcloud.vn/dedicated-cloud-instance/flavor)

### **Bước 3: Khởi tạo Network**

1. Truy cập Portal → **Network**
2. Nhấn **Tạo Mạng (Create Network)**
3. Nhập:
   * **Tên mạng**: để dễ phân biệt (ví dụ: `vnet-project-a`)
4. Nhấn **Xác nhận**

> **CIDR sẽ được VNG Cloud tự động cấp phát.**\
> Nếu bạn có yêu cầu CIDR cụ thể hãy liên hệ bộ phận kỹ thuật để được hỗ trợ tùy chỉnh.

### **Bước 4: Tạo Dedicated Cloud Instance (vDCI Instance)**

Để đảm bảo instance được khởi tạo có thể truy cập và cấu hình ngay từ đầu, bạn cần chuẩn bị một trong hai loại thông tin sau trước khi thực hiện khởi tạo:

**Lựa chọn 1: Chế độ Thông tin cơ bản (Basic mode)**

* Yêu cầu: Phải khởi tạo SSH Key trước để truy cập máy qua SSH.
* Cách tạo SSH Key: Truy cập portal vServer để khởi tạo/import SSH Key [tại đây](https://hcm-3.console.vngcloud.vn/vserver/v-server/ssh-key)

**Lựa chọn 2: Chế độ Thông tin người dùng (User Data mode)**

* Tham khảo thêm User Data mode [tại đây](https://docs.vngcloud.vn/vng-cloud-document/vn/vserver/compute-hcm03-1a/trai-nghiem-san-pham-vserver/userdata)

**Sau khi đã chuẩn bị SSH Key hoặc User Data, điền các thông tin sau để khởi tạo DCI:**

#### 1. **Name (Tên máy chủ)**

* **Mục đích**: Đặt tên định danh cho máy vDCI, giúp dễ quản lý và phân biệt giữa các máy.
* **Yêu cầu**:
  * Tên không trùng với các instance đang tồn tại trong cùng tài khoản
  * Thường viết không dấu, không có ký tự đặc biệt
* **Ví dụ**: `webserver-01`, `db-prod`, `test-vm-001`

#### 2. **OS Image (Hệ điều hành)**

* **Mục đích**: Chọn hệ điều hành để cài đặt cho máy chủ khi khởi tạo.
* **Tùy chọn phổ biến**:
  * Ubuntu (20.04, 22.04)
  * CentOS
  * Windows Server (2019, 2022)
* **Lưu ý**: Một số image yêu cầu license (ví dụ: Windows), hệ thống sẽ tính phí tương ứng nếu áp dụng.

#### 3. **Flavor (Cấu hình phần cứng)**

* **Mục đích**: Chọn cấu hình tài nguyên cho máy chủ (GPU, vCPU, RAM, Disk)
* **Ý nghĩa**: Flavor đại diện cho nhóm cấu hình phần cứng được phép sử dụng trong dự án hoặc tenant
* **Ví dụ**:
  * `vDCI.small`: 2 vCPU, 4GB RAM, 50GB SSD
  * `vDCI.medium`: 4 vCPU, 8GB RAM, 100GB SSD
  * `vDCI.gpu.1`: 8 vCPU, 32GB RAM, 1 GPU

> - Tham khảo danh sách cấu hình khả dụng [tại đây](cau-hinh-kha-dung.md).&#x20;
> - Nếu bạn không thấy flavor phù hợp, liên hệ bộ phận kỹ thuật để được cấp thêm.

#### 4. **Cài đặt mạng (Networking)**

**a. Chọn Network**

* **Mục đích**: Xác định mạng nội bộ mà máy vDCI sẽ kết nối
* **Ý nghĩa**: Giúp máy chủ có thể giao tiếp nội bộ hoặc truy cập Internet
* **Lưu ý**: Mạng này đã được kỹ thuật tạo sẵn hoặc bạn có thể tự khởi tạo (CIDR cấp tự động)

**b. Public IP (Bật / Tắt)**

* **Mục đích**: Xác định xem máy vDCI có cần IP công cộng để truy cập từ Internet hay không
* **Trường hợp bật**:
  * Dành cho các máy cần truy cập SSH/Remote từ xa
  * Máy chủ web/public API
* **Trường hợp tắt**:
  * Máy nội bộ, backend, hoặc máy test/dev không cần expose ra Internet

> Gợi ý: Tắt IP Public nếu chỉ dùng private hoặc quản lý qua bastion host để tăng bảo mật.

#### 5. **Chế độ khởi tạo truy cập (Access Mode)**

Người dùng bắt buộc chọn **một trong hai chế độ** để truy cập vào máy chủ sau khi khởi tạo:

**a. SSH Mode**

* **Yêu cầu**: Chọn một SSH Key đã được upload trước đó
* **Tác dụng**: Hệ thống sẽ gán public key vào máy để bạn có thể SSH ngay sau khi máy chạy
* **Phù hợp với**: Hầu hết người dùng kỹ thuật, đơn giản và an toàn

**b. User Data Mode**

* **Yêu cầu**: Nhập một đoạn script (cloud-init hoặc shell script) để cấu hình máy chủ
* **Tác dụng**: Dùng để tự động tạo user, cài phần mềm, thiết lập dịch vụ
* **Phù hợp với**: Các hệ thống có pipeline tự động hóa, cần bootstrap cấu hình phức tạp

> Một trong hai mode này **phải được cung cấp** trước khi nhấn "Create". Nếu không, hệ thống sẽ báo lỗi.

