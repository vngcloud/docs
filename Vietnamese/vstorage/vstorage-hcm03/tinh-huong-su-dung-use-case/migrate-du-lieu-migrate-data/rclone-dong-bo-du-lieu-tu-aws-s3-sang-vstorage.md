# \[Rclone] Đồng bộ dữ liệu từ AWS S3 sang vStorage

Rclone là công cụ giúp đồng bộ hoá dữ liệu và directory đến nhiều dịch vụ lưu trữ khác nhau, bao gồm AWS S3, Google Cloud, Dropbox, vStorage,...

Bên dưới là hướng dẫn của chúng tôi nhằm giúp bạn thiết lập replicate data/ migrate data từ AWS S3 sang vStorage.

**Lưu ý:** VNG Cloud khuyến khích sử dụng phiên bản **mới nhất của rclone** để có trải nghiệm tốt nhất.&#x20;

**Chú ý:**

1. Không nên sử dụng phiên bản Rclone quá cũ/ quá mới trên các hệ điều hành có phiên bản quá cũ/ quá mới vì có thể gặp lỗi.
2. Không khuyến khích sử dụng rclone sync vì khi sync sẽ copy **source** sang **destination** và xóa phần khác biệt ở **destination** (khiến **destination** trở thành bản sao của **source**), dễ gây ra sự cố xoá nhầm data nếu truyền sai thông tin **source**, **destination**. Khuyến cáo nên dùng rclone copy.
3. &#x20;Có vài vấn đề khi dùng rclone mount để mount các vStorage container (bucket) thành local directory để sử dụng:\
   \+ Không thể copy, rename, move\
   \+ Không thể listing nhanh chóng\
   \+ Không phân quyền như trên các loại filesystem truyền thống: rwx, uid, gid,...

#### Cài đặt <a href="#id-rclone-dongbodulieutuawss3sangvstorage-caidat" id="id-rclone-dongbodulieutuawss3sangvstorage-caidat"></a>

> $ curl [https://rclone.org/install.sh](https://rclone.org/install.sh) | sudo bash

***

#### Chuẩn bị thông tin  <a href="#id-rclone-dongbodulieutuawss3sangvstorage-chuanbithongtin" id="id-rclone-dongbodulieutuawss3sangvstorage-chuanbithongtin"></a>

**Chuẩn bị thông tin Source**

Thực hiện lấy thông tin access\_key\_id và secret\_access\_key\_id của AWS S3 theo hướng dẫn bên dưới:

1. Truy cập vào **portal AWS**, chọn **Account**.
2. Chọn **Security Credentials.**&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/49648978/image2023-11-13_9-35-27.png?version=1&#x26;modificationDate=1699842929000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


&#x20;3\. Tại mục Access Key, bạn sẽ lấy được access\_key\_id và secret\_key tương ứng đang có. Nếu bạn chưa có access\_key\_id và secret\_key nào, hãy chọn **Create Access Key** và tiếp tục thực hiện các bước tạo mới access\_key.&#x20;

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/49648978/image2023-11-13_9-38-30.png?version=1&#x26;modificationDate=1699843112000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


**Chuẩn bị thông tin Destination**

Thực hiện lấy thông tin access\_key và secret\_key mà bạn đã khởi tạo để truy cập vào vStorage thông qua vIAM theo hướng dẫn tại [Khởi tạo S3 key](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59804857).

***

#### Cấu hình Rclone <a href="#id-rclone-dongbodulieutuawss3sangvstorage-cauhinhrclone" id="id-rclone-dongbodulieutuawss3sangvstorage-cauhinhrclone"></a>

**Tạo file cấu hình Rclone trên máy**

> $ vi \~/.config/rclone/rclone.conf

**Nội dung file cấu hình như sau**

| <p><code>~/.config/rclone/rclone.conf</code></p><p><code>[vstorage]</code><br><code>type = s3</code><br><code>provider = Other</code><br><code>env_auth = false</code><br><code>access_key_id = &#x3C;access_key_vStorage></code><br><code>secret_access_key = &#x3C;secret_key_vStorage></code><br><code>endpoint =</code> <a href="https://hcm01.vstorage.vngcloud.vn/"><code>https://hcm01.vstorage.vngcloud.vn/</code></a><br><code>acl = private</code><br><code>v2_auth = true</code><br><code>region = other-v2-signature</code><br><code>location_constraint = HCM01</code></p><p><br></p><p><br></p><p><code>[awss3]</code><br><code>type = s3</code><br><code>provider = AWS</code><br><code>env_auth = false</code><br><code>access_key_id = &#x3C;access_key_id_S3></code><br><code>secret_access_key = &#x3C;secret_access_key_S3></code><br><code>region = ap-southeast-1</code><br><code>location_constraint = ap-southeast-1</code><br><code>acl = private</code></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**Kiểm tra thông tin cấu hình Rclone**

> $ rclone config

## 4. Copy data từ AWS S3 → VNG Cloud S3 vStorage.  <a href="#id-rclone-dongbodulieutuawss3sangvstorage-4.copydatatuawss3-vngclouds3vstorage" id="id-rclone-dongbodulieutuawss3sangvstorage-4.copydatatuawss3-vngclouds3vstorage"></a>

&#x20;

Chạy lệnh: &#x20;

| `rclone copy source:sourcepath dest:destpath` |
| --------------------------------------------- |

Ví dụ: để copy data từ bucket aws-s3-source tới container01 trên hệ thống vStorage, bạn cần chạy cú pháp sau đây:

| `rclone copy awss3:aws-s3-source vstorage:container01` |
| ------------------------------------------------------ |

Kết quả: Trên Portal vStorage, tại Container01 sẽ xuất hiện các file vừa được copy từ AWS S3.&#x20;

**Chú ý:**

1. Đối với trường hợp bạn có dữ liệu quá lớn (từ 20TB) mà không thể tự thực hiện được vui lòng gửi ticket support để được tư vấn hỗ trợ.

\
