# Pull và Push image với Docker

## Điều kiện cần

* Yêu cầu máy tính đã cài **Docker Engine** hoặc **Docker Desktop.**

## Khởi tạo Repoitory

**Repository** (hay còn gọi là "repo") là nơi **lưu trữ các Docker image**. Repo giống như **một thư mục chứa nhiều phiên bản khác nhau của một ứng dụng** dưới dạng các Docker image. Mỗi phiên bản thường được đánh dấu bằng một `tag` như `:latest`, `:v1.0`, `:2025-04-15`, v.v.

Thực hiện theo các bước sau để khởi tạo một Repository:

**Bước 1**: Truy cập Portal của vContainer Registry.&#x20;

* Với **Region HCM**: [https://vcr.console.vngcloud.vn/repository/list](https://vcr.console.vngcloud.vn/repository/list)
* Với **Region HAN**: [https://han-1.console.vngcloud.vn/vcr/repository/list](https://han-1.console.vngcloud.vn/vcr/repository/list)

**Bước 2:** Chọn mục **Repository** sau đó chọn nút **"Create Repository".**&#x20;

**Bước 3:** Thực hiện nhập **Repository name, Access level và Quota Limit** tùy theo nhu cầu của bạn.

**Bước 4:** Nhấn **"Create"** để hoàn tất quá trình khởi tạo.

<figure><img src="../../.gitbook/assets/image (1059).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1060).png" alt="" width="518"><figcaption></figcaption></figure>

#### 3. Khởi tạo Repository User <a href="#gettingstarted-vcr-3.khoitaorepositoryuser" id="gettingstarted-vcr-3.khoitaorepositoryuser"></a>

**Cách khởi tạo Repository User**

1. Tại trang chủ Container Registry, nhấn vào **menu "Repository User"** phía bên tay phải để truy cập đến danh sách Repository User, nhấn nút **"CreateRepository User"** để bắt đầu tạo mới một Repository User.
2. Một popup **"Create Repository"** hiển thị cho phép bạn điền các thông tin như:
   * **User Name (optional)**: Tên của Repository User, trường hợp không điền tên, hệ thống sẽ tự động sinh ra tên tương ứng. Lưu ý tên sau khi điền/sinh tự động sẽ được add thêm prefix {AccountID} tương ứng với tài khoản VNG Cloud đang đăng nhập.
   * **Expiration Date:** Ngày hết hạn của User. Có 3 chế độ như sau:
     * Để trống: Đồng nghĩa với việc user này không có thời gian expired
     * Điền ngày cụ thể: User này sẽ expired tại thời điểm được chọn. Đối với user bị expired, hệ thống sẽ tạm khóa toàn bộ các tính năng có liên quan đối với Repository User này cho đến khi user được gia hạn thêm thời gian
   * **Description (optional):** Thông tin thêm về Repository User
   * **Repositories (required):** Đính kèm các Repository và cài đặt Permission tương ứng
     * Tìm Repository cần attach theo repository name
     * Nhấn nút "Add"
     * Tại danh sách Repository được thêm vào bên dưới, cài đặt permission tương ứng Push\&Pull/Pull Only
3. Nhấn nút **"Create"** để hoàn tất việc khởi tạo
4. Kiểm tra thông tin Repository vừa khởi tạo tại danh sách

## Khởi tạo Repository User

**Repository** (hay còn gọi là "repo") là nơi **lưu trữ các Docker image**. Repo giống như **một thư mục chứa nhiều phiên bản khác nhau của một ứng dụng** dưới dạng các Docker image. Mỗi phiên bản thường được đánh dấu bằng một `tag` như `:latest`, `:v1.0`, `:2025-04-15`, v.v.

Thực hiện theo các bước sau để khởi tạo một Repository:

**Bước 1**: Truy cập Portal của vContainer Registry.&#x20;

* Với **Region HCM**: [https://vcr.console.vngcloud.vn/repository/list](https://vcr.console.vngcloud.vn/repository/list)
* Với **Region HAN**: [https://han-1.console.vngcloud.vn/vcr/repository/list](https://han-1.console.vngcloud.vn/vcr/repository/list)

**Bước 2:** Chọn **"Create Repository".**&#x20;

**Bước 3:** Thực hiện nhập **Repository name, Access level và Quota Limit** tùy theo nhu cầu của bạn.

**Bước 4:** Nhấn **"Create"** để hoàn tất quá trình khởi tạo.

## Thực hiện Push Image

### Trên Region HCM

### Trên Region HAN

## Thực hiện Pull Image

### Trên Region HCM

### Trên Region HAN
