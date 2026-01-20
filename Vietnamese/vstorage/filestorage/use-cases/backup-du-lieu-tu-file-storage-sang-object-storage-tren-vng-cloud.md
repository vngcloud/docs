# Backup dữ liệu từ NFS File Storage sang Object Storage trên GreenNode

Để đảm bảo an toàn và khả năng phục hồi dữ liệu, việc sao lưu (backup) định kỳ dữ liệu từ **File Storage** sang **Object Storage** là một giải pháp cần thiết trong hạ tầng hiện đại.&#x20;

GreenNode cung cấp dịch vụ **Object Storage**, tương thích với chuẩn S3, giúp dễ dàng tích hợp và sao lưu dữ liệu từ máy chủ hoặc các hệ thống lưu trữ nội bộ.

## Các công cụ phổ biến để backup dữ liệu lên vStorage:

* **`aws-cli`**: Công cụ chính thức của AWS, hoạt động tốt với các dịch vụ S3-compatible.
* **`rclone`** _(Khuyến nghị)_: Hỗ trợ nhiều backend, dễ dàng cài đăt và cấu hình với nhiều tuỳ chọn nâng cao.
* **`s3cmd`**: Dễ sử dụng nếu bạn quen dòng lệnh cổ điển, hỗ trợ S3 API chuẩn.

Trong tài liệu này, chúng ta sẽ sử dụng **`rclone`**, vì tính linh hoạt và khả năng tương thích tốt với Object Storage của GreenNode.

***

## Điều kiện cần

### Máy chủ cần backup

* Đã **mount File Storage** vào máy (VD: tôi đã mount file storage tới thư mục `/mnt/demo`)
* Mặc định, nếu máy chủ của bạn truy cập được tới internet, việc backup sẽ đi theo đường public. Bạn có thể thiết lập việc backup đi qua đường private nhưng máy chủ của bạn lúc này cần kết nối được tới **endpoint của vstorage.**&#x20;

Dưới đây là hướng dẫn cách tạo endpoint để kết nối vStorage thông qua dịch vụ Endpoint trên hệ thống vServer, nhằm đảm bảo backup đi qua đường private:

**Bước 1:** Đăng nhập vào Portal của hệ thống vServer tại [https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server)

**Bước 2:** Chọn mục **Endpoint**.

<figure><img src="../../../.gitbook/assets/image (1063).png" alt=""><figcaption></figcaption></figure>

**Bước 3:** Trên trang chủ của dịch vụ **vNetwork.**&#x20;

* Vào mục **Endpoint sau đó chọn Create an Endpoint.**

<figure><img src="../../../.gitbook/assets/image (1064).png" alt=""><figcaption></figcaption></figure>

**Bước 4:** Thiết lập thông số **Endpoint**

* **Endpoint name:** nhập tên gợi nhớ của endpoint. Endpoint name là bắt buộc, dài tối thiểu 5 tới tối đa 50 ký tự và chỉ bao gồm các chữ cái, ký tự sau a-z, A-Z, 0-9, '\_', '-'
* **Region:** chọn Region bạn muốn thực hiện tạo endpoint.&#x20;
  * Nếu bạn muốn backup vào vStorage trên region **HCM04, HCM03**: vui lòng chọn Region **HCM-03** tại đây.
  * Nếu bạn muốn backup vào vStorage trên region **HAN02**: vui lòng chọn Region **HAN-01** tại đâ&#x79;**.**
* **Zone**: chọn Zone bạn muốn endpoint được khởi tạo.&#x20;
* **Service Selection**:&#x20;
  * Nếu bạn chọn Region HCM-03: tại đây bạn có thể chọn&#x20;
    * `vstorage.hcm03`: nếu bạn muốn endpoint này sẽ tạo kết nối từ máy chủ của bạn tới vStorage trên region **HCM03**.
    * `vstorage.hcm04`: nếu bạn muốn endpoint này sẽ tạo kết nối từ máy chủ của bạn tới vStorage trên region **HCM04**.
  * Nếu bạn chọn Region HAN-02: tại đây bạn có thể chọn&#x20;
    * `vstorage.han02`: nếu bạn muốn endpoint này sẽ tạo kết nối từ máy chủ của bạn tới vStorage trên region **HAN02**.
