# Khởi tạo SMB File Storage có AD

Để khởi tạo một SMB (Server Message Block) trên hệ thống File Storage, bạn có thể làm theo các bước sau:

## Khởi tạo Active Directory trên Windows Server

Để khởi tạo được Active Directory trên Windows Server, bạn cần thực hiện:

* **Cài đặt và cấu hình DNS Server**
* **Tạo Forward Lookup Zone**
* **Cài đặt và cấu hình Active Directory**

Cụ thể, vui lòng thực hiện theo các bước bên dưới:

### Cài đặt và cấu hình DNS Server

Để cài đặt và cấu hình DNS Server trên Windows Server, bạn có thể làm theo các bước sau:

1. Từ màn hình **Desktop**, bạn mở **Start** menu và chọn **Server Manager.**
2. Chọn mục **All Servers,** chọn chuột phải sau đó chọn **Add roles and Features**

<figure><img src="../../../../.gitbook/assets/image (897).png" alt="" width="563"><figcaption></figcaption></figure>

3. Tại trang **Before you begin,** nhấn **Next**

<figure><img src="../../../../.gitbook/assets/image (898).png" alt="" width="563"><figcaption></figcaption></figure>

4. Tại trang **Installation Type**: Chọn **Role-based or feature-based installation** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (1).png" alt="" width="563"><figcaption></figcaption></figure>

5. Tại mục **Server Selection**: bạn chọn **Select a server from the server pool** và **chọn server hiện tại** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>

6. Tại mục **Server Roles**: Tick chọn **DNS Server** sau đó nhấn **Next** và **Install** để cài đặt.

<figure><img src="../../../../.gitbook/assets/image (899).png" alt="" width="563"><figcaption></figcaption></figure>

7. Lúc này, bạn sẽ được nhắc thêm các tính năng cần thiết cho DNS Server, chọn **Add Features** nếu bạn đồng ý với các mặc định.

<figure><img src="../../../../.gitbook/assets/image (900).png" alt="" width="563"><figcaption></figcaption></figure>

8. Tại trang **Confirmation**, kiểm tra lại các lựa chọn của bạn và nhấn Install để bắt đầu cài đặt DNS Server

<figure><img src="../../../../.gitbook/assets/image (5).png" alt="" width="563"><figcaption></figcaption></figure>

9. Sau khi việc cài đặt hoàn tất, bạn hãy nhấn **Close**.

<figure><img src="../../../../.gitbook/assets/image (6).png" alt="" width="563"><figcaption></figcaption></figure>

### Tạo một Forward Lookup Zone&#x20;

Tiếp theo, bạn sẽ cần tạo một Forward Lookup Zone để chuyển domain thành địa chỉ IP. Cụ thể các bước thực hiện như sau:&#x20;

1. Thực hiện mở **DNS Manager** bằng cách chọn **Tools**, sau đó chọn **DNS**

<figure><img src="../../../../.gitbook/assets/image (7).png" alt="" width="336"><figcaption></figcaption></figure>

2. Trong DNS Manager, chọn vào DNS đang có và tiếp tục nhấp chuột phải vào **Forward Lookup Zones** và chọn **New Zone**

<figure><img src="../../../../.gitbook/assets/image (8).png" alt="" width="563"><figcaption></figcaption></figure>

3. Màn hình Tạo zone mới hiển thị, tiếp tục chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (9).png" alt="" width="514"><figcaption></figcaption></figure>

4. Tại màn hình **Zone Type**: chọn **Primary zone,** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (11).png" alt="" width="509"><figcaption></figcaption></figure>

5. Tại màn hình **Active Directory Zone Replication Scope:** chọn **To all DNS servers running on domain controllers in this domain: \<domainname>** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (12).png" alt="" width="509"><figcaption></figcaption></figure>

6. Tại màn hình **Zone Name**: nhập tên domain của bạn và chọn **Next**. Ví dụ: `example.local`.

<figure><img src="../../../../.gitbook/assets/image (13).png" alt="" width="509"><figcaption></figcaption></figure>

