# Khởi tạo một Private SMB File Storage có Active Directory

Để khởi tạo một SMB (Server Message Block) trên hệ thống File Storage, bạn có thể làm theo các bước sau:

## Khởi tạo Windows server on vServer

Trước khi có thể thực hiện khởi tạo Windows server, hãy đảm bảo bạn khởi tạo VPC, Subnet trên hệ thống vServer. Tiếp theo, thực hiện các bước theo hướng dẫn bên dưới để khởi tạo Windows server:&#x20;

1. Đăng nhập vào vServer tại [https://hcm-03.console.vngcloud.tech/vserver](https://hcm-03.console.vngcloud.tech/vserver/v-server/create-server).
2. Tiếp tục chọn mục **Servers**.
3. Chọn **Create a Server.**
4. Ở mục **Basic Configuration**, nhập **Server name** để mô tả tên cho Server của bạn. Tên Server có thể bao gồm các chữ cái (a-z, A-Z, 0-9, '\_', '-'). Độ dài dữ liệu đầu vào nằm trong khoảng từ 5 đến 50. Nó không được bao gồm khoảng trắng ở đầu hoặc ở cuối và tên Server name phải khác với Username
5. Lựa chọn **Zone** mà bạn mong muốn tạo server.
6. Nhập thông tin **Tag** bao gồm **Key**/ **Value** cho server và click **Add** để thêm tag này nếu bạn có nhu cầu.
7. Lựa chọn **OS Images: Windows,** tiếp tục chọn **Window version** tùy thuộc theo nhu cầu sử dụng của bạn.
8. Dưới mục **Instance type,** là danh sách các cấu hình Flavor, bạn có thể chọn cấu hình Flavor mong muốn cho Server của mình theo. **iot.v1.small1x1** được chúng tôi đề xuất như một cấu hình cơ bản mặc định để khởi tạo Server
9. Ở mục **Volume Settings**, nhập cấu hình cho Boot OS Volume (Root) gồm **Size GB**, **Volume Type SSD** và **IOPS**, sau đó chọn **Next**
10. Ngoài ra bạn có thể thêm **Data Volume** vào Server trong quá trình khởi tạo bằng cách chọn **Add Data volume,** sau đó **n**hập cấu hình cho Data Volume gồm **Volume name**, **Size GB**, **Volume Type SSD** và **IOPS**, chọn **Next**
11. Kế tiếp chọn thông số mục **Network settings:** Tại đây có thể chọn **VPC** để cấp Private IP cho Server và **Subnet** từ danh sách bạn đã tạo trước đó, hoặc có thể nhấn vào [**đây**](https://hcm-3.console.vngcloud.vn/vserver/network/vpc) để tạo mới VPC và Subnet, cần lưu ý ràng sau khi tạo VPC và Subnet, nó sẽ hiển thị tại trang danh sách cho phép bạn chọn trong quá trình khởi tạo Server:
    1. Tích vào ô Floating IP để gán Public IP cho Server (Nhấn vào [**đây**](https://docs.vngcloud.vn/vng-cloud-document/vn/vserver/compute-hcm03-1a/network/floating-ip) để xem hướng dẫn attach/ detach Floating IP)
    2. **Security group** để quản lý bộ ACL - Access Control List cho Server. (Nhấp vào [**đây**](https://docs.vngcloud.vn/vng-cloud-document/vn/vserver/compute-hcm03-1a/security/security-groups) để xem hướng dẫn tạo và quản lý Security group)
12. Nhập thông tin **Authentication**: Empty: hệ thống sẽ tự động tạo và gắn password hoặc user tự tinh chỉnh và enable hay disable việc bỏ qua change password lần đầu.
13. Ở mục **Other Settings**, có thể tùy chọn server Group hoặc không theo nhu cầu sử dụng. Bạn có thể gán Server vào các Group trước đó đã tạo (Với các thuộc tính như cùng Compute Host hay khác Compute Host)
14. Chọn **Launch Server** và thực hiện các bước thanh toán để hoàn thành việc khởi tạo server

<figure><img src="../../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

***

## Kết nối tới Windows server vừa khởi tạo

**Để có thể kết nối vào máy chủ Window, trước tiên, bạn cần cài đặt RDP:** Theo mặc định, Windows sẽ bao gồm RDP Client. Để xác minh, hãy nhập **mstsc** tại cửa sổ Command Prompt. Nếu máy tính của bạn không nhận ra lệnh này, hãy xem trang chủ Windows và tìm kiếm bản tải xuống cho ứng dụng[ Microsoft Remote Desktop](https://www.microsoft.com/vi-vn/windows).

1. Truy cập vào trang quản lý Server tại trình điều khiển của chúng tôi tại: [https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server)
2. Chọn **Server** cần kết nối, sau đó chọn **Action, tiếp tục chọn Connect**
3. Trên trang Kết nối tới máy chủ, chọn tab **RDP (Window)**

<figure><img src="../../../../.gitbook/assets/image (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

4. Chọn **Tải xuống tệp RDP**. Trình duyệt của bạn sẽ nhắc bạn mở hoặc lưu tệp RDP. Khi bạn đã hoàn tất tải xuống tệp, hãy chọn **Hoàn thành** để quay lại trang máy chủ:

* Nếu bạn đã mở tệp RDP, bạn sẽ thấy hộp thoại Kết nối Máy tính Từ xa.
* Nếu bạn đã lưu tệp RDP, hãy điều hướng đến thư mục tải xuống của bạn và mở tệp RDP để hiển thị hộp thoại.

5. Bạn có thể nhận được cảnh báo rằng nhà xuất bản của kết nối từ xa không xác định. Chọn **Connect** để tiếp tục kết nối với máy chủ của bạn

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FfuEO8mrahhrFz1w6mUJN%252Fimage.png%3Falt%3Dmedia%26token%3D0a210d8e-cfe1-4fe8-9d9a-cefa8a87194d&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=79b6565d&#x26;sv=2" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (2) (1).png" alt="" width="275"><figcaption></figcaption></figure>

6. Tài khoản quản trị viên được chọn theo mặc định. Bạn cần sao chép và dán mật khẩu mà bạn đã lưu trước đó vào pop-up đăng nhập (Thông tin này lấy từ email), trong đó nhập thông tin **InstanceLogin** vào **Username**, **InstancePassword** vào **Password**:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FYtoGMhcAycCS94iY1Oiw%252Fimage.png%3Falt%3Dmedia%26token%3Da55f53fd-362c-4d92-bc11-5863f59e818f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=153a315d&#x26;sv=2" alt="" width="375"><figcaption></figcaption></figure>

7. Chọn **OK.** Do tính chất của chứng chỉ tự ký, bạn có thể nhận được cảnh báo rằng chứng chỉ bảo mật không thể được xác thực. Sử dụng các bước sau để xác minh danh tính của máy tính từ xa hoặc chỉ cần chọn **Yes** (Windows) hoặc **Continue** (Mac OS X) nếu bạn tin cậy chứng chỉ.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FNH1l2utiMi3RJxfBoknu%252Fimage.png%3Falt%3Dmedia%26token%3Db50838b8-d830-4273-a67f-6ccfe237ccf4&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=f64057f4&#x26;sv=2" alt="" width="375"><figcaption></figcaption></figure>

8. Màn hình sẽ hiển thị đang kết nối đến máy chủ Window thành công

<figure><img src="../../../../.gitbook/assets/image (3) (1).png" alt="" width="272"><figcaption></figcaption></figure>

***

## Khởi tạo Active Directory trên Windows Server

Để khởi tạo được Active Directory trên Windows Server, bạn cần:

* **Cài đặt và cấu hình DNS Server**
* **Cài đặt và cấu hình Active Directory**

Cụ thể, vui lòng thực hiện theo các bước bên dưới

### Cài đặt và cấu hình DNS Server

Để cài đặt và cấu hình DNS Server trên Windows Server, bạn có thể làm theo các bước sau:

1. Từ màn hình **Desktop**, bạn mở **Start** menu và chọn **Server Manager**
2. Chọn mục **All Servers,** chọn chuột phải sau đó chọn **Add roles and Features**

<figure><img src="../../../../.gitbook/assets/image (872).png" alt=""><figcaption></figcaption></figure>

3. Tại trang **Before you begin,** nhấn **Next**

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

4. Tại trang **Installation Type**: Chọn **Role-based or feature-based installation** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

5. Tại mục **Server Selection**: bạn chọn **Select a server from the server pool** và **chọn server hiện tại** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

6. Tại mục **Server Roles**: Tick chọn **DNS Server** sau đó nhấn **Next** và **Install** để cài đặt.

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

7. Lúc này, bạn sẽ được nhắc thêm các tính năng cần thiết cho DNS Server, chọn **Add Features** nếu bạn đồng ý với các mặc định.
8. Tại trang **Confirmation**, kiểm tra lại các lựa chọn của bạn và nhấn Install để bắt đầu cài đặt DNS Server

<figure><img src="../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

7. Sau khi việc cài đặt hoàn tất, bạn hãy nhấn **Close**.

<figure><img src="../../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### Tạo một Forward Lookup Zone (nếu chưa có)

Tiếp theo, bạn sẽ cần tạo một Forward Lookup Zone để giải quyết tên thành địa chỉ IP. Cụ thể các bước thực hiện như sau:&#x20;

1. Thực hiện mở **DNS Manager** bằng cách chọn **Tools**, sau đó chọn **DNS**

<figure><img src="../../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

2. Trong DNS Manager, chọn vào DNS đang có và tiếp tục nhấp chuột phải vào **Forward Lookup Zones** và chọn **New Zone**

<figure><img src="../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

3. Màn hình Tạo zone mới hiển thị, tiếp tục chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

3. Tại màn hình **Zone Type**: chọn **Primary zone,** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

3. Tại màn hình **Active Directory Zone Replication Scope:** chọn **To all DNS servers running on domain controllers in this domain: \<domainname>** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

3. Tại màn hình **Zone Name**: nhập tên domain của bạn và chọn **Next**. Ví dụ: `example.local`.

<figure><img src="../../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

3. Tại màn hình **Dynamic Update**: Chọn **Do not allow dynamic updates**, sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

3. Chọn **Finish** để hoàn thành việc tạo New Zone

<figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

3. Sau khi chọn **Finish**, bạn sẽ thấy forwarding lookup zone trên màn hình chính như hình

<figure><img src="../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

4. Sau khi tạo zone, bạn cần thêm bản ghi cho **Domain Controller** bằng cách chọn vào **Zone** vừa tạo, nhần chuột phải và chọn **New Host (A or AAAA)**

<figure><img src="../../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

5. Tại màn hình **New Host,** bạn cần:

* **Name**: Nhập tên Windows server của bạn (VD: `demo-smb`).
* **IP Address**: Nhập địa chỉ IP tĩnh của Domain Controller (VD: `10.50.3.3`).
* Nhấn **Add Host**.

<figure><img src="../../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

### Kiểm tra DNS name&#x20;

Trên Windows server của bạn, mở Command Prompt và chạy:

```bash
nslookup <DNS Domain>
```

Ví dụ:&#x20;

```bash
nslookup example.local
```

<figure><img src="../../../../.gitbook/assets/image (19).png" alt=""><figcaption><p><br></p></figcaption></figure>

```bash
nsloopup demo_windows_server.example.local
```

<figure><img src="../../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

### Cài đặt và cấu hình Active Directory Domain Services

Để cài đặt và cấu hình Active Directory Domain Service trên Windows Server, bạn có thể làm theo các bước sau:

1. Từ màn hình **Desktop**, bạn mở **Start** menu và chọn **Server Manager**
2. Chọn mục **All Servers,** chọn chuột phải sau đó chọn **Add roles and Features**
3. Tại mục Before You Begin, chọn Next
4. Tại mục **Installation Type**: Chọn **Role-based or feature-based installation sau đó chọn Next**
5. Tại mục **Server Selection**: bạn chọn **Select a server from the server pool** và **chọn server hiện tại** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

6. Tại mục **Server Roles**: Tick chọn **Active Directory Domain Services** sau đó nhấn **Next** và **Install** để cài đặt.
7. Lúc này, bạn sẽ được nhắc thêm các tính năng cần thiết cho Active Directory, chọn **Add Features** nếu bạn đồng ý với các mặc định, sau đó chọn **Next**
8. Tại trang Feature, giữ các thông số mặc định và chọn Next
9. Tại trang AD DS, chọn Next
10. Tại trang **Confirmation**, kiểm tra lại các lựa chọn của bạn và nhấn Install để bắt đầu cài đặt AD DS
11. Sau khi chọn **Install**. Hệ thống sẽ bắt đầu cài đặt, quá trình cài đặt này sẽ mất vài phút. Bạn không cần khởi động lại server ngay sau khi cài đặt.
12. Khi việc cài đặt hoàn thành, bạn chọn tiếp Promote this server to a domain controller
13. Tại màn hình Deployment Configuration, chọn Add a new forest sau đó chọn Next
14. Tại màn hình Domain Controller Options, bạn hãy nhập Password và Confirm Password cho DSRM của bạn
15. Tại mục DNS Option, bạn bỏ qua và chỉ nhần Next
16. Tại mục Additional Options, bạn hãy kiểm tra lại NetBIOS name và thay đổi nếu bạn thấy cần thiết sau đó chọn Next
17. Tại màn hình Paths, bạn có thể thay đổi các đường dẫn tới Database folder, Log file folder, Sysvol hoặc giữ như mặc định của hệ thống, sau đó chọn Next
18. Tại màn hình Review Options, bạn hãy review lại các thông số và chọn Next nếu thông tin đã đúng
19. Tại màn hình Prerequisites Check, bạn sẽ thấy kết quả kiểm tra, tiếp tục chọn Install để hệ thống cài đặt AD
20. Sau khi quá trình cài đặt hoàn thành, hệ thống sẽ tự động khởi động lại server của bạn, bạn cần login lại vào server với tài khoản Administrator





***

## Khởi tạo File Storage

**Bước 1:** Truy cập vào [https://efs.console.vngcloud.vn/overview](https://efs.console.vngcloud.vn/overview)

**Bước 2:** Chọn mục **File Storage** sau đó chọn **Create a File storage.**

<figure><img src="../../../../.gitbook/assets/image (818).png" alt=""><figcaption></figcaption></figure>

**Bước 3:** Tại màn hình khởi tạo File Storage, bạn cần nhập/ chọn:&#x20;

* **File Storage name:** tên gợi nhớ của file storage. Tên file cần dài từ 5 tới 50 ký tự và có thể bao gồm các ký tự a-z, A-Z, 0-9, '-', '\_'
* **Description**: nhập mô tả cho file storage.
* **File storage type:** chọn loại ổ đĩa mà bạn mong muốn sử dụng. Hiện tại chúng tôi chỉ cung cấp loại ổ đĩa **Standard HDD.**
* **Protocol:** chọn NFS và version NFS mà bạn mong muốn
* **Tag:** bạn có thể thêm các tag để đánh dầu file storage theo nhu cầu.

<figure><img src="../../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

* **File Storage Max quota:** trong bước khởi tạo file storage, bạn cần đặt một giới hạn quota tối đa cho file storage đó. Quota này có ý nghĩa chính là giới hạn dung lượng lưu trữ mà file storage có thể sử dụng, giúp quản lý tài nguyên hiệu quả. <mark style="color:red;">**Mức quota tối thiểu bạn cần chọn là 1 TB và mức quota tối đa chúng tôi cung cấp là 50 TB.**</mark> Nếu bạn có nhu cấu sử dụng nhiều hơn 50 TB cho một file storage, vui lòng liên hệ với chúng tôi.
* **Network type**: đối với loại file SMB, network type bắt buộc phải là Private.&#x20;
* **Window Authentication: c**ấu hình quyền truy cập thông qua **Basic Authentication** hoặc **Active Directory Authentication**
  * **Basic Authentication:** Nếu Windows server của bạn không có Active Directory hoặc bạn muốn quản lý quyền truy cập đơn giản thông qua username và password, bạn có thể sử dụng Basic authentication, chúng tôi hỗ trợ bạn tạo tối đa 10 tài khoản username/password để truy cập file storage.

<figure><img src="../../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

* **Active Directory Authentication:** Nếu Windows server của bạn sử dụng Active Directory để quản lý người dùng và quyền truy cập, thì AD Authentication sẽ dễ dàng tích hợp và quản lý tập trung. Bạn có thể xác thực thông qua Active Directory domain name, DNS server IP addresses, Username, Password trên Active Directory của bạn.

<figure><img src="../../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 5:** Chọn **Create File Storage.**

***

## Map File Storage vừa khởi tạo tới Windows server

Trên Windows Server, bạn có thể map file storage SMB thông qua giao diện hoặc dòng lệnh.

**Qua giao diện:**

1. **Mở File Explorer.**
2. Nhấp chuột phải vào **This PC** và chọn **Map network drive**.
3. Trong cửa sổ **Map Network Drive**:

* **Drive letter**: Chọn một ký tự ổ đĩa (VD: `Z:`).
* **Folder**: Nhập đường dẫn SMB share, ví dụ: `\\<File Storage IP Address>\<File Storage Name>`. Ví dụ `\\10.210.2.5\demo-smb`.
* Tiếp tục nhập thông tin đăng nhập:
  * **Username**: Tên tài khoản bạn đã tạo trên file storage SMB trước đó.
  * **Password**: Mật khẩu tương ứng.
* Nhấn **Finish** để hoàn tất.

**Qua dòng lệnh:**

Sử dụng lệnh sau trong **Command Prompt** hoặc **PowerShell**:

```cmd
net use Z: \\<File Storage IP Address>\<File Storage Name> /user:USERNAME PASSWORD
```

* **Z:**: Là ký tự ổ đĩa mà bạn muốn gắn.
* **\\\\\<File Storage IP Address>\\\<File Storage Name>**: Đường dẫn File Storage SMB.
* **USERNAME**: Tên tài khoản bạn đã tạo trên file storage SMB trước đó.
* **PASSWORD**: Mật khẩu tương ứng.

Ví dụ:

```cmd
net use Z: \\10.210.2.5\share /user:admin_password_123
```

<figure><img src="../../../../.gitbook/assets/image (8) (1).png" alt="" width="353"><figcaption></figcaption></figure>

4. Chọn Finish, sau khi hoàn tất, bạn có thể kiểm tra trong **File Explorer** để thấy ổ đĩa được map.

{% hint style="info" %}
**Chú ý:**

* Để tự động map file storage SMB mỗi lần khởi động Windows Server, bạn có thể lưu thông tin khi map qua giao diện bằng cách tích vào ô **Reconnect at sign-in** trước khi nhấn **Finish**.
{% endhint %}

***

## Write data tới File Storage

Sau khi bạn đã **map File Storage SMB** vào Windows Server thành công, bạn có thể thực hiện việc ghi dữ liệu (write data) tới File Storage như sau:

Đúng, cách bạn mô tả là một phương pháp đơn giản và trực quan để **ghi dữ liệu (write data)** vào File Storage SMB của bạn. Dưới đây là các bước chi tiết để thực hiện:

1. **Mở trình soạn thảo văn bản (Notepad):**
   * Trên Windows Server, mở **Notepad** bằng cách:
     * Nhấn **Start** và gõ **Notepad**, sau đó nhấn **Enter**.
   * Hoặc, nhấn tổ hợp phím **Windows + R**, nhập `notepad` và nhấn **Enter**.
2. **Viết nội dung vào file:**
   *   Trong Notepad, nhập một nội dung đơn giản, ví dụ:

       ```
       Đây là file test ghi vào SMB share.
       ```
   * Hoặc nhập bất kỳ nội dung nào bạn muốn.
3. **Lưu file vào file storage SMB:**
   * Nhấn **File > Save As...**.
   * Trong hộp thoại **Save As**, điều hướng đến ổ đĩa mà bạn đã map SMB share (VD: `Z:`).
   * Đặt tên file (VD: `testfile.txt`).
   * Nhấn **Save** để lưu file.
4. **Kiểm tra file trong SMB share:**
   * Mở **File Explorer** (phím tắt: **Windows + E**).
   * Điều hướng đến ổ đĩa SMB (VD: `Z:`).
   * Tìm và mở file `testfile.txt` mà bạn vừa lưu để xác minh nội dung
