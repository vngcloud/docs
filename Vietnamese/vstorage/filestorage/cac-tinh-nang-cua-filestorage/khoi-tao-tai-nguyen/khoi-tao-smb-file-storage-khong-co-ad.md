# Khởi tạo SMB File Storage không có AD

Để khởi tạo một SMB (Server Message Block) không có AD trên hệ thống File Storage, bạn có thể làm theo các bước sau:

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
* **Network type**: đối với loại file SMB, network type bắt buộc phải là Private. Lúc này, bạn cần chọn **VPC**, **Subnet** mà bạn đã khởi tạo từ vServer Portal.

<figure><img src="../../../../.gitbook/assets/image (904).png" alt=""><figcaption></figcaption></figure>

* **Window Authentication: c**ấu hình quyền truy cập thông qua **Basic Authentication** hoặc **Active Directory Authentication**
  * **Basic Authentication:** Nếu Windows server của bạn không có Active Directory hoặc bạn muốn quản lý quyền truy cập đơn giản thông qua username và password, bạn có thể sử dụng Basic authentication, chúng tôi hỗ trợ bạn tạo tối đa 10 tài khoản username/password để truy cập file storage.

<figure><img src="../../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 5:** Chọn **Create File Storage.**

***

## Map File Storage vừa khởi tạo tới Windows server

Trên Windows Server, bạn có thể map file storage SMB thông qua giao diện hoặc dòng lệnh.

### **Qua giao diện**

1. **Mở File Explorer.**
2. Nhấp chuột phải vào **This PC** và chọn **Map network drive**.

<figure><img src="../../../../.gitbook/assets/image (874).png" alt=""><figcaption></figcaption></figure>

3. Trong cửa sổ **Map Network Drive**:

* **Drive letter**: Chọn một ký tự ổ đĩa (VD: `Z:`).
* **Folder**: Nhập đường dẫn SMB share, ví dụ: `\\<File Storage IP Address>\<File Storage Name>`. Ví dụ `\\10.210.2.5\demo-smb`.
* Tiếp tục nhập thông tin đăng nhập:
  * **Username**: Tên tài khoản bạn đã tạo trên file storage SMB trước đó.
  * **Password**: Mật khẩu tương ứng.
* Nhấn **Finish** để hoàn tất.

<figure><img src="../../../../.gitbook/assets/image (875).png" alt="" width="503"><figcaption></figcaption></figure>

{% hint style="info" %}
**Chú ý:**

* Để tự động map file storage SMB mỗi lần khởi động Windows Server, bạn có thể lưu thông tin khi map qua giao diện bằng cách tích vào ô **Reconnect at sign-in** trước khi nhấn **Finish**.
{% endhint %}

### **Qua dòng lệnh**

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
net use Z: \\10.210.2.5\demo-smb /user:admin password_123
```

### Qua trực tiếp File Explorer

Đơn giản hơn, bạn cũng có thể truy cập trực tiếp tới File Storage SMB qua File Explorer qua các bước:

* **Mở File Explorer**:
  * Nhấn tổ hợp phím **Windows + E** hoặc nhấp vào biểu tượng File Explorer.
* **Nhập UNC Path**:
  *   Trên thanh địa chỉ, nhập đường dẫn UNC đến file share. Ví dụ:

      ```
      \\10.210.2.5\demo-smb
      ```
* **Nhấn Enter** và nhập **username/ mật khẩu**.

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