7. Tại màn hình **Dynamic Update**: Chọn **Do not allow dynamic updates**, sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (14).png" alt="" width="509"><figcaption></figcaption></figure>

8. Chọn **Finish** để hoàn thành việc tạo New Zone

<figure><img src="../../../../.gitbook/assets/image (15).png" alt="" width="508"><figcaption></figcaption></figure>

9. Sau khi chọn **Finish**, bạn sẽ thấy forwarding lookup zone trên màn hình chính như hình

<figure><img src="../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

10. Sau khi tạo zone, bạn cần thêm bản ghi cho **Domain Controller** bằng cách chọn vào **Zone** vừa tạo, nhần chuột phải và chọn **New Host (A or AAAA)**

<figure><img src="../../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

11. Tại màn hình **New Host,** bạn cần:

* **Name**: Nhập tên Windows server của bạn (VD: `demo-smb`).
* **IP Address**: Nhập địa chỉ IP tĩnh của Domain Controller (VD: `10.50.3.3`).
* Nhấn **Add Host**.

<figure><img src="../../../../.gitbook/assets/image (18).png" alt="" width="349"><figcaption></figcaption></figure>

### Kiểm tra DNS name&#x20;

Trên Windows server của bạn, mở Command Prompt và chạy:

```bash
nslookup <DNS Domain>
```

Ví dụ:&#x20;

```bash
nslookup example.local
```

<figure><img src="../../../../.gitbook/assets/image (19).png" alt="" width="234"><figcaption><p><br></p></figcaption></figure>

```bash
nsloopup demo_windows_server.example.local
```

<figure><img src="../../../../.gitbook/assets/image (20).png" alt="" width="377"><figcaption></figcaption></figure>

### Cài đặt và cấu hình Active Directory Domain Services

Để cài đặt và cấu hình Active Directory Domain Service trên Windows Server, bạn có thể làm theo các bước sau:

1. Từ màn hình **Desktop**, bạn mở **Start** menu và chọn **Server Manager**
2. Chọn mục **All Servers,** chọn chuột phải sau đó chọn **Add roles and Features**

<figure><img src="../../../../.gitbook/assets/image (877).png" alt=""><figcaption></figcaption></figure>

3. Tại mục **Before You Begin**, chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (878).png" alt="" width="563"><figcaption></figcaption></figure>

4. Tại mục **Installation Type**: Chọn **Role-based or feature-based installation** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (879).png" alt="" width="563"><figcaption></figcaption></figure>

5. Tại mục **Server Selection**: bạn chọn **Select a server from the server pool** và **chọn server hiện tại** sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>

6. Tại mục **Server Roles**: Tick chọn **Active Directory Domain Services.**

<figure><img src="../../../../.gitbook/assets/image (881).png" alt="" width="563"><figcaption></figcaption></figure>

7. Lúc này, bạn sẽ được nhắc thêm các tính năng cần thiết cho Active Directory, chọn **Add Features** nếu bạn đồng ý với các mặc định, sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (880).png" alt="" width="563"><figcaption></figcaption></figure>

8. Tại trang **Feature**, giữ các thông số mặc định và chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (882).png" alt="" width="563"><figcaption></figcaption></figure>

9. Tại trang AD DS, chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (883).png" alt="" width="563"><figcaption></figcaption></figure>

10. Tại trang **Confirmation**, kiểm tra lại các lựa chọn của bạn và nhấn **Install** để bắt đầu cài đặt AD DS

<figure><img src="../../../../.gitbook/assets/image (884).png" alt="" width="563"><figcaption></figcaption></figure>

11. Sau khi chọn **Install**. Hệ thống sẽ bắt đầu cài đặt, bạn không cần khởi động lại server ngay sau khi cài đặt.
12. Khi việc cài đặt hoàn thành, bạn chọn tiếp **Promote this server to a domain controller**

<figure><img src="../../../../.gitbook/assets/image (885).png" alt="" width="563"><figcaption></figcaption></figure>

