# Backup dữ liệu từ File Storage sang Object Storage trên VNG Cloud

Để đảm bảo an toàn và khả năng phục hồi dữ liệu, việc sao lưu (backup) định kỳ dữ liệu từ **File Storage** sang **Object Storage** là một giải pháp cần thiết trong hạ tầng hiện đại.&#x20;

VNG Cloud cung cấp dịch vụ **Object Storage**, tương thích với chuẩn S3, giúp dễ dàng tích hợp và sao lưu dữ liệu từ máy chủ hoặc các hệ thống lưu trữ nội bộ.

## Các công cụ phổ biến để backup dữ liệu lên vStorage:

* **`aws-cli`**: Công cụ chính thức của AWS, hoạt động tốt với các dịch vụ S3-compatible.
* **`rclone`** _(Khuyến nghị)_: Hỗ trợ nhiều backend, dễ dàng cài đăt và cấu hình với nhiều tuỳ chọn nâng cao.
* **`s3cmd`**: Dễ sử dụng nếu bạn quen dòng lệnh cổ điển, hỗ trợ S3 API chuẩn.

Trong tài liệu này, chúng ta sẽ sử dụng **`rclone`**, vì tính linh hoạt và khả năng tương thích tốt với Object Storage của VNG Cloud.

***

## Điều kiện cần

#### 1. Máy chủ cần backup:

* Đã **mount File Storage** vào máy (VD: tôi đã mount file storage tới thư mục `/mnt/demo`)
* Mặc định, nếu máy chủ của bạn truy cập được tới internet, việc backup sẽ đi theo đường backup. Hoặc đi private nhưng máy chủ lúc này cần kết nối được tới endpoint **của vstorage. Bạn có thể tạo endpoint để kết nối thông qua dịch vụ Endpoint trên hệ thống vServer theo hướng dẫn sau:**

**Bước 1:**&#x20;

<details>

<summary>Nếu bạn muốn backup private</summary>



</details>

#### 2. Thông tin cần có:

* `Access Key` và `Secret Key` từ IAM của VNG Cloud
* Tên `Bucket` đã tạo trên Object Storage
* Cài đặt sẵn công cụ `rclone`

***

### Cài đặt và cấu hình rclone

#### 1. Cài đặt rclone

```bash
curl https://rclone.org/install.sh | sudo bash
```

#### 2. Cấu hình kết nối đến VNG Cloud

```bash
rclone config
```

Làm theo hướng dẫn:

```
[vstorage]
type = s3
provider = Other
env_auth = false
access_key_id = e38043b072c9ef37cfe8a33f31c54b6a
secret_access_key = zw6gSMjIBjgtmQyhBbZFJko4RKQezeAVDjPuPAks
endpoint = https://hcm04.vstorage.vngcloud.vn
```

Nhấn `Enter` cho các bước còn lại để hoàn tất.

***

### Thực hiện backup dữ liệu

#### Câu lệnh sao lưu:

```bash
rclone copy /mnt/filestorage vngcloud:my-backup-bucket/filestorage-backup --progress
```

* `copy`: chỉ sao chép file mới hoặc bị thay đổi
* `sync`: đồng bộ hoàn toàn (sẽ xóa file ở đích nếu không còn tồn tại ở nguồn)

> ✅ Thêm `--dry-run` để kiểm tra trước khi chạy thật

***

### Thiết lập lịch backup tự động

Mở crontab:

```bash
crontab -e
```

Thêm dòng sau để chạy backup mỗi ngày lúc 2h sáng:

```bash
0 2 * * * /usr/bin/rclone copy /mnt/filestorage vngcloud:my-backup-bucket/filestorage-backup --quiet
```

***

### Lưu ý bảo mật & tối ưu

* Chỉ gán quyền cần thiết (write-only hoặc backup-only) cho IAM User
* Bật Versioning trên Bucket nếu cần phục hồi phiên bản cũ
* Theo dõi dung lượng lưu trữ để tối ưu chi phí

***

### Kết luận

Việc sử dụng `rclone` để backup dữ liệu từ File Storage lên Object Storage là phương pháp hiệu quả, an toàn và dễ triển khai. Kết hợp với các chính sách versioning, lifecycle và phân quyền truy cập, bạn có thể đảm bảo dữ liệu quan trọng được bảo vệ tối đa trên hạ tầng VNG Cloud.

***

Bạn muốn mình tạo file Markdown, HTML hay PDF từ nội dung này để lưu trữ nội bộ không?
