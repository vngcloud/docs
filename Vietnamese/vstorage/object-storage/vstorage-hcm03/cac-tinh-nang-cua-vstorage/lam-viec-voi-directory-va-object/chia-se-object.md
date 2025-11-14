# Chia sẻ object

Mặc định, tất cả các object trong vStorage là riêng tư. Chỉ chủ sở hữu các object này mới có quyền truy cập chúng. Tuy nhiên, chủ sở hữu các object có thể tùy chọn chia sẻ chúng với người dùng khác bằng cách tạo ra các URL tạm thời. Ở đây chúng tôi cung cấp cho bạn 2 loại URL bao gồm:

* **Temporary URL**: sử dụng thông tin chứng thực là tài khoản OpenStack Swift của bạn.
* **Presigned URL**: sử dụng thông tin chứng thực là tài khoản S3 key của bạn.

Khi bạn tạo một Temporary URL hay Presigned URL được chỉ định cho một object của bạn, bạn phải cung cấp thông tin chứng thực bảo mật của mình, sau đó chỉ định tên container, tên object và ngày giờ hết hạn của URL tương ứng. Các URL này chỉ hợp lệ trong khoảng thời gian mà bạn chỉ định trước. Bất kỳ ai nhận được URL này đều có thể Xem hoặc Tải xuống object. Chúng tôi khuyên bạn nên cân nhắc kỹ đối tượng bạn muốn chia sẻ cũng như thời gian bạn muốn chia sẻ tài nguyên của mình đến những đối tượng đó. Để biết thêm chi tiết về cách bảo vệ các URL, hãy xem [Phân quyền truy cập](../../quan-ly-truy-cap/).

Để thực hiện chia sẻ object, hãy làm theo hướng dẫn bên dưới:

{% tabs %}
{% tab title="Sử dụng vStorage Portal" %}
Để thực hiện chia sẻ một object trong một container, bạn có thể thực hiện theo các bước bên dưới:

