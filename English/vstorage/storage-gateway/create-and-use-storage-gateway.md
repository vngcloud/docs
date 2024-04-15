# Create and Use Storage Gateway

#### Create storage gateway <a href="#createandusestoragegateway-createstoragegateway" id="createandusestoragegateway-createstoragegateway"></a>

1. On VNG Cloud console portal, choose **Storage Gateway**

&#x20; ![](https://docs.vngcloud.vn/download/attachments/69468545/image2023-12-26\_9-25-29.png?version=1\&modificationDate=1703557531000\&api=v2)2. On vStorage Gateway Portal, choose **Go to vMarketPlace**

&#x20;![](https://docs.vngcloud.vn/download/attachments/69468545/image2020-7-14\_7-33-14.png?version=1\&modificationDate=1703557683000\&api=v2)

3\. After that, you should lauch VM and setting information

&#x20;![](https://docs.vngcloud.vn/download/attachments/69468545/image2020-7-14\_7-33-31.png?version=1\&modificationDate=1703557684000\&api=v2)

4\. Dùng browser truy cập vào WAN IP của VM đã tạo: Đăng nhập với tài khoản được gửi về email đăng ký vngcloud (lần đăng nhập đầu tiên sẽ đổi lại password mặc định)&#x20;

&#x20;![](https://docs.vngcloud.vn/download/attachments/69468545/image2020-7-14\_7-34-2.png?version=1\&modificationDate=1703557684000\&api=v2)

\* Lưu ý: Security Groups cần mở thêm các port sau để share được dữ liệu:

\- port web: 80,443&#x20;

\- port share:

\+ port 445,139: nếu sử dụng SMB

\+ port 111,2049,34567: nếu sử dụng NFS

#### 2. Tạo file share  <a href="#createandusestoragegateway-2.taofileshare" id="createandusestoragegateway-2.taofileshare"></a>

**2.1 Tạo credential**

**Credential** chọn **create credentials:**&#x20;

&#x20;![](https://docs.vngcloud.vn/download/attachments/69468545/image2020-7-14\_7-35-36.png?version=1\&modificationDate=1703557684000\&api=v2)

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

[Hướng dẫn tạo s3 key](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2721352)

&#x20;**2.2 Tạo file share**

Chọn **file share** rồi chọn **create file share**

![](https://docs.vngcloud.vn/download/attachments/69468545/image2020-7-14\_7-46-27.png?version=1\&modificationDate=1703557684000\&api=v2)

Chú thích:

\- vStorage Credential: chọn credential đã tạo bên trên

\- Container:  list container trong project credential (Lưu ý: Container có khoảng trắng / ký tự đặc biệt thì gateway sẽ không nhìn thấy,)

\- cache: sử dụng local dish làm cache để tăng hiệu suất (mặc định là 1GB)

\- client: hỗ trợ nfs và smb

\+ nfs: sử dụng ip để phân quyền, nhập ip và chọn qyền tương ứng

\+ smb: chon user đã tạo ở user

Nhấn create và đợi hoàn tất

![](https://docs.vngcloud.vn/download/attachments/69468545/image2020-7-14\_7-55-5.png?version=1\&modificationDate=1703557684000\&api=v2)

Có thể xem thêm thông tin mount trong **Mount**

![](https://docs.vngcloud.vn/download/attachments/69468545/image2020-7-14\_7-56-19.png?version=1\&modificationDate=1703557684000\&api=v2)

#### 3. Client kết nối và sử dụng file share <a href="#createandusestoragegateway-3.clientketnoivasudungfileshare" id="createandusestoragegateway-3.clientketnoivasudungfileshare"></a>

**3.1 Client nfs**

Trên máy linux, mở terminal gõ lệnh: _apt install nfs-common_

Trên UI gateway File Share -> Show Commands -> nfs -> copy -> dán lệnh vào terminal client

**3.2 Client smb**

Trên window: Trên UI gateway **File Share -> Show Commands -> smb -> window -> copy -> dán vào search của window -> nhập user/password**

Trên máy linhx, cài dặt client:  _apt install cifs-utils_&#x20;

Trên UI gateway **File Share -> Show Commands -> smb -> window -> copy -> dán vào terminal -> nhập user/password**