13. Tại màn hình **Deployment Configuration**, bạn có thể chọn một domain nếu bạn đã có sắn hoặc chọn **Add a new forest** và nhập domain name để tạo mới domain sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (887).png" alt="" width="563"><figcaption></figcaption></figure>

14. Tại màn hình **Domain Controller Options**, bạn hãy nhập **Password** và **Confirm Password** cho DSRM của bạn

<figure><img src="../../../../.gitbook/assets/image (888).png" alt="" width="563"><figcaption></figcaption></figure>

15. Tại mục DNS Option, bạn bỏ qua và chỉ nhần **Next**

<figure><img src="../../../../.gitbook/assets/image (889).png" alt="" width="563"><figcaption></figcaption></figure>

16. Tại mục **Additional Options**, bạn hãy kiểm tra lại **NetBIOS name** và thay đổi nếu bạn thấy cần thiết sau đó chọn **Next**

<figure><img src="../../../../.gitbook/assets/image (890).png" alt="" width="563"><figcaption></figcaption></figure>

17. Tại màn hình **Paths**, bạn có thể thay đổi các đường dẫn tới **Database folder, Log file folder, Sysvol** hoặc giữ như mặc định của hệ thống, sau đó chọn Next

<figure><img src="../../../../.gitbook/assets/image (891).png" alt="" width="563"><figcaption></figcaption></figure>

18. Tại màn hình **Review Options**, bạn hãy review lại các thông số và chọn **Next** nếu thông tin đã đúng

<figure><img src="../../../../.gitbook/assets/image (892).png" alt="" width="563"><figcaption></figcaption></figure>

19. Tại màn hình **Prerequisites Check**, bạn sẽ thấy kết quả kiểm tra, tiếp tục chọn **Install** để hệ thống cài đặt AD

<figure><img src="../../../../.gitbook/assets/image (893).png" alt="" width="563"><figcaption></figcaption></figure>

20. Sau khi quá trình cài đặt hoàn thành, hệ thống sẽ tự động khởi động lại server của bạn, bạn cần login lại vào server với tài khoản **Administrator**

{% hint style="info" %}
**Chú ý:**