1. Đăng nhập vào [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).
2. Chọn **project, container** sau đó chọn một hoặc nhiều các **object** bạn muốn thực hiện chia sẻ.
3. Chọn ![](https://docs.vngcloud.vn/download/thumbnails/49648532/image2023-3-6_10-50-12.png?version=1\&modificationDate=1678074613000\&api=v2)hoặc chọn biểu tượng ![](https://docs.vngcloud.vn/download/thumbnails/49648532/image2023-2-6_10-20-54.png?version=1\&modificationDate=1678074600000\&api=v2)tại **object** bạn muốn thực hiện chia sẻ và chọn![](https://docs.vngcloud.vn/download/thumbnails/49648532/image2023-3-6_10-50-38.png?version=1\&modificationDate=1678074639000\&api=v2)**.**
4. Chọn **Protocol** là:
5. **OpenStack Swift** nếu bạn muốn tạo đường dẫn **Temporary URL.**
6. **S3** nếu bạn muốn tạo đường dẫn **Presigned URL.**

5\. Chọn **Mode**:

* Nếu **Protocol** là **OpenStack Swift** thì bạn có thể chọn **Mode** là **Download** hoặc **View**.
* Nếu **Protocol** là **S3** thì mặc định đường dẫn **Presigned URL** sẽ được sử dụng để **View** object.

6\. Nếu bạn chọn Protocol là S3 thì bạn cần nhập thông tin **S3 key** tại đây. Thông tin S3 key có thể lấy tại IAM. Bạn có thể chọn [Nhấn vào đây để vào vIAM và quản lý s3 keys.](https://iam.console.vngcloud.vn/vstorage-credentials/s3) để xem thông tin chi tiết các cặp s3 key đã tạo cũng như tạo mới cặp S3 key để sử dụng. Chi tiết tham khảo thêm tại [Khởi tạo S3 key](../../quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials/khoi-tao-s3-key.md).

7\. Nhập **Thời gian hết hạn** bạn muốn chia sẻ object tức là thời gian đường dẫn (Temporary URL) truy cập tới object có hiệu lực. Bạn có thể giới hạn số **ngày**, **giờ**, **phút** mà đường dẫn truy cập tới object tồn tại.

8\. Chọn **Tạo đường dẫn**.

9\. Chọn ![](https://docs.vngcloud.vn/download/thumbnails/49648532/image2023-3-6_10-51-24.png?version=1\&modificationDate=1678074685000\&api=v2) để sao chép từng đường dẫn cho từng object. Mỗi object được chúng tôi tạo ra một URL riêng biệt.

Nếu bạn chia sẻ object thông qua Temporary URL hoặc Presigned URL ở cơ chế View, bạn sẽ nhận được 1 đường dẫn (URL). Bạn sao chép đường dẫn này và dán vào bất kỳ trình duyệt nào mà bạn sử dụng. Khi bạn dán đường dẫn và chọn mở đường dẫn:

* Nếu trình duyệt của bạn hỗ trợ mở trực tiếp loại object thì bạn có thể xem trực tiếp object ngày trên trình duyệt. Khi object đang được mở trên trình duyệt thì thời gian tồn tại của URL vẫn được tính. Nếu URL của bạn còn thời hạn, bạn có thể nhấn chuột phải và tải xuống object ( tải từ trình duyệt về thiết bị cá nhân chứ không phải tải từ vStorage về thiết bị cá nhân). Nếu URL của bạn đã hết hạn, bạn không thể nhấn chuột phải để tải xuống object và khi bạn Reload lại trình duyệt, dữ liệu của object hiển thị cũng sẽ mất.
* Nếu trình duyệt của bạn không hỗ trợ mở trực tiếp loại object này trên trình duyệt thì chúng tôi tự động chuyển cơ chế chia sẻ object qua Download, hệ thống sẽ tự động tải xuống object này về thiết bị cá nhân của bạn.
* Chi tiết từng trình duyệt hỗ trợ mở trực tiếp loại object này tham khảo thêm ở : [![](https://fileinfo.com/svg/favicon.svg)FileInfo.com - The File Format Database](https://fileinfo.com/) .

Để chia sẻ toàn bộ object trong một container, thay vì tạo nhiều URL cho từng object, bạn có thể thực hiện chia sẻ toàn bộ Container thông tua tính năng Chuyển chế độ công khai container. Chi tiết xem tại [Chuyển chế độ công khai container](../lam-viec-voi-container/chuyen-che-do-cong-khai-container.md).
{% endtab %}

{% tab title="Sử dụng vStorage API" %}
Ngoài cổng giao diện quản lý truyền thống, chúng tôi cũng cung cấp API cho phép bạn tích hợp với các ứng dụng, công cụ phía bạn của bạn với vStorage để lưu trữ dữ liệu.

1. [Khởi tạo tài khoản Service Account](../../quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-tai-khoan-service-account.md) nếu chưa có
2. Lấy thông tin access token. Tham khảo tại [Chứng thực với Service Account](../../quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/chung-thuc-voi-service-account.md)
3. Nếu bạn muốn tạo đường dẫn **Presigned URL** thì bạn cần nhập thông tin **S3 key**. Thông tin S3 key có thể lấy tại IAM. Bạn có thể chọn [Nhấn vào đây để vào vIAM và quản lý s3 keys.](https://iam.console.vngcloud.vn/vstorage-credentials/s3) để xem thông tin chi tiết các cặp s3 key đã tạo cũng như tạo mới cặp S3 key để sử dụng. Chi tiết tham khảo thêm tại [Khởi tạo S3 key](../../quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials/khoi-tao-s3-key.md).
4. Lấy đường dẫn Tempoary URL hoặc Presigned URL cho object thông qua vStorage API. Hãy xem [API download/chia sẻ object](https://docs.api.vngcloud.vn/service-docs/vstorage-api.html#tag/object/operation/retrieveDownloadObjectTempURLUsingPOST).

**Ví dụ 1: Lấy temporary URL cho object**

```json
Request:
curl -X POST 'https://hcm03-api.vstorage.vngcloud.vn/api/v1/projects/77bd99c393dc4bf5a796b0c327cd70bd/containers/test/objects/2009009063434563310.jpg/download_tempurls'
-H 'Authorization: Bearer access_token'
-H 'Content-Type: application/json'
-d '{"timeExpire":3600,"urlType":"swift","viewMode":"view"}'
Response:
{
    "errorMsg": null,
    "code": 200,
    "success": true,
    "data": {
        "2009009063434563310.jpg": "https://hcm03.vstorage.vngcloud.vn/v1/AUTH_77bd99c393dc4bf5a796b0c327cd70bd/test/2009009063434563310.jpg?temp_url_sig=465d7f6f07536c4fdcd70b8a53516fe53874bf5f&temp_url_expires=1763095206&inline"
    }
}
```

**Ví dụ 2: Lấy presigned URL cho object**

```json
Request:
curl -X POST 'https://hcm03-api.vstorage.vngcloud.vn/api/v1/projects/77bd99c393dc4bf5a796b0c327cd70bd/containers/test/objects/2009009063434563310.jpg/download_tempurls'
-H 'Authorization: Bearer ***'
-H 'Content-Type: application/json'
-d '{"timeExpire":3600,"urlType":"s3","viewMode":"view","accessKey":"d461f281e569d814dfd491ee989dba28","secretKey":"***"}'
Response:
{
    "errorMsg": null,
    "code": 200,
    "success": true,
    "data": {
        "2009009063434563310.jpg": "https://test.hcm03.vstorage.vngcloud.vn/2009009063434563310.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20251114T034634Z&X-Amz-SignedHeaders=host&X-Amz-Expires=3600&X-Amz-Credential=d461f281e569d814dfd491ee989dba28%2F20251114%2FHCM03%2Fs3%2Faws4_request&X-Amz-Signature=4d5ef43478c90eb681e40ec8e77d2d1b0e6f5e7757f0ba5b8b48a651dd438e3e"
    }
}
```
{% endtab %}

{% tab title="Sử dụng 3rd party softwares" %}
vStorage cũng tương thích với các công cụ phía bạn sử dụng S3 protocol. Bạn có thể dễ dàng sử dụng các công cụ đã quen thuộc như Rclone, s3cmd, Cyberduck,...

Để lấy đường dẫn Temporary URL hoặc Presigned URL nhằm chia sẻ object qua 3rd party software, hãy xem [3rd party softwares](../../3rd-party-softwares/).
{% endtab %}
{% endtabs %}

