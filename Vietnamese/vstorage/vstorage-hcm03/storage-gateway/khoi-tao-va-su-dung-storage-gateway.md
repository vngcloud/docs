# Khởi tạo và sử dụng Storage Gateway

#### Hướng dẫn khởi tạo storage gateway <a href="#khoitaovasudungstoragegateway-1.taostoragegateway" id="khoitaovasudungstoragegateway-1.taostoragegateway"></a>

1. Truy cập trang chủ VNGCloud tại [đây](https://dashboard.console.vngcloud.vn/). Chọn Service: **vStorage**, sau đó chọn **Storage Gateway**:

<figure><img src="../../../.gitbook/assets/image (555).png" alt=""><figcaption></figcaption></figure>

2. Tại trang vMarketplace, chọn **Launch on Computer Engine**

<figure><img src="../../../.gitbook/assets/image (556).png" alt=""><figcaption></figcaption></figure>

3. Bạn nhập thông tin App mong muốn, lựa chọn Instance phù hợp, lựa chọn loại ổ đĩa và kích thước phù hợp, sau đó chọn network, security mong muốn và chọn **Launch Application**

<figure><img src="../../../.gitbook/assets/image (557).png" alt=""><figcaption></figcaption></figure>

Sau khi Application được tạo thành công, sẽ có email thông tin VM gửi về tài khoản của bạn. Dùng browser truy cập vào WAN IP của VM đã tạo: Đăng nhập với tài khoản được gửi về email đăng ký vngcloud (lần đăng nhập đầu tiên sẽ đổi lại password mặc định)

{% hint style="info" %}
**Chú ý:**

Security Groups cần mở thêm các port sau để share được dữ liệu:

* port web: 80,443&#x20;
* port share:
  * port 445,139: nếu sử dụng SMB
  * port 111,2049,34567: nếu sử dụng NFS
{% endhint %}

***

#### Hướng dẫn tạo file share  <a href="#khoitaovasudungstoragegateway-2.taofileshare" id="khoitaovasudungstoragegateway-2.taofileshare"></a>

**2.1 Tạo credential**

**Credential** chọn **create credentials:**&#x20;

Trong đó:&#x20;

\- Region: region của project vstorage lấy trên portal&#x20;

\- Project ID: lấy trên portal&#x20;

\- Provider: chọn S3 hoặc Swift&#x20;

Nếu dùng Swift&#x20;

\+ username: thông tin vstorage trong mail lúc tạo vstorage đầu tiên&#x20;

\+ password: trong mail&#x20;

Dùng S3:&#x20;

\+ Access key: lấy trên portal&#x20;

\+ Secret key: lấy trên portal&#x20;

&#x20;**2.2 Tạo file share**

Chọn **file share** rồi chọn **create file share**

Chú thích:

\- vStorage Credential: chọn credential đã tạo bên trên

\- Container:  list container trong project credential (Lưu ý: Container có khoảng trắng / ký tự đặc biệt thì gateway sẽ không nhìn thấy,)

\- cache: sử dụng local dish làm cache để tăng hiệu suất (mặc định là 1GB)

\- client: hỗ trợ nfs và smb

\+ nfs: sử dụng ip để phân quyền, nhập ip và chọn qyền tương ứng

\+ smb: chon user đã tạo ở user

Nhấn create và đợi hoàn tất

Có thể xem thêm thông tin mount trong **Mount**

#### 3. Client kết nối và sử dụng file share <a href="#khoitaovasudungstoragegateway-3.clientketnoivasudungfileshare" id="khoitaovasudungstoragegateway-3.clientketnoivasudungfileshare"></a>

**3.1 Client nfs**

Trên máy linux, mở terminal gõ lệnh: _apt install nfs-common_

Trên UI gateway File Share -> Show Commands -> nfs -> copy -> dán lệnh vào terminal client

**3.2 Client smb**

Trên window: Trên UI gateway **File Share -> Show Commands -> smb -> window -> copy -> dán vào search của window -> nhập user/password**

Trên máy linhx, cài dặt client:  _apt install cifs-utils_&#x20;

Trên UI gateway **File Share -> Show Commands -> smb -> window -> copy -> dán vào terminal -> nhập user/password**