* Bạn có thể thực hiện phân quyền cho tài khoản AD hoặc nhóm thông qua tính năng cấp quyền truy cập qua Group Policy hoặc ACL. Cụ thể, tham khảo thêm tại [đây](https://learn.microsoft.com/en-us/troubleshoot/windows-server/active-directory/active-directory-overview).
{% endhint %}

***

## Khởi tạo File Storage

**Bước 1:** Truy cập vào [https://efs.console.vngcloud.vn/overview](https://efs.console.vngcloud.vn/overview)

**Bước 2:** Chọn mục **File Storage** sau đó chọn **Create a File storage.**

**Bước 3:** Tại màn hình khởi tạo File Storage, bạn cần nhập/ chọn:&#x20;

* **File Storage name:** tên gợi nhớ của file storage. Tên file cần dài từ 5 tới 50 ký tự và có thể bao gồm các ký tự a-z, A-Z, 0-9, '-', '\_'
* **Description**: nhập mô tả cho file storage.
* **File storage type:** chọn loại ổ đĩa mà bạn mong muốn sử dụng. Hiện tại chúng tôi chỉ cung cấp loại ổ đĩa **Standard HDD.**
* **Protocol:** chọn NFS và version NFS mà bạn mong muốn
* **Tag:** bạn có thể thêm các tag để đánh dầu file storage theo nhu cầu.

<figure><img src="../../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

* **File Storage Max quota:** trong bước khởi tạo file storage, bạn cần đặt một giới hạn quota tối đa cho file storage đó. Quota này có ý nghĩa chính là giới hạn dung lượng lưu trữ mà file storage có thể sử dụng, giúp quản lý tài nguyên hiệu quả. <mark style="color:red;">**Mức quota tối thiểu bạn cần chọn là 1 TB và mức quota tối đa chúng tôi cung cấp là 50 TB.**</mark> Nếu bạn có nhu cấu sử dụng nhiều hơn 50 TB cho một file storage, vui lòng liên hệ với chúng tôi.
* **Network type**: đối với loại file SMB, network type bắt buộc phải là Private. Lúc này, bạn cần chọn **VPC**, **Subnet** mà bạn đã khởi tạo từ vServer Portal.

<figure><img src="../../../../.gitbook/assets/image (904).png" alt=""><figcaption></figcaption></figure>

* **Window Authentication: c**ấu hình quyền truy cập thông qua **Active Directory Authentication**
  * **Active Directory Authentication:** Nếu Windows server của bạn sử dụng Active Directory để quản lý người dùng và quyền truy cập, thì AD Authentication sẽ dễ dàng tích hợp và quản lý tập trung. Bạn có thể xác thực thông qua Active Directory domain name, DNS server IP addresses, Username, Password trên Active Directory của bạn. Ví dụ, ứng với Avtive Directory đã tạo bên trên, tôi sẽ nhập vào:
    * **Active Directory domain name**: Domain bạn tạo bên trên, ví dụ: example.local
    * **DNS server IP Address**: Địa chỉ IP DNS Server, ví dụ: 10.50.3.3
    * **Username:** Tên tài khoản admin, ví dụ Administrator
    * **Password**: Mật khẩu bạn đã tạo bên trên, ví dụ: 123456789aA@
    * **Confirm Password:** Xác nhận mật khẩu, ví dụ: 123456789aA@

<figure><img src="../../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 5:** Chọn **Create File Storage.**

***

## Map File Storage vừa khởi tạo tới Windows server&#x20;

Trên Windows Server, bạn có thể map file storage SMB thông qua giao diện hoặc dòng lệnh.

### **Qua giao diện**

1. **Mở File Explorer.**
2. Nhấp chuột phải vào **This PC** và chọn **Map network drive**.
3. Trong cửa sổ **Map Network Drive**:

* **Drive letter**: Chọn một ký tự ổ đĩa (VD: `Z:`).
* **Folder**: Nhập đường dẫn SMB share, ví dụ: `\\<File Storage IP Address>\<File Storage Name>`. Ví dụ `\\10.210.2.5\demo-smb`.
* Nhấn **Finish** để hoàn tất.

### **Qua dòng lệnh**

Sử dụng lệnh sau trong **Command Prompt** hoặc **PowerShell**:

```cmd
net use Z: \\<File Storage IP Address>\<File Storage Name> 
```

* **Z:**: Là ký tự ổ đĩa mà bạn muốn gắn.
* **\\\\\<File Storage IP Address>\\\<File Storage Name>**: Đường dẫn File Storage SMB.

Ví dụ:

```cmd
net use Z: \\10.210.2.5\demo-smb
```

4. Chọn Finish, sau khi hoàn tất, bạn có thể kiểm tra trong **File Explorer** để thấy ổ đĩa được map.

<figure><img src="../../../../.gitbook/assets/image (902).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Chú ý:**

* Để tự động map file storage SMB mỗi lần khởi động Windows Server, bạn có thể lưu thông tin khi map qua giao diện bằng cách tích vào ô **Reconnect at sign-in** trước khi nhấn **Finish**.
{% endhint %}

### Qua trực tiếp File Explorer

Đơn giản hơn, bạn cũng có thể truy cập trực tiếp tới File Storage SMB qua File Explorer qua các bước:

* **Mở File Explorer**:
  * Nhấn tổ hợp phím **Windows + E** hoặc nhấp vào biểu tượng File Explorer.
* **Nhập UNC Path**:
  *   Trên thanh địa chỉ, nhập đường dẫn UNC đến file share. Ví dụ:

      ```
      \\10.210.2.5\demo-smb
      ```
* **Nhấn Enter**.

***

## Write data tới File Storage

Sau khi bạn đã **map File Storage SMB** vào Windows Server thành công, bạn có thể thực hiện việc ghi dữ liệu (write data) tới File Storage như sau:

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
