# \[Rclone] Sync data from AWS S3 to vStorage

Rclone is a tool that helps synchronize data and directories to various storage services, including AWS S3, Google Cloud, Dropbox, vStorage,...

Below is our guide to help you set up replicating data/migrating data from AWS S3 to vStorage.

**Note**: VNG Cloud recommends using the **latest version of rclone** for the best experience.

**Warning:**

1. Do not use Rclone versions that are too old or too new on operating systems that are too outdated or too recent, as it may result in errors.
2. It is not recommended to use rclone sync because, during sync, it copies the **source** to **destination** and deletes the differences at **destination** (making **destination** a copy of **source**), which can lead to accidental deletion of data if incorrect source or **destination** information is provided. It is advised to use rclone copy.
3. There are some issues when using rclone mount to mount vStorage containers (buckets) as local directories for use:\
   \+ Unable to copy, rename, move.\
   \+ Unable to list quickly.\
   \+ No permissions like on traditional filesystems: rwx, uid, gid,...

#### Set up <a href="#id-rclone-syncdatafromawss3tovstorage-setup" id="id-rclone-syncdatafromawss3tovstorage-setup"></a>

> $ curl [https://rclone.org/install.sh](https://rclone.org/install.sh) | sudo bash

***

#### Chuẩn bị thông tin  <a href="#id-rclone-syncdatafromawss3tovstorage-chuanbithongtin" id="id-rclone-syncdatafromawss3tovstorage-chuanbithongtin"></a>

**Chuẩn bị thông tin Source**

Thực hiện lấy thông tin access\_key\_id và secret\_access\_key\_id của AWS S3 theo hướng dẫn bên dưới:

1. Truy cập vào **portal AWS**, chọn **Account**.
2. Chọn **Security Credentials.**&#x20;

![](https://docs.vngcloud.vn/download/attachments/69468592/image2023-11-13\_9-35-27.png?version=1\&modificationDate=1703573814000\&api=v2)

\


&#x20;3\. Tại mục Access Key, bạn sẽ lấy được access\_key\_id và secret\_key tương ứng đang có. Nếu bạn chưa có access\_key\_id và secret\_key nào, hãy chọn **Create Access Key** và tiếp tục thực hiện các bước tạo mới access\_key.&#x20;

![](https://docs.vngcloud.vn/download/attachments/69468592/image2023-11-13\_9-38-30.png?version=1\&modificationDate=1703573814000\&api=v2)\


\


**Chuẩn bị thông tin Destination**

Thực hiện lấy thông tin access\_key và secret\_key mà bạn đã khởi tạo để truy cập vào vStorage thông qua vIAM theo hướng dẫn tại [Khởi tạo S3 key](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59804857).

***

#### Cấu hình Rclone <a href="#id-rclone-syncdatafromawss3tovstorage-cauhinhrclone" id="id-rclone-syncdatafromawss3tovstorage-cauhinhrclone"></a>

**Tạo file cấu hình Rclone trên máy**

> $ vi \~/.config/rclone/rclone.conf

**Nội dung file cấu hình như sau**

| <p><code>~/.config/rclone/rclone.conf</code></p><p><code>[vstorage]</code><br><code>type = s3</code><br><code>provider = Other</code><br><code>env_auth = false</code><br><code>access_key_id = &#x3C;access_key_vStorage></code><br><code>secret_access_key = &#x3C;secret_key_vStorage></code><br><code>endpoint =</code> <a href="https://hcm01.vstorage.vngcloud.vn/"><code>https://hcm01.vstorage.vngcloud.vn/</code></a><br><code>acl = private</code><br><code>v2_auth = true</code><br><code>region = other-v2-signature</code><br><code>location_constraint = HCM01</code></p><p><br></p><p><br></p><p><code>[awss3]</code><br><code>type = s3</code><br><code>provider = AWS</code><br><code>env_auth = false</code><br><code>access_key_id = &#x3C;access_key_id_S3></code><br><code>secret_access_key = &#x3C;secret_access_key_S3></code><br><code>region = ap-southeast-1</code><br><code>location_constraint = ap-southeast-1</code><br><code>acl = private</code></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**Kiểm tra thông tin cấu hình Rclone**

> $ rclone config

## 4. Copy data từ AWS S3 → VNG Cloud S3 vStorage.  <a href="#id-rclone-syncdatafromawss3tovstorage-4.copydatatuawss3-vngclouds3vstorage" id="id-rclone-syncdatafromawss3tovstorage-4.copydatatuawss3-vngclouds3vstorage"></a>

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
