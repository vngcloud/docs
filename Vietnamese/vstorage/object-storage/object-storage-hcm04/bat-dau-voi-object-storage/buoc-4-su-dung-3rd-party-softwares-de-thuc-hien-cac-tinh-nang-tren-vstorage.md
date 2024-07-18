# Bước 4: Sử dụng 3rd party softwares để thực hiện các tính năng trên vStorage

## Các usecase cơ bản

Bên dưới là hướng dẫn cho một số use case thông thường bạn có thể thực hiện trên S3 Browser:

### **Tạo / Xóa bucket**

* Thực hiện tạo xóa bucket bằng cách chọn nút New bucket, lúc này bạn thực hiện nhập Bucket name và chọn Create new bucket.

### **Upload / Download file**

* Sau khi đã tạo bucket, bạn chọn vào bucket cần tải file lên/ xuống. Tiếp theo, bạn chọn Upload/ Download tùy theo nhu cầu.

### **Tạo / Xóa Folder**

* Bạn cũng có thể tạo/ xóa folder bằng cách chọn New Folder hoặc Delete.

<figure><img src="../../../../.gitbook/assets/image (589).png" alt=""><figcaption></figcaption></figure>

***

## Các usecase nâng cao

Tiếp theo đây là các hướng dẫn cho các tính năng nâng cao bạn có thể thực hiện trên S3 Browser:

### **ACL**

Để thiết lập ACL cho một bucket bằng S3 Browser, bạn hãy nhấn chuột phải vào bucket, sau đó chọn Edit Permission (ACL) . Trong phần permission, hãy check chọn quyền hạn bạn mong muốn cấp cho người dùng. Chi tiết tham khảo thêm tại [https://s3browser.com/share-s3-bucket-edit-acls.aspx](https://s3browser.com/share-s3-bucket-edit-acls.aspx)

<figure><img src="../../../../.gitbook/assets/image (590).png" alt=""><figcaption></figcaption></figure>

### **SSE-S3**

SSE-S3 (Server-Side Encryption with S3 Managed Keys) là tính năng mã hóa dữ liệu phía máy chủ do Amazon S3 cung cấp. Với SSE-S3, dữ liệu của bạn được mã hóa tự động khi được tải lên S3 và được giải mã tự động khi bạn tải xuống. Hiện tại tính năng này chưa có sẵn, **nếu bạn có nhu cầu sử dụng, hãy gửi yêu cầu sử dụng dịch vụ thông qua ticket tới VNGCloud.**

### **SSE-C**

**SSE-C** (Server-Side Encryption with Customer-Provided Keys) là tính năng mã hóa dữ liệu phía máy chủ do Amazon S3 cung cấp. Giống như SSE-S3, SSE-C mã hóa dữ liệu của bạn tự động khi được tải lên S3 và giải mã tự động khi bạn tải xuống. Tuy nhiên, với SSE-C, bạn cung cấp và quản lý khóa mã hóa của riêng mình, thay vì sử dụng khóa do AWS quản lý. Hiện tại tính năng này chưa có sẵn, **nếu bạn có nhu cầu sử dụng, hãy gửi yêu cầu sử dụng dịch vụ thông qua ticket tới VNGCloud.**

### **Object Locked**



1. **Versioning**
2. **Lifecycle rotation**
3. **Lifecycle transit (No)**
4. **CORS**
5. **IP range ACLs**
6. **Public/ Private bucket**
7. **Bucket policy**
