# API developers

Object Storage (HCM04) cung cấp một loạt API để quản lý dữ liệu và tương tác với các tài nguyên lưu trữ đám mây của bạn. Dưới đây là một tóm tắt về các loại API chính mà chúng tôi đang cung cấp:

## Authentication

* Type: AWS Signature
* Access Key: khởi tạo và lấy thông tin trên vStorage Portal.
* Secret Key: khởi tạo và lấy thông tin trên vStorage Portal.
* Region: HCM04
* Endpoint: [https://hcm04.vstorage.vngcloud.vn](https://hcm04.vstorage.vngcloud.vn)

Ví dụ:&#x20;

<figure><img src="../../../.gitbook/assets/image (715).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (714).png" alt=""><figcaption></figcaption></figure>

***

## Làm việc với Bucket

Những API này cho phép bạn quản lý các bucket

### 1. Những API cơ bản

*   **Create Bucket**: Tạo một bucket mới.

    * Đường dẫn: `PUT /<bucket-name>`
    * Ví dụ: `PUT`[`https://hcm04.vstorage.vngcloud.vn/demobucket`](https://hcm04.vstorage.vngcloud.vn/demobucket)
    * Hoặc Curl qua lệnh:&#x20;

    ```
    curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket' \
    --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
    --header 'X-Amz-Date: 20240829T041014Z' \
    --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=8b4d67b37ab0ba0c6bb42df8d6451fdb48aba5874a0717798aeee9f4c57b8fe9'
    ```

<figure><img src="../../../.gitbook/assets/image (718).png" alt=""><figcaption></figcaption></figure>

*   **List Buckets**: Liệt kê tất cả các bucket thuộc về người dùng.

    * Đường dẫn: `GET /`
    * Ví dụ: `GET` [`https://hcm04.vstorage.vngcloud.vn/`](https://hcm04.vstorage.vngcloud.vn/demobucket)
    * Hoặc Curl qua lệnh:&#x20;

    ```
    curl --location 'https://hcm04.vstorage.vngcloud.vn/' \
    --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
    --header 'X-Amz-Date: 20240829T041050Z' \
    --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=997d9b761262a6827002384dd9ba21b777ec4f26e84dedd164a5866bf78d348a'
    ```

<figure><img src="../../../.gitbook/assets/image (717).png" alt=""><figcaption></figcaption></figure>

* **Delete Bucket**: Xóa một bucket (chỉ khi bucket rỗng).
  * Đường dẫn: `DELETE /<bucket-name>`
  * Ví dụ: `DELETE` [`https://hcm04.vstorage.vngcloud.vn/demobucket`](https://hcm04.vstorage.vngcloud.vn/demobucket)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --request DELETE 'https://hcm04.vstorage.vngcloud.vn/demobucket' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041239Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=e164da98dd0564eea205ec8624d701d8809afab7ab57867e45a3beb227f8a71d'
      ```

<figure><img src="../../../.gitbook/assets/image (719).png" alt=""><figcaption></figcaption></figure>

* **GET Bucket (List Objects)**: Liệt kê các đối tượng trong một bucket.
  * Đường dẫn: `GET /<bucket-name>`
  * Ví dụ: `GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket`](https://hcm04.vstorage.vngcloud.vn/demobucket)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041313Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=7481242fb41364a753658d7db3b2e95c4b2e10458987e14584dc297330ea7dab'
      ```

<figure><img src="../../../.gitbook/assets/image (720).png" alt=""><figcaption></figcaption></figure>

* **HEAD Bucket**: Kiểm tra sự tồn tại và quyền truy cập vào bucket.
  * Đường dẫn: `HEAD /<bucket-name>`
  * Ví dụ: `HEAD` [`https://hcm04.vstorage.vngcloud.vn/demobucket`](https://hcm04.vstorage.vngcloud.vn/demobucket)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --head 'https://hcm04.vstorage.vngcloud.vn/demobucket' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041336Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=425119560f45bd0cd7a5a58f6835d189e0cc3d7907cdd72bfd84bd6d88f59ae9'
      ```

<figure><img src="../../../.gitbook/assets/image (721).png" alt=""><figcaption></figcaption></figure>

### **2. API Kiểm soát truy cập (Access Control APIs)**

Quản lý quyền truy cập cho các bucket và đối tượng.

* **GET Bucket ACL**: Lấy danh sách quyền kiểm soát truy cập (ACL) của bucket.
  * Đường dẫn: `GET /<bucket-name>?acl`
  * Ví dụ: `GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket?acl`](https://hcm04.vstorage.vngcloud.vn/demobucket?acl)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket?acl=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041447Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=fd112a35fed96929de946f9c48d050c8f15ca1249ae549d7b86664adde8d81cd'
      ```

<figure><img src="../../../.gitbook/assets/image (722).png" alt=""><figcaption></figcaption></figure>

* **PUT Bucket ACL**: Thiết lập ACL cho bucket.
  * Đường dẫn: `PUT /<bucket-name>?acl`
  * Ví dụ: `PUT` [`https://hcm04.vstorage.vngcloud.vn/demobucket?acl`](https://hcm04.vstorage.vngcloud.vn/demobucket?acl)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket?acl=null' \
      --header 'Content-Type: application/xml' \
      --header 'X-Amz-Content-Sha256: beaead3198f7da1e70d03ab969765e0821b24fc913697e929e726aeaebf0eba3' \
      --header 'X-Amz-Date: 20240829T043655Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=content-length;content-type;host;x-amz-content-sha256;x-amz-date, Signature=47e95dfbf5a61141dd1088cc286ee2f187ae78c0f7cc108c20538ac1ee77d18b' \
      --data '<AccessControlPolicy xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
        <Owner>
          <ID>rootuser-092410</ID> <!-- Replace with the bucket owner'\''s canonical user ID -->
          <DisplayName>Demo_user</DisplayName> <!-- Optional: Owner'\''s display name -->
        </Owner>
        <AccessControlList>
          <Grant>
            <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
              <ID>user1-054549</ID> <!-- Replace with the grantee'\''s canonical user ID -->
              <DisplayName>UserA</DisplayName> <!-- Optional: Grantee'\''s display name -->
            </Grantee>
            <Permission>FULL_CONTROL</Permission> <!-- Possible values: FULL_CONTROL, WRITE, WRITE_ACP, READ, READ_ACP -->
          </Grant>
          <Grant>
            <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
              <URI>http://acs.amazonaws.com/groups/global/AllUsers</URI> <!-- All users -->
            </Grantee>
            <Permission>READ</Permission>
          </Grant>
        </AccessControlList>
      </AccessControlPolicy>
      '
      ```

<figure><img src="../../../.gitbook/assets/image (741).png" alt=""><figcaption></figcaption></figure>

* **GET Object ACL**: Lấy ACL của một đối tượng.
  * Đường dẫn: `GET /<bucket-name>/<object-key>?acl`
  * Ví dụ: `GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket/videoplayback.mp4?acl`](https://hcm04.vstorage.vngcloud.vn/demobucket/videoplayback.mp4?acl)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket/videoplayback.mp4?acl=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041603Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=eb53bff6d55ade68e688ea5af5b44ff9da9afb7b361e5e60563f6d0f3e4c763b'
      ```

<figure><img src="../../../.gitbook/assets/image (724).png" alt=""><figcaption></figcaption></figure>

### **3. API Quản Lý Phiên Bản (Versioning)**

Quản lý phiên bản của đối tượng trong bucket.

* **PUT Bucket Versioning**: Bật hoặc tắt tính năng quản lý phiên bản cho bucket.
  * Đường dẫn: `PUT /<bucket-name>?versioning`
  * Ví dụ: `PUT`[`https://hcm04.vstorage.vngcloud.vn/demobucket?versioning`](https://hcm04.vstorage.vngcloud.vn/demobucket?versioning)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket?versioning=null' \
      --header 'Content-Type: application/xml' \
      --header 'X-Amz-Content-Sha256: beaead3198f7da1e70d03ab969765e0821b24fc913697e929e726aeaebf0eba3' \
      --header 'X-Amz-Date: 20240829T041647Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=content-length;content-type;host;x-amz-content-sha256;x-amz-date, Signature=79d17ba3ab6fe55a68df54b423fa17c9633ed24b462ab4727f9997bef28ed3ac' \
      --data '<VersioningConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
         <Status>Enabled</Status>
      </VersioningConfiguration>'
      ```

<figure><img src="../../../.gitbook/assets/image (725).png" alt=""><figcaption></figcaption></figure>

* **GET Bucket Versioning**: Kiểm tra trạng thái quản lý phiên bản của bucket.
  * Đường dẫn: `GET /<bucket-name>?versioning`
  * Ví dụ: `GET` [`https://hcm04.vstorage.vngcloud.vn/demobucket?versioning`](https://hcm04.vstorage.vngcloud.vn/demobucket?versioning)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket?versioning=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041708Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=b45886dbf42a0a6d613a465e38e33f6e59b548c27f361798ea168335fe8243e3'
      ```

<figure><img src="../../../.gitbook/assets/image (726).png" alt=""><figcaption></figcaption></figure>

* **GET Object Versions**: Liệt kê các phiên bản của các đối tượng trong bucket.
  * Đường dẫn: `GET /<bucket-name>?versions`
  * Ví dụ: `GET` [`https://hcm04.vstorage.vngcloud.vn/demobucket/?versions`](https://hcm04.vstorage.vngcloud.vn/demobucket/?versions)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket/?versions=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041846Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=1b4454bcc74c22d919121588f4c26ccc921b69544510ae65de3fdb1c5c9ac274'
      ```

<figure><img src="../../../.gitbook/assets/image (727).png" alt=""><figcaption></figcaption></figure>

### **4. API Lifecycle**&#x20;

Quản lý vòng đời cho bucket và đối tượng:

* **PUT Bucket Lifecycle**: Khởi tạo lifecycle expiration cho một bucket.
  * Đường dẫn: `PUT /<bucket-name>?lifecycle`
  * Ví dụ: `PUT`[`https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle`](https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle=null' \
      --header 'Content-Type: application/xml' \
      --header 'X-Amz-Content-Sha256: beaead3198f7da1e70d03ab969765e0821b24fc913697e929e726aeaebf0eba3' \
      --header 'X-Amz-Date: 20240829T042040Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=content-length;content-type;host;x-amz-content-sha256;x-amz-date, Signature=9bc1af859707fb67367fda2cb60236b2d1b9c4442a9e44a77f918242ae8bca87' \
      --data '<LifecycleConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
          <Rule>
              <Expiration>
                  <Days>1</Days>
              </Expiration>
              <ID>test-lifecyle</ID>
              <Filter>
                  <Prefix>*</Prefix>
              </Filter>
              <Status>Enabled</Status>
          </Rule>
      </LifecycleConfiguration>'
      ```

<figure><img src="../../../.gitbook/assets/image (728).png" alt=""><figcaption></figcaption></figure>

* **GET Bucket Lifecycle**: Lấy thông tin quy tắc vòng đời của bucket.
  * Đường dẫn: `GET /<bucket-name>?lifecycle`
  * Ví dụ: `GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle`](https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042134Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=31f4e56f55429f271348de461934dc4c495856330d333559fa6e9ae983800fbd'
      ```

<figure><img src="../../../.gitbook/assets/image (729).png" alt=""><figcaption></figcaption></figure>

* **DELETE Bucket Lifecycle**: Xóa các quy tắc vòng đời đã thiết lập cho bucket.
  * Đường dẫn: `DELETE /<bucket-name>?lifecycle`
  * Ví dụ: `DELETE`[`https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle`](https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --request DELETE 'https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042209Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=c4ab9fbfa8ca73af115142e0a78103e0292e87af6b70a214f21fe020535c3db0'
      ```

<figure><img src="../../../.gitbook/assets/image (730).png" alt=""><figcaption></figcaption></figure>

### **5. API CORS**

Quản lý truy cập và sử dụng S3 như một dịch vụ lưu trữ trang web tĩnh.

* **PUT Bucket Website**: Thiết lập bucket như một trang web tĩnh.
  * Đường dẫn: `PUT /<bucket-name>?cors`
  * Ví dụ: `PUT`[`https://hcm04.vstorage.vngcloud.vn/demobucket?cors`](https://hcm04.vstorage.vngcloud.vn/demobucket?cors)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket?cors=null' \
      --header 'Content-Type: application/xml' \
      --header 'X-Amz-Content-Sha256: beaead3198f7da1e70d03ab969765e0821b24fc913697e929e726aeaebf0eba3' \
      --header 'X-Amz-Date: 20240829T042330Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=content-length;content-type;host;x-amz-content-sha256;x-amz-date, Signature=bdfa1e44bd7f1e52c0c40b73ea484b68dbd2bd80c2a470f41262740614d64a1d' \
      --data '<CORSConfiguration>
        <CORSRule>
          <AllowedOrigin>*</AllowedOrigin> <!-- Allows all origins -->
          <AllowedMethod>GET</AllowedMethod> <!-- Allows the GET HTTP method -->
          <AllowedMethod>POST</AllowedMethod> <!-- Allows the POST HTTP method -->
          <AllowedMethod>PUT</AllowedMethod> <!-- Allows the PUT HTTP method -->
          <AllowedMethod>DELETE</AllowedMethod> <!-- Allows the DELETE HTTP method -->
          <AllowedHeader>*</AllowedHeader> <!-- Allows all headers in requests -->
          <MaxAgeSeconds>3000</MaxAgeSeconds> <!-- Cache the response for preflight requests for 3000 seconds -->
          <ExposeHeader>x-amz-request-id</ExposeHeader> <!-- Exposes the x-amz-request-id header to the client -->
        </CORSRule>
      </CORSConfiguration>
      '
      ```

<figure><img src="../../../.gitbook/assets/image (731).png" alt=""><figcaption></figcaption></figure>

* **GET Bucket Website**: Lấy cấu hình trang web của bucket.
  * Đường dẫn: `GET /<bucket-name>?cors`
  * Ví dụ: `GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket?cors`](https://hcm04.vstorage.vngcloud.vn/demobucket?cors)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket?cors=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042406Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=7632d687924e286195d06f4024d2307c91ccb6df49f6da27328acdd63da63458'
      ```

<figure><img src="../../../.gitbook/assets/image (732).png" alt=""><figcaption></figcaption></figure>

* **DELETE Bucket Website**: Xóa cấu hình trang web của bucket.
  * Đường dẫn: `DELETE /<bucket-name>?website`
  * Ví dụ: `DELETE`[`https://hcm04.vstorage.vngcloud.vn/demobucket?cors`](https://hcm04.vstorage.vngcloud.vn/demobucket?cors)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --request DELETE 'https://hcm04.vstorage.vngcloud.vn/demobucket?cors=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042453Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=78fdf2ff9a9ec36927431dc1f42a8d5fdcb8fd4a1a2c48794cd45c555de3d6b9'
      ```

<figure><img src="../../../.gitbook/assets/image (733).png" alt=""><figcaption></figcaption></figure>

***

## Làm việc với Object

Đây là những API cơ bản để thao tác với các đối tượng (tệp tin) trong S3.

* **PUT Object**: Được sử dụng để tải lên các đối tượng vào một bucket.
  * Đường dẫn: `PUT /<bucket-name>/<object-key>`
  * Ví dụ: `PUT`[`https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt`](https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt' \
      --header 'Content-MD5: h6xLdLBQrPaV94Ve6q8WPQ==' \
      --header 'Content-Type: text/plain' \
      --header 'X-Amz-Content-Sha256: beaead3198f7da1e70d03ab969765e0821b24fc913697e929e726aeaebf0eba3' \
      --header 'X-Amz-Date: 20240829T042534Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=content-length;content-md5;content-type;host;x-amz-content-sha256;x-amz-date, Signature=f0592a78ee6b84a5b7cbc4edaf90e76cacc496a0351c5d10b19b9a574e4e9a1a' \
      --data 'datatest'
      ```

<figure><img src="../../../.gitbook/assets/image (734).png" alt=""><figcaption></figcaption></figure>

* **GET Object**: Lấy một đối tượng từ S3.
  * Đường dẫn: `GET /<bucket-name>/<object-key>`
  * Ví dụ: `GET` [`https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt`](https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042558Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=5d1d085388c0464652e30d68b894e4ff1a6ade86c8f04eed4f9fba7c5968676d'
      ```

<figure><img src="../../../.gitbook/assets/image (735).png" alt=""><figcaption></figcaption></figure>

* **DELETE Object**: Xóa một đối tượng khỏi S3.
  * Đường dẫn: `DELETE /<bucket-name>/<object-key>`
  * Ví dụ: `DELETE` [`https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt`](https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --request DELETE 'https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt' \
      --header 'x-amz-bypass-governance-retention: true' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042811Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-bypass-governance-retention;x-amz-content-sha256;x-amz-date, Signature=54babdc95afd251946a37352d569f825cc5bce8c7b900c0c03874fb3554fdf6c'
      ```

<figure><img src="../../../.gitbook/assets/image (739).png" alt=""><figcaption></figcaption></figure>

* **HEAD Object**: Truy vấn metadata của đối tượng mà không cần tải về nội dung.
  * Đường dẫn: `HEAD /<bucket-name>/<object-key>`
  * Ví dụ: `HEAD`[`https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt`](https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt)
  *   Hoặc Curl qua lệnh:&#x20;

      ```
      curl --location --head 'https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042639Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=0fe5fc5caca290919c3782c74f793c0f7cfe36f4f2c7829de8b895bab51ac7d1'
      ```

<figure><img src="../../../.gitbook/assets/image (736).png" alt=""><figcaption></figcaption></figure>

* **COPY Object**: Sao chép một đối tượng từ một vị trí S3 này sang một vị trí khác.
  * Request: `PUT /<destination-bucket>/<destination-object-key>` với header `x-amz-copy-source`.
  * Ví dụ: `PUT` [`https://hcm04.vstorage.vngcloud.vn/demobucket01/demoobject.txt`](https://hcm04.vstorage.vngcloud.vn/demobucket01/demoobject.txt)
  * Hoặc Curl qua lệnh:&#x20;

```
curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket01/demoobject.txt' \
--header 'x-amz-copy-source: /demobucket/demoobject.txt' \
--header 'x-amz-object-lock-legal-hold: OFF' \
--header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
--header 'X-Amz-Date: 20240829T040428Z' \
--header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-copy-source;x-amz-date;x-amz-object-lock-legal-hold, Signature=bf53eedc8b407de21d94c73191940f2257a6c9759f411e844c912de3c2b26ee9'
```

<figure><img src="../../../.gitbook/assets/image (737).png" alt=""><figcaption></figcaption></figure>