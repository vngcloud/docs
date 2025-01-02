# Kiểm tra kết nối của Active Directory Domain Controller, DNS Server trong VPC của bạn

## Tổng quan

Khi bạn thực hiện mapping File Storage với **Windows Server** có tích hợp **Active Directory**, cần đảm bảo rằng **Active Directory Domain Controller** và **DNS Server** của bạn đã được kết nối trên VPC/ Subnet của bạn. Với SMB File Storage, hệ thống vStorage đã tự động mở các port cần thiết cho việc kết nối trong VPC/ Subnet của bạn. Đối với Active Directory Domain Controller, DNS Server, bạn cần thực hiện mở các kết nối theo mô tả trong hình bên dưới:&#x20;



<figure><img src="../../../../../.gitbook/assets/image (922).png" alt="" width="563"><figcaption></figcaption></figure>

***

## Hướng dẫn kiểm tra kết nối

Giả sử, bạn đã khởi tạo:&#x20;

* **Windows Server**:
  * **Server name**: `my-window-server`
  * **DNS Domain**: `example.local`
  * **DA Domain Name**: `my-window-server.example.local`
  * **Forward Lookup Zone Name**: `example.local`
  * **DNS server IP addresses**: `10.50.3.10`
  * **Security Group**: Đã/ Chưa mở một số port cần thiết.
* **SMB File Storage**:
  * **File storage name**: `my-smb-file`
  * **IP Address**: `10.50.3.15`
  * **Security Group**: Hệ thống vStorage đã tự động mở các port cần thiết cho việc kết nối trong VPC/ Subnet của bạn.&#x20;

Bạn có thể kiểm tra việc kết nối này theo hướng dẫn sau:&#x20;

### **Bước 1: Truy cập vServer Portal** tại [đây ](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server).

### **Bước 2: Tạo CentOS Server**

* Chọn **Create a Server** và khởi tạo một server **CentOS** chạy **RockyOS phiên bản 8.0 trở lên**.
* Server này cần thuộc **cùng VPC và Subnet** với Windows Server của bạn.
* Mở quyền ra ngoài internet trong **Security Group** cho server.

<figure><img src="../../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### **Bước 3: Tải và chuẩn bị script kiểm tra**

* **SSH** vào **CentOS server** vừa tạo.
* Chạy lệnh sau để kiểm tra kết nối ra ngoài internet cũng như tải và cài đặt script `efs_check.sh`

```bash
curl -L "https://hcm04.vstorage.vngcloud.vn/efs-source/efs_check.sh" -o /usr/local/sbin/efs_check.sh && chmod +x /usr/local/sbin/efs_check.sh
efs_check.sh --help
```

Nếu **user** bạn đang sử dụng **không có quyền** tải script`efs_check.sh`, vui lòng chuyển qua dùng **root user** rồi thực hiện chạy curl thông qua lệnh:&#x20;

```bash
sudo -i
```

```bash
curl -L "https://hcm04.vstorage.vngcloud.vn/efs-source/efs_check.sh" -o /usr/local/sbin/efs_check.sh && chmod +x /usr/local/sbin/efs_check.sh
efs_check.sh --help
```

Nếu thành công, kết quả trả về như sau:&#x20;

```bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  5559  100  5559    0     0  28362      0 --:--:-- --:--:-- --:--:-- 28362
Usage: /usr/local/sbin/efs_check.sh [option...] {--install-packages|--check-dns|--check-AD}

  -h, --help              Show display information
  -i, --install-packages  Install packages samba and library for tool efs_check
                          Note: you network need access internet for download packages.
  --check-dns             Run check dns reachability
  --check-AD              Run check join Active Directory Domain Controller
```

### **Bước 4: Cấu hình thông tin kết nối**

* Cấu hình thông tin cần thiết cho script bằng lệnh:&#x20;

```bash
export \
HOST_NAME=<Bất kỳ tên nào mà bạn mong muốn> \
DOMAIN_NAME=<Forward Lookup Zone Name> \
IP_DNS=<DNS server IP addresses> \
USER_NAME=<Username> \
USER_PASS=<Password>
```

Ví dụ:

```bash
export \
HOST_NAME="VNG-CHECK-CONNECT" \
DOMAIN_NAME="example.local" \
IP_DNS="10.50.3.10" \
USER_NAME="Administrator" \
USER_PASS="987654321aA@"
```

### **Bước 5: Cài đặt các package cần thiết**

* Chạy lệnh sau để cài đặt:

```bash
efs_check.sh -i
```

### **Bước 6: Kiểm tra kết nối của DNS Server**

* Kiểm tra khả năng kết nối của DNS Server bằng lệnh:

```bash
efs_check.sh --check-dns
```

Nếu thành công, kết quả trả về như sau:&#x20;

```lua
Checking DNS reachability:
nameserver 10.50.3.10
search example.local
Result:
IP DNS 10.50.3.10 reachable
example.local has address 10.50.3.10
```

Nếu thất bại, kết quả trả về là:&#x20;

```bash
Checking DNS reachability:
nameserver 10.50.3.10
search example.local
Result:
IP DNS 10.50.3.10 unreachable
```

Lúc này, bạn cần kiểm tra lại **Security Group** trên **Window server** và mở thêm các port cần thiết. Chi tiết các port xem phần dưới cùng của tài liệu này.&#x20;

### **Bước 7: Kiểm tra kết nối với Active Directory**

* Kiểm tra khả năng kết nối của Active Directory bằng lệnh:

```bash
efs_check.sh --check-AD
```

Nếu thành công, kết quả trả về như sau:&#x20;

```sql
Checking join server as a member of Domain Controller: example.local
Result:
WARNING: Using passwords on command line is insecure. Installing the setproctitle python module will hide these from shortly after program start.
Joined domain example.local (S-1-5-21-155487562-3339548754-483448002)
```

Nếu thất bại, kết quả trả về là:&#x20;

```vbnet
Checking join server as a member of Domain Controller: example.local
Result:
WARNING: Using passwords on command line is insecure. Installing the setproctitle python module will hide these from shortly after program start.
ERROR(runtime): uncaught exception - (3221225653, '{Device Timeout} The specified I/O operation on %hs was not completed before the time-out period expired.')
  File "/usr/lib64/python3.9/site-packages/samba/netcmd/__init__.py", line 353, in _run
    return self.run(*args, **kwargs)
  File "/usr/lib64/python3.9/site-packages/samba/netcmd/domain/join.py", line 106, in run
    lp.set('workgroup', net.finddc(domain=domain,
```

Lúc này, bạn cần kiểm tra lại **Security Group** trên **Window server** và mở thêm các port cần thiết. Chi tiết các port xem phần dưới cùng của tài liệu này.&#x20;

{% hint style="info" %}
Chú ý:&#x20;

* **Một CentOS Server chỉ dùng để kiểm tra một Active Directory (AD):**  Sau khi kiểm tra thành công kết nối với một **AD**, script sẽ **lưu cấu hình** cũ, do đó, bạn **không nên tái sử dụng server này để kiểm tra các AD khác**. Nếu cần kiểm tra một AD mới, bạn nên:
  * Tạo một CentOS server mới.
  * Thực hiện lại các bước từ đầu để đảm bảo kiểm tra độc lập và chính xác.
* **Trường hợp kiểm tra thất bại (check fail):** Trong trường hợp kiểm tra thất bại, bạn **có thể sử dụng lại CentOS server** để kiểm tra kết nối trên chính DNS Server, AD đã kiểm tra trước đó sau khi đã cập nhật thêm các port trong **Security Group**.
{% endhint %}

***

## Danh sách các Port cần thiết để kết nối DNS Server, Active Directory tới VPC&#x20;

Bên dưới là toàn bộ các port cần thiết mà bạn cần mở trong **Security Group** để đảm bảo kết nối thông suốt giữa DNS Server, Active Directory, và VPC của bạn:

| **Service**                                | **Port**    | **Protocol** |
| ------------------------------------------ | ----------- | ------------ |
| DNS \*                                     | 53          | tcp/udp      |
| Kerberos                                   | 88          | tcp/udp      |
| ntp \*\*                                   | 123         | udp          |
| End Point Mapper (DCE/RPC Locator Service) | 135         | tcp          |
| NetBIOS Name Service                       | 137         | udp          |
| NetBIOS Datagram                           | 138         | udp          |
| NetBIOS Session                            | 139         | tcp          |
| LDAP                                       | 389         | tcp/udp      |
| SMB over TCP                               | 445         | tcp          |
| Kerberos kpasswd                           | 464         | tcp/udp      |
| LDAPS \*\*\*                               | 636         | tcp          |
| Global Catalog                             | 3268        | tcp          |
| Global Catalog SSL \*\*\*                  | 3269        | tcp          |
| Dynamic RPC Ports \*\*\*\*                 | 49152-65535 | tcp          |

