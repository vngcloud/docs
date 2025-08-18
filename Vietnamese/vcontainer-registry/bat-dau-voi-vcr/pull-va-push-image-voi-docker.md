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

## Khởi tạo Repository User

**Repository User** là người dùng được tạo riêng để phục vụ cho việc **Push** và **Pull Docker Image**. Repository User có thể gắn quyền truy cập cụ thể đến từng Repository, giúp kiểm soát bảo mật và phân quyền hiệu quả.

Thực hiện theo các bước sau để khởi tạo một Repository user:

**Bước 1**: Truy cập Portal của vContainer Registry.&#x20;

* Với **Region HCM**: [https://vcr.console.vngcloud.vn/repository/list](https://vcr.console.vngcloud.vn/repository/list)
* Với **Region HAN**: [https://han-1.console.vngcloud.vn/vcr/repository/list](https://han-1.console.vngcloud.vn/vcr/repository/list)

**Bước 2:** Chọn mục **Reposity** sau đó chọn vào **Repository** cần tạo **Repository User**, tiếp tục chọn mục **Repository User.** Tiếp tục chọn **Create a user**

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 3:** Thực hiện nhập **User name**, chọn **Expiration Date**, nhập **Description** nếu có sau đó chọn chọn **Permission** mong muốn tùy theo nhu cầu của bạn.

**Bước 4:** Nhấn **"Create"** để hoàn tất quá trình khởi tạo.

<figure><img src="../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

Sau khi user được tạo, bạn hãy nhớ lưu thông tin Secret key lại để sử dụng, ví dụ:

<figure><img src="../../.gitbook/assets/image (11) (1).png" alt="" width="346"><figcaption></figcaption></figure>

## Thực hiện PULL/ PUSH Image

Sau khi đã khởi tạo Repository và Repository User, bạn có thể bắt đầu push Docker image lên hệ thống vContainer Registry. Trước tiên, bạn cần:&#x20;

* Đảm bảo Docker đã được cài đặt và đang chạy.
* Đã tạo Repository và Repository User có quyền **Pull/ Push**.
* Lấy thông tin **Username** và **Secret key** của Repository User vừa tạo.

Bên dưới là ví dụ cho việc pull/ push image nginx trên vCR:

**Bước 1:** Thực hiện **pull** image nginx về máy local theo lệnh:

```docker
docker pull nginx:latest
```

**Bươc 2:** Thực hiện login vào vCR qua lệnh:

* Với **Region HCM**:

```docker
docker login vcr.vngcloud.vn -u <repository_user>
```

* Với **Region HAN**:

```docker
docker login vcr-han.vngcloud.vn -u <repository_user>
```

* Ví dụ, câu lệnh dưới tôi sử dụng để login vào repo demo:

```docker
docker login vcr-han.vngcloud.vn -u 53461-user_demo
```

**Bước 3:** Gán tag cho image nginx

* Với **Region HCM:**

```docker
docker tag SOURCE_IMAGE[:TAG] vcr.vngcloud.vn/REPO_NAME/IMAGE[:TAG]
```

* Với **Region HAN:**

```docker
docker tag SOURCE_IMAGE[:TAG] vcr-han.vngcloud.vn/REPO_NAME/IMAGE[:TAG]
```

* Ví dụ, câu lệnh dưới tôi sử dụng để gán tag cho image nginx:

```docker
docker tag nginx:latest vcr-han.vngcloud.vn/53461-repo_demo/nginx-demo:latest
```

**Bước 4:** Thực hiện push image lên repo qua lệnh:

* Với **Region HCM:**

```docker
docker push vcr.vngcloud.vn/REPO_NAME/IMAGE[:TAG]
```

* Với **Region HAN:**

```docker
docker push vcr-han.vngcloud.vn/REPO_NAME/IMAGE[:TAG]
```

* Ví dụ, câu lệnh dưới tôi sử dụng để push image lên demo\_repo:

```docker
docker push vcr-han.vngcloud.vn/53461-repo_demo/nginx-demo:latest
```