* **Tag:** bạn có thể thêm một hoặc nhiều tag để quản lý endpoint theo cấu trúc key-value.
* **VPC**: Chọn VPC nơi các máy chủ (vServer) của bạn đang hoạt động.
* **Subnet**: Chọn subnet có IP mà máy chủ của bạn đang sử dụng.

Trong ví dụ dưới, tôi sẽ tạo kết nối từ máy chủ của tôi tới vStorage HCM04:

<figure><img src="../../../.gitbook/assets/image (1065).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1066).png" alt=""><figcaption></figcaption></figure>

**Bước 5: Xác nhận và tạo Endpoint**

* Kiểm tra lại thông tin.
* Nhấn **Create Endpoint** để khởi tạo endpoint.
* Chờ vài phút để endpoint được tạo thành công và liên kết với dịch vụ vStorage.

**Bước 6: Kiểm tra kết nối từ máy chủ**

Từ máy chủ vServer, bạn cần add host của enpoint vào máy chủ vserver qua lệnh:&#x20;

```bash
vi /etc/hostsh
```

<figure><img src="../../../.gitbook/assets/image (1067).png" alt=""><figcaption></figcaption></figure>

Bạn có thể dùng `ping`, `curl`, hoặc `telnet` tới địa chỉ endpoint của vStorage để đảm bảo rằng nó đã kết nối thành công qua private network.

Ví dụ:

```bash
telnet hcm04.vstorage.vngcloud.vn 443
```

```bash
-- Ví dụ kết quả như bên dưới là đã kết nối thành công
root@client-nfs:~# telnet hcm04.vstorage.vngcloud.vn 443
Trying 10.7.9.8...
Connected to hcm04.vstorage.vngcloud.vn.
```

### Thông tin cần có

* Bạn đã tạo project, bucket và có đầy đủ thông tin `Access Key` và `Secret Key` có quyền READ/ WHITE vào bucket trên vStorage.&#x20;
* Máy chủ của bạn đã cài đặt sẵn công cụ `rclone`&#x20;

Nếu máy chủ của bạn chưa cài đặt công cụ rclone, vui lòng thực hiện theo hướng dẫn sau đây:&#x20;

**Bước 1:** Thực hiện SSH vào máy chủ của bạn và chạy lệnh:

```bash
curl https://rclone.org/install.sh | sudo bash
```

#### Bước 2: Cấu hình kết nối đến GreenNode

* Thực hiện tạo file config tại thư mục: `~/.config/rclone/rclone.conf` , chỉnh sửa file qua lệnh:

```bash
rclone config 
```

hoặc&#x20;

```bash
vi ~/.config/rclone/rclone.conf
```

* Nếu bạn muốn backup vào vStorage HCM04, nội dung file config sẽ có định dạng sau:&#x20;

```bash
[vstorage]
type = s3
provider = Other
env_auth = false
access_key_id = <<Access key bạn lấy được từ vStorage Portal>>
secret_access_key = <<Secret key hệ thống tạo cho bạn tương ứng với Access key>>
endpoint = https://hcm04.vstorage.vngcloud.vn
```

* Nếu bạn muốn backup vào vStorage HCM03 , nội dung file config sẽ có định dạng sau:&#x20;

```bash
[vstorage]
type = s3
provider = Other
env_auth = false
access_key_id = <<Access key bạn lấy được từ IAM>>
secret_access_key = <<Secret key hệ thống tạo cho bạn tương ứng với Access key>>
endpoint = https://hcm03.vstorage.vngcloud.vn/
acl = private
v2_auth = true
region = other-v2-signature
location_constraint = HCM03
```

* Nếu bạn muốn backup vào vStorage HAN02 , nội dung file config sẽ có định dạng sau:&#x20;

```bash
[vstorage]
type = s3
provider = Other
env_auth = false
access_key_id = <<Access key bạn lấy được từ vStorage Portal>>
secret_access_key = <<Secret key hệ thống tạo cho bạn tương ứng với Access key>>
endpoint = https://han02.vstorage.vngcloud.vn
```

* Sau khi bạn đã tải và thiết lập config cho Rclone, bạn có thể kiểm tra kết nối tới bucket qua lệnh:&#x20;

```bash
rclone lsd vstorage:
```

Ví dụ như bên dưới là kết nối đã đúng và rclone đã list được danh sách bucket trên project mà bạn mong muốn nhận dữ liệu backup:

