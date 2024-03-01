# Kết nối vào máy chủ Linux bằng công cụ SSH Client

Để kết nối đến một máy chủ Linux bằng SSH Client, bạn cần có một Terminal hoặc Command Prompt trên máy tính của bạn và sử dụng lệnh SSH. Dưới đây là hướng dẫn cách thực hiện kết nối SSH đến máy chủ Linux

Để biết thông tin về cách kết nối với phiên bản Window, hãy xem hướng dẫn [Kết nối vào máy chủ Windows sử dụng công cụ Remote Desktop (RDP)](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49650320\&src=contextnavpagetreemode) về cách kết nối với máy chủ của bạn.

***

### **Điều kiện tiên quyết** <a href="#ketnoivaomaychulinuxbangcongcusshclient-dieukientienquyet" id="ketnoivaomaychulinuxbangcongcusshclient-dieukientienquyet"></a>

* **Máy chủ phải đang chạy**:
  * Sau khi máy chủ được khởi tạo thành công, thông tin của nó sẽ xuất hiện trên trang danh sách máy chủ của bảng điều khiển và trạng thái của máy chủ là Active
*   **Thông tin kết nối đến máy chủ**: Để biết thông tin kết nối của máy chủ, vui lòng kiểm tra email đã đăng ký:\


    ### &#x20;  <a href="#ketnoivaomaychulinuxbangcongcusshclient" id="ketnoivaomaychulinuxbangcongcusshclient"></a>

    _**Lưu ý:** Thông tin này là bảo mật và chỉ được gởi cho email đã đăng kí. VNG Cloud không thể can thiệp để phục hồi thông tin login của vServer (username/ passsword/ key) trong mọi tình huống_

    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddav9fdcf0e67cb77f0d02b8ec165754a337.png?version=1&#x26;modificationDate=1681439918000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>

***

### **Kết nối sử dụng Client trên hệ điều hành Linux và MacOS** <a href="#ketnoivaomaychulinuxbangcongcusshclient-ketnoisudungclienttrenhedieuhanhlinuxvamacos" id="ketnoivaomaychulinuxbangcongcusshclient-ketnoisudungclienttrenhedieuhanhlinuxvamacos"></a>

#### _**Phương án 1**_: **Login SSH bằng password** <a href="#ketnoivaomaychulinuxbangcongcusshclient-phuongan1-loginsshbangpassword" id="ketnoivaomaychulinuxbangcongcusshclient-phuongan1-loginsshbangpassword"></a>

1.  Sử dụng Terminal của Linux để kết nối đến vServer

    | `ssh -p 234` `stackops@61.28.233.113` |
    | ------------------------------------- |
2.  Thay đổi password cho user stackops ở lần đầu tiên login:

    \
    \
    \
    **1 -** Nhập password của user stackops với nội dung là **instancePassword** trong email\
    **2 -** Nhập lại password của user stackops với nội dung là **instancePassword** trong email\
    **3 -** Nhập new password cho user stackops để dùng cho login sau này\
    **4 -** Nhập lại new password cho user stackops để dùng cho login sau này\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddav645b0b160648aea1be9e857acd48b121.png?version=1&#x26;modificationDate=1681439918000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
3.  Kết nối lại đến vServer\
    \
    \
    \
    **1 -** Nhập password mới đã thay đổi ở Bước 2 cho user stackops\
    **2 -** Gõ lệnh sudo -i hoặc sudo su để có quyền thực thi quyền root trên Server

    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddavc0518012f866015e758dd8f477be1ad5.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### _**Phương án 2**_: **Login SSH bằng SSH KEY** <a href="#ketnoivaomaychulinuxbangcongcusshclient-phuongan2-loginsshbangsshkey" id="ketnoivaomaychulinuxbangcongcusshclient-phuongan2-loginsshbangsshkey"></a>

Nếu bạn đã tạo một SSH Key Pair trên portal VNGCLOUD (_Nhấp vào_ [_**đây**_](https://docs.vngcloud.vn/display/ONVINA/SSH+Keys+HCM+03) _để xem hướng dẫn tạo SSH Keys_) và có add SSH Key vô vServer trong quá trình khởi tạo, bạn có thể thực hiện các bước sau đây

1.  Sử dụng Terminal của Linux để kết nối đến vServer\
    \


    | `ssh -i ~/Download/private_key01.pem -p 234` `stackops@61.28.233.113` |
    | --------------------------------------------------------------------- |
2.  Thay đổi password cho user stackops ở lần đầu tiên login\
    \
    \
    \
    **1 -** Nhập password của user stackops với nội dung là **instancePassword** trong email\
    **2 -** Nhập new password cho user stackops để dùng cho login sau này\
    **3 -** Nhập lại new password cho user stackops để dùng cho login sau này\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddavab40475527cfecafa102351f46a7d4fb.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
3.  Kết nối lại đến vServer\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddav5d99c6c67278dedcb58856d15b62ba28.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

### **Đối với Client thuộc hệ điều hành Window** <a href="#ketnoivaomaychulinuxbangcongcusshclient-doivoiclientthuochedieuhanhwindow" id="ketnoivaomaychulinuxbangcongcusshclient-doivoiclientthuochedieuhanhwindow"></a>

_**Phương án 1**_**: Login SSH bằng password**

1.  Sử dụng Putty của Windows để kết nối đến vServer\
    \
    \
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddav10df9d8abb709c3d868645d7e28adc11.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddav6e80b3ab1314c67cd1ef4c0274fc4e72.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
2.  Thay đổi password cho user stackops ở lần đầu tiên login\
    \
    \
    \
    **1 -** Nhập password của user stackops với nội dung là **instancePassword** email\
    **2 -** Nhập lại password của user stackops với nội dung là **instancePassword** email\
    **3 -** Nhập new password cho user stackops để dùng cho login sau này\
    **4 -** Nhập lại new password cho user stackops để dùng cho login sau này\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddavcbd733454b766bb045f267d2db1ce607.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
3.  Kết nối lại đến vServer\
    \
    \
    \
    **1 -** Nhập password mới đã thay đổi ở Bước 2 cho user stackops\
    **2 -** Gõ lệnh sudo -i hoặc sudo su để có quyền thực thi quyền root trên Server

    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddav8dafb46ee04530a331aeef5ac72047fa.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

_**Option 2**_: **Login SSH bằng SSH KEY**\
Nếu bạn đã tạo một SSH Key Pair trên portal VNGCLOUD (_Nhấp vào_ [_**đây**_](https://docs.vngcloud.vn/display/ONVINA/SSH+Keys+HCM+03) _để xem hướng dẫn tạo SSH Keys_) và có add SSH Key vô vServer trong quá trình khởi tạo, bạn có thể thực hiện các bước sau đây

1.  Dùng putty-gen để convert file **key.pem** đã download thành file **key.ppk**\
    \
    \
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddav7679555bfbb6439237fffdc106a76e2d.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddavd7e2274d07354de680f999a6452282ff.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
2.  Sử dụng Putty của Windows để kết nối đến vServer, authen bằng file **key.ppk** đã tạo ra ở trên\
    \
    \
    \
    \
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddav10df9d8abb709c3d868645d7e28adc11.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddav6e80b3ab1314c67cd1ef4c0274fc4e72.png?version=1&#x26;modificationDate=1681439919000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddav579b9aebecec54acba532f22a56d9b6b.png?version=1&#x26;modificationDate=1681439920000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
3.  Thay đổi password cho user stackops ở lần đầu tiên login\
    \
    \
    \
    **1 -** Nhập password của user stackops với nội dung là **instancePassword** email\
    **2 -** Nhập new password cho user stackops để dùng cho login sau này\
    **3 -** Nhập lại new password cho user stackops để dùng cho login sau này\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddavaeb40edb06de4e5e0a70690e24480fef.png?version=1&#x26;modificationDate=1681439920000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
4.  Kết nối lại đến vServer\
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650301/worddavdf51b4ff159865c247926e017937ad93.png?version=1&#x26;modificationDate=1681439920000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
