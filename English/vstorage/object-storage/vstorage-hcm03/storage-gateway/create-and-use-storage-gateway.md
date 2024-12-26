# Create and Use Storage Gateway

**Hướng dẫn khởi tạo storage gateway**

1. Truy cập trang chủ VNGCloud tại [đây](https://dashboard.console.vngcloud.vn/). Chọn Service: **vStorage**, sau đó chọn **Storage Gateway**:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Frcir0HyPBZPsnCfVV2Bj%252Fimage.png%3Falt%3Dmedia%26token%3D6052f33c-dc01-417e-b73a-1a11de19ffcf&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6ee619cb&#x26;sv=1" alt=""><figcaption></figcaption></figure>

1. Tại trang vMarketplace, chọn **Launch on Computer Engine**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fv2jqhe7z3POx4bFx1Q5n%252Fimage.png%3Falt%3Dmedia%26token%3Ddae869f2-f6ba-4285-ace5-cd5b0e485754&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=8c968905&#x26;sv=1" alt=""><figcaption></figcaption></figure>

1. Bạn nhập thông tin App mong muốn, lựa chọn Instance phù hợp, lựa chọn loại ổ đĩa và kích thước phù hợp, sau đó chọn network, security mong muốn và chọn **Launch Application**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FJDvQxCBJq8iF7CEB4Ncp%252Fimage.png%3Falt%3Dmedia%26token%3D4582a638-64d0-4e1d-9ca6-5865abc730c0&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=3ff0bf5f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Sau khi bạn Launch Application thành công, hệ thống sẽ thực hiện khởi tạo một server tương ứng. Sau khi VM được tạo thành công, bạn hãy truy cập vào địa chỉ External IP của VM và thực hiện đăng nhập với thông tin đăng nhập đã được gửi về email của bạn (lần đăng nhập đầu tiên sẽ đổi lại password mặc định).

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fo3YkbqWClgG28OFR3htL%252Fimage.png%3Falt%3Dmedia%26token%3Db95a55b4-b37a-4e55-baf0-036ab000faab&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7e375025&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Chú ý:**

Security Groups cần mở thêm các port sau để share được dữ liệu:

* port web: 80,443
* port share:
  * port 445,139: nếu sử dụng SMB
  * port 111,2049,34567: nếu sử dụng NFS

***

**Hướng dẫn tạo file share**

1. **Tạo credential**

Tại mục **Credential** chọn C**reate credentials:**

Trong đó:

* Credential name: nhập tên credential mong muốn.
* Region: chọn Region chứa project mà bạn muốn thực hiện lưu trữ trên vStorage.
* Project ID
* Provider: bạn có thể chọn sử dụng S3 key hoặc Swift user tùy chọn.
  * Nếu dùng Swift, bạn cần nhập username và password.
  * Nếu dùng S3 key, bạn cần nhập Access key và Secret key.

Những thông tin này bạn có thể tạo cũng như lấy thông tin trên vStorage Portal và IAM Portal.

1. **Tạo file share**

Chọn **file share** rồi chọn C**reate file share**

Trong đó:

* Volume Information:
  * vStorage Credential: chọn credential đã tạo bên trên.
  * Container: chọn một container trong danh sách container trong project đã được khai báo sử dụng.
* Permission:
  * nfs: phân quyền theo IP, chúng tôi sẽ sử dụng IP để phân quyền, bạn cần nhập IP và chọn quyền tương ứng
  * smb: phân quyền theo User, chúng tôi sẽ sử dụng User để phân quyền, bạn cần chọn User và chọn quyền tương ứng

Chọn **Create** và đợi hoàn tất việc tạo File Share. Bạn cũng có thể xem thêm thông tin mount trong mục **Mount**

<figure><img src="../../../../.gitbook/assets/image (30) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (31) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (32) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**3. Client kết nối và sử dụng file share**

**3.1 Client nfs**

Trên máy linux, mở terminal gõ lệnh: _apt install nfs-common_

Trên UI gateway File Share -> Show Commands -> nfs -> copy -> dán lệnh vào terminal client

**3.2 Client smb**

Trên window: Trên UI gateway **File Share -> Show Commands -> smb -> window -> copy -> dán vào search của window -> nhập user/password**

Trên máy linhx, cài dặt client: _apt install cifs-utils_

Trên UI gateway **File Share -> Show Commands -> smb -> window -> copy -> dán vào terminal -> nhập user/password**

[PreviousStorage gateway](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vstorage/vstorage-hcm03/storage-gateway)[Next](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vstorage/vstorage-hcm03/storage-gateway/ung-dung-gateway-thay-the-fileserver)
