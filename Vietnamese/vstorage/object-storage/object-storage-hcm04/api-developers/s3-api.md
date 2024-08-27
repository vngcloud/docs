# S3 API

Amazon S3 (Simple Storage Service) cung cấp một loạt API để quản lý dữ liệu và tương tác với các tài nguyên lưu trữ đám mây của bạn. Dưới đây là một tóm tắt về các loại API chính mà Amazon S3 cung cấp:

## Authentication



***

## Làm việc với Bucket

Những API này cho phép bạn quản lý các bucket

### 1. Những API cơ bản

* **Create Bucket**: Tạo một bucket mới.
  * Đường dẫn: `PUT /<bucket-name>`
  * `Ví dụ: PUT /demobucket`

<figure><img src="../../../../.gitbook/assets/image (703).png" alt=""><figcaption></figcaption></figure>

* **List Buckets**: Liệt kê tất cả các bucket thuộc về người dùng.
  * Đường dẫn: `GET /`
* **Delete Bucket**: Xóa một bucket (chỉ khi bucket rỗng).
  * Đường dẫn: `DELETE /<bucket-name>`
* **GET Bucket (List Objects)**: Liệt kê các đối tượng trong một bucket.
  * Đường dẫn: `GET /<bucket-name>`
* **HEAD Bucket**: Kiểm tra sự tồn tại và quyền truy cập vào bucket.
  * Đường dẫn: `HEAD /<bucket-name>`

### **2. API Kiểm soát truy cập (Access Control APIs)**

Quản lý quyền truy cập cho các bucket và đối tượng.

* **GET Bucket ACL**: Lấy danh sách quyền kiểm soát truy cập (ACL) của bucket.
  * Đường dẫn: `GET /<bucket-name>?acl`
* **PUT Bucket ACL**: Thiết lập ACL cho bucket.
  * Đường dẫn: `PUT /<bucket-name>?acl`
* **GET Object ACL**: Lấy ACL của một đối tượng.
  * Đường dẫn: `GET /<bucket-name>/<object-key>?acl`
* **PUT Object ACL**: Thiết lập ACL cho một đối tượng.
  * Đường dẫn: `PUT /<bucket-name>/<object-key>?acl`

### **3. API Quản Lý Phiên Bản (Versioning)**

Quản lý phiên bản của đối tượng trong bucket.

* **PUT Bucket Versioning**: Bật hoặc tắt tính năng quản lý phiên bản cho bucket.
  * Đường dẫn: `PUT /<bucket-name>?versioning`
* **GET Bucket Versioning**: Kiểm tra trạng thái quản lý phiên bản của bucket.
  * Đường dẫn: `GET /<bucket-name>?versioning`
* **GET Object Versions**: Liệt kê các phiên bản của một đối tượng trong bucket.
  * Đường dẫn: `GET /<bucket-name>?versions`

### **4. API Lifecycle**&#x20;

Quản lý vòng đời và chính sách cho bucket và đối tượng.

* **PUT Bucket Lifecycle**: Đặt quy tắc vòng đời cho bucket (tự động xóa hoặc lưu trữ đối tượng sau một thời gian).
  * Đường dẫn: `PUT /<bucket-name>?lifecycle`
* **GET Bucket Lifecycle**: Lấy thông tin quy tắc vòng đời của bucket.
  * Đường dẫn: `GET /<bucket-name>?lifecycle`
* **DELETE Bucket Lifecycle**: Xóa các quy tắc vòng đời đã thiết lập cho bucket.
  * Đường dẫn: `DELETE /<bucket-name>?lifecycle`

### **5. API CORS**

Quản lý truy cập và sử dụng S3 như một dịch vụ lưu trữ trang web tĩnh.

* **PUT Bucket Website**: Thiết lập bucket như một trang web tĩnh.
  * Đường dẫn: `PUT /<bucket-name>?website`
* **GET Bucket Website**: Lấy cấu hình trang web của bucket.
  * Đường dẫn: `GET /<bucket-name>?website`
* **DELETE Bucket Website**: Xóa cấu hình trang web của bucket.
  * Đường dẫn: `DELETE /<bucket-name>?website`

***

## Làm việc với Object

Đây là những API cơ bản để thao tác với các đối tượng (tệp tin) trong S3.

* **PUT Object**: Được sử dụng để tải lên các đối tượng vào một bucket.
  * Đường dẫn: `PUT /<bucket-name>/<object-key>`
  * Yêu cầu bao gồm dữ liệu đối tượng và có thể có các metadata tùy chọn.
  * Ví dụ:&#x20;

<figure><img src="../../../../.gitbook/assets/image (704).png" alt=""><figcaption></figcaption></figure>

* **GET Object**: Lấy một đối tượng từ S3.
  * Đường dẫn: `GET /<bucket-name>/<object-key>`
  * Trả về nội dung của đối tượng và các metadata liên quan.

<figure><img src="../../../../.gitbook/assets/image (705).png" alt=""><figcaption></figcaption></figure>

* **DELETE Object**: Xóa một đối tượng khỏi S3.
  * Đường dẫn: `DELETE /<bucket-name>/<object-key>`

<figure><img src="../../../../.gitbook/assets/image (706).png" alt=""><figcaption></figcaption></figure>

* **HEAD Object**: Truy vấn metadata của đối tượng mà không cần tải về nội dung.
  * Đường dẫn: `HEAD /<bucket-name>/<object-key>`
* **COPY Object**: Sao chép một đối tượng từ một vị trí S3 này sang một vị trí khác.
  * Đường dẫn: `PUT /<destination-bucket>/<destination-object-key>` với header `x-amz-copy-source`.