```bash
          -1 2024-11-11 02:53:22        -1 bucket01
          -1 2024-11-11 02:53:30        -1 bucket02
          -1 2025-04-22 07:44:37        -1 nfs-backup
          -1 2024-11-11 03:36:52        -1 objectlock
```

## Thực hiện backup dữ liệu

Giả sử, tôi đã sử dụng file storage và **mount File Storage** vào máy chủ tại thư mục/mnt/demo. Hiện tại trong thư mục này đang có 4 file như sau:&#x20;

```bash
ls /mnt/demo
NFS1.pdf  NFS2.pdf  NFS3.docx  NFS4.pdf
```

Tiếp theo, tôi sẽ backup các file ở thư mục `/mnt/demo` này vào `nfs-backup` bucket trên vStorage HCM04.

### Thực hiện backup một lần

* Để thực hiện backup, chúng tôi khuyến cáo bạn sử dụng câu lệnh rclone copy như sau:&#x20;

```bash
rclone copy --progress --metadata --checksum --transfers 8 --checkers 8 /mnt/demo vstorage:nfs-backup
```

* `copy`: chỉ sao chép file mới hoặc bị thay đổi
* `sync`: đồng bộ hoàn toàn (sẽ xóa file ở đích nếu không còn tồn tại ở nguồn)
* `> /tmp/abc.log` : nếu muốn lưu log của việc copy hoặc sync vào file abc.log

Ví dụ kết quả chạy thành công sẽ như sau:&#x20;

```bash
rclone copy --progress --metadata --checksum --transfers 8 --checkers 8 /mnt/demo vstorage:nfs-backup
Transferred:       53.592 MiB / 53.592 MiB, 100%, 26.796 MiB/s, ETA 0s
Transferred:            4 / 4, 100%
Elapsed time:         2.4s
```

Lúc này, tại bucket `nfs-backup` trên vStorage, bạn sẽ thấy các tệp tin này như sau:&#x20;

<figure><img src="../../../.gitbook/assets/image (1068).png" alt=""><figcaption></figcaption></figure>

### Thiết lập lịch backup tự động

* Đầu tiên, bạn cần cài đặt crontab trên máy chủ qua lệnh:&#x20;

```bash
sudo apt update
sudo apt install cron -y
```

* Mở crontab qua lệnh:

```bash
crontab -e
```

* Thêm dòng sau để chạy backup mỗi ngày 5 phút một lần:&#x20;

```bash
*/5 * * * * /usr/bin/rclone copy --progress --metadata --checksum --transfers 8 --checkers 8 /mnt/demo vstorage:nfs-backup
```

Sau 5 phút, bạn sẽ thấy hệ thống copy tệp tin mới có qua vStorage như hình:&#x20;

<figure><img src="../../../.gitbook/assets/image (1069).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Chú ý:** Dưới đây là các lưu ý quan trọng khi sử dụng `rclone` để backup lên hệ thống **vStorage**, đặc biệt trong các trường hợp liên quan đến quota, versioning và object lock:

* **Hết quota, không thể backup thêm:** Khi project trên **vStorage đạt ngưỡng quota**, các thao tác `rclone copy` hoặc `sync` sẽ **bị lỗi** vì không thể ghi thêm dữ liệu. Lúc này, bạn cần **Resize quota** (tăng dung lượng thủ công qua Portal) hoặc **Bật tính năng auto-scale quota** nếu hệ thống vStorage hỗ trợ, để tự động tăng dung lượng khi cần.
* **Bật Versioning – Hỗ trợ khôi phục file:** Nên bật versioning để có thể khôi phục các file đã bị ghi đè (overwrite) hoặc đã bị xóa nhầm. Rclone sẽ vẫn hoạt động bình thường khi versioning bật — mỗi lần upload là một phiên bản mới.
* **Object Lock – Có thể gây lỗi khi sync/copy:** Nếu bật tính năng **Object Lock** `rclone sync` hoặc `rclone copy`có thể **bị lỗi** vì không thể xóa object hay ghi đè object đang bị khóa. Lúc này, Rclone sẽ **bỏ qua** file bị lỗi và tiếp tục phần còn lại. Bạn hãy chú ý việc lưu log đầy đủ để kiểm tra lỗi trong mọi trường hợp.
{% endhint %}
