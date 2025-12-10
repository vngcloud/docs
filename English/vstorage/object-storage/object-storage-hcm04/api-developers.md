# API Developers

Object Storage (HCM04) provides a range of APIs for managing data and interacting with your cloud storage resources. Here is a summary of the main types of APIs we provide:

* **vStorage API:** you can use **Service Account** to authenticate and work with **projects, buckets, objects, reports** via API.
* **S3 API** : you can use **S3 keys** to authenticate and work with **buckets and objects** via API.

## vStorage API - Authentication <a href="#vstorage-api-authentication" id="vstorage-api-authentication"></a>

Follow the steps below to work with vStorage via Service Account

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list)
2. Select the Integration folder **.**
3. **Select the vStorage API** icon .
4. In the **Authentication** section , you need to fill in the necessary information to configure your vStorage API including:
   1. Enter **the Client ID** . A **Client ID** is a string of characters used by the Service API to identify your application, and is also used to construct the "authorization URL" displayed to the user. You can create and manage **Client IDs** through the vIAM system. **The Client ID** is automatically generated when you create a new **Service Account** .
   2. Enter **the Client Secret** corresponding to **the Client ID** you just entered. The Client ID and Client Secret pair are created and managed by you through the vIAM system. You can select [Click here to manage your Client ID.](https://iam.console.vngcloud.vn/service-accounts) so we can navigate you to the vIAM system and in detail the Service Account management screens.
5. Once you've finished selecting your **authentication** configuration , select **Authentication** to go to the Configuration screen **. Here you can use the vStorage APIs directly, or you can use the API via Postman** . You can always come back here to change your **Authorization** information , then select **Authentication** again to update the S3 Rest API list with your new parameters.

For details, please refer to [https://docs.api.vngcloud.vn/service-docs/vstorage-hcm04-api.html](https://docs.api.vngcloud.vn/service-docs/vstorage-hcm04-api.html) .

<figure><img src="../../../.gitbook/assets/image (19) (1) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (20) (1) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (444) (1).png" alt=""><figcaption></figcaption></figure>

## S3 API - Authentication <a href="#authentication" id="authentication"></a>

* Type: AWS Signature
* Access Key: initialize and retrieve information on the vStorage Portal.
* Secret Key: initialize and retrieve information on vStorage Portal.
* Region: HCM04
* Endpoint: [https://hcm04.vstorage.vngcloud.vn](https://hcm04.vstorage.vngcloud.vn/)

For example:

<figure><img src="../../../.gitbook/assets/image (22) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (23) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

***

## Working with Bucket <a href="#lam-viec-voi-bucket" id="lam-viec-voi-bucket"></a>

These APIs allow you to manage buckets.

### 1. Basic APIs <a href="#id-1.-nhung-api-co-ban" id="id-1.-nhung-api-co-ban"></a>

*   **Create Bucket** : Create a new bucket.

    * Path:`PUT /<bucket-name>`
    * For example: `PUT`[`https://hcm04.vstorage.vngcloud.vn/demobucket`](https://hcm04.vstorage.vngcloud.vn/demobucket)
    * Or Curl via command:

    ```bash
    curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket' \
    --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
    --header 'X-Amz-Date: 20240829T041014Z' \
    --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=8b4d67b37ab0ba0c6bb42df8d6451fdb48aba5874a0717798aeee9f4c57b8fe9'
    ```

<figure><img src="../../../.gitbook/assets/image (25) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

*   **List Buckets** : List all buckets belonging to the user.

    * Path:`GET /`
    * For example:`GET` [`https://hcm04.vstorage.vngcloud.vn/`](https://hcm04.vstorage.vngcloud.vn/demobucket)
    * Or Curl via command:

    ```bash
    curl --location 'https://hcm04.vstorage.vngcloud.vn/' \
    --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
    --header 'X-Amz-Date: 20240829T041050Z' \
    --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=997d9b761262a6827002384dd9ba21b777ec4f26e84dedd164a5866bf78d348a'
    ```

<figure><img src="../../../.gitbook/assets/image (26) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Delete Bucket** : Delete a bucket (only if the bucket is empty).
  * Path:`DELETE /<bucket-name>`
  * For example:`DELETE` [`https://hcm04.vstorage.vngcloud.vn/demobucket`](https://hcm04.vstorage.vngcloud.vn/demobucket)
  *   Or Curl via command:

      ```bash
      curl --location --request DELETE 'https://hcm04.vstorage.vngcloud.vn/demobucket' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041239Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=e164da98dd0564eea205ec8624d701d8809afab7ab57867e45a3beb227f8a71d'
      ```

<figure><img src="../../../.gitbook/assets/image (27) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **GET Bucket (List Objects)** : List objects in a bucket.
  * Path:`GET /<bucket-name>`
  * For example:`GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket`](https://hcm04.vstorage.vngcloud.vn/demobucket)
  *   Or Curl via command:

      ```bash
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041313Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=7481242fb41364a753658d7db3b2e95c4b2e10458987e14584dc297330ea7dab'
      ```

<figure><img src="../../../.gitbook/assets/image (28) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **HEAD Bucket** : Check for existence and access to bucket.
  * Path:`HEAD /<bucket-name>`
  * For example:`HEAD` [`https://hcm04.vstorage.vngcloud.vn/demobucket`](https://hcm04.vstorage.vngcloud.vn/demobucket)
  *   Or Curl via command:

      ```bash
      curl --location --head 'https://hcm04.vstorage.vngcloud.vn/demobucket' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041336Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=425119560f45bd0cd7a5a58f6835d189e0cc3d7907cdd72bfd84bd6d88f59ae9'
      ```

<figure><img src="../../../.gitbook/assets/image (29) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **2. Access Control APIs** <a href="#id-2.-api-kiem-soat-truy-cap-access-control-apis" id="id-2.-api-kiem-soat-truy-cap-access-control-apis"></a>

Manage access rights for buckets and objects.

* **GET Bucket ACL** : Get the bucket's access control list (ACL).
  * Path:`GET /<bucket-name>?acl`
  * For example:`GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket?acl`](https://hcm04.vstorage.vngcloud.vn/demobucket?acl)
  *   Or Curl via command:

      ```bash
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket?acl=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041447Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=fd112a35fed96929de946f9c48d050c8f15ca1249ae549d7b86664adde8d81cd'
      ```

<figure><img src="../../../.gitbook/assets/image (30) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **PUT Bucket ACL** : Set ACL for bucket.
  * Path:`PUT /<bucket-name>?acl`
  * For example:`PUT` [`https://hcm04.vstorage.vngcloud.vn/demobucket?acl`](https://hcm04.vstorage.vngcloud.vn/demobucket?acl)
  *   Or Curl via command:

      ```bash
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

<figure><img src="../../../.gitbook/assets/image (31) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **GET Object ACL** : Get the ACL of an object.
  * Path:`GET /<bucket-name>/<object-key>?acl`
  * For example:`GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket/videoplayback.mp4?acl`](https://hcm04.vstorage.vngcloud.vn/demobucket/videoplayback.mp4?acl)
  *   Or Curl via command:

      ```bash
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket/videoplayback.mp4?acl=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041603Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=eb53bff6d55ade68e688ea5af5b44ff9da9afb7b361e5e60563f6d0f3e4c763b'
      ```

<figure><img src="../../../.gitbook/assets/image (32) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **PUT Bucket Make Public:** Set up a Public Bucket
  * Path:`GET /<bucket-name>/?publicAccessBlock`
  * For example:`PUT` [`https://hcm04.vstorage.vngcloud.vn/demobucket01/?publicAccessBlock`](https://hcm04.vstorage.vngcloud.vn/demobucket01/?publicAccessBlock)
  *   Or Curl via command:

      ```bash
      curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket01/?publicAccessBlock=null' \
      --header 'Content-Type: application/xml' \
      --header 'X-Amz-Content-Sha256: beaead3198f7da1e70d03ab969765e0821b24fc913697e929e726aeaebf0eba3' \
      --header 'X-Amz-Date: 20240829T063152Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=9c9624d2ac082b98e6925444ab497746/20240829/HCM04/s3/aws4_request, SignedHeaders=content-length;content-type;host;x-amz-content-sha256;x-amz-date, Signature=341d2a2ba5e1645ae7ee1b9d5e06649333b08433c7efcd47953ac3e2603ee0bb' \
      --data '<PublicAccessBlockConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
        <BlockPublicAcls>true</BlockPublicAcls>
        <IgnorePublicAcls>true</IgnorePublicAcls>
        <BlockPublicPolicy>true</BlockPublicPolicy>
        <RestrictPublicBuckets>true</RestrictPublicBuckets>
      </PublicAccessBlockConfiguration>'
      ```

<figure><img src="../../../.gitbook/assets/image (33) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **GET Bucket Make Public:** Get public or private bucket information.
  * Path:`GET /<bucket-name>/?publicAccessBlock`
  * For example:`GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket01/?publicAccessBlock`](https://hcm04.vstorage.vngcloud.vn/demobucket01/?publicAccessBlock)
  *   Or Curl via command:

      ```bash
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket01/?publicAccessBlock=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T063914Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=9c9624d2ac082b98e6925444ab497746/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=041a0737e3e204ca2941069a3bab021ad54a8eb837fcbfd2ff8d2a3dd647d060'
      ```

<figure><img src="../../../.gitbook/assets/image (34) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **3. Versioning API** <a href="#id-3.-api-quan-ly-phien-ban-versioning" id="id-3.-api-quan-ly-phien-ban-versioning"></a>

Manage versions of objects in buckets.

* **PUT Bucket Versioning** : Enable or disable versioning for the bucket.
  * Path:`PUT /<bucket-name>?versioning`
  * For example:`PUT`[`https://hcm04.vstorage.vngcloud.vn/demobucket?versioning`](https://hcm04.vstorage.vngcloud.vn/demobucket?versioning)
  *   Or Curl via command:

      ```bash
      curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket?versioning=null' \
      --header 'Content-Type: application/xml' \
      --header 'X-Amz-Content-Sha256: beaead3198f7da1e70d03ab969765e0821b24fc913697e929e726aeaebf0eba3' \
      --header 'X-Amz-Date: 20240829T041647Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=content-length;content-type;host;x-amz-content-sha256;x-amz-date, Signature=79d17ba3ab6fe55a68df54b423fa17c9633ed24b462ab4727f9997bef28ed3ac' \
      --data '<VersioningConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
         <Status>Enabled</Status>
      </VersioningConfiguration>'
      ```

<figure><img src="../../../.gitbook/assets/image (35) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **GET Bucket Versioning** : Check the bucket versioning status.
  * Path:`GET /<bucket-name>?versioning`
  * For example:`GET` [`https://hcm04.vstorage.vngcloud.vn/demobucket?versioning`](https://hcm04.vstorage.vngcloud.vn/demobucket?versioning)
  *   Or Curl via command:

      ```bash
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket?versioning=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041708Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=b45886dbf42a0a6d613a465e38e33f6e59b548c27f361798ea168335fe8243e3'
      ```

<figure><img src="../../../.gitbook/assets/image (36) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **GET Object Versions** : List versions of objects in the bucket.
  * Path:`GET /<bucket-name>?versions`
  * For example: `GET` [`https://hcm04.vstorage.vngcloud.vn/demobucket/?versions`](https://hcm04.vstorage.vngcloud.vn/demobucket/?versions)
  *   Or Curl via command:

      ```bash
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket/?versions=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T041846Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=1b4454bcc74c22d919121588f4c26ccc921b69544510ae65de3fdb1c5c9ac274'
      ```

<figure><img src="../../../.gitbook/assets/image (37) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **4. API Lifecycle** <a href="#id-4.-api-lifecycle" id="id-4.-api-lifecycle"></a>

Lifecycle management for buckets and objects:

* **PUT Bucket Lifecycle** : Initializes lifecycle expiration for a bucket.
  * Path:`PUT /<bucket-name>?lifecycle`
  * For example: `PUT`[`https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle`](https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle)
  *   Or Curl via command:

      ```bash
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

<figure><img src="../../../.gitbook/assets/image (38) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **GET Bucket Lifecycle** : Get bucket lifecycle rule information.
  * Path:`GET /<bucket-name>?lifecycle`
  * For example: `GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle`](https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle)
  *   Or Curl via command:

      ```bash
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042134Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=31f4e56f55429f271348de461934dc4c495856330d333559fa6e9ae983800fbd'
      ```

<figure><img src="../../../.gitbook/assets/image (335).png" alt=""><figcaption></figcaption></figure>

* **DELETE Bucket Lifecycle** : Deletes the lifecycle rules set for the bucket.
  * Path:`DELETE /<bucket-name>?lifecycle`
  * For example:`DELETE`[`https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle`](https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle)
  *   Or Curl via command:

      ```bash
      curl --location --request DELETE 'https://hcm04.vstorage.vngcloud.vn/demobucket?lifecycle=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042209Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=c4ab9fbfa8ca73af115142e0a78103e0292e87af6b70a214f21fe020535c3db0'
      ```

<figure><img src="../../../.gitbook/assets/image (336).png" alt=""><figcaption></figcaption></figure>

### **5. CORS API** <a href="#id-5.-api-cors" id="id-5.-api-cors"></a>

Manage access and use S3 as a static website hosting service.

* **PUT Bucket Website** : Set up the bucket as a static website.
  * Path:`PUT /<bucket-name>?cors`
  * For example: `PUT`[`https://hcm04.vstorage.vngcloud.vn/demobucket?cors`](https://hcm04.vstorage.vngcloud.vn/demobucket?cors)
  *   Or Curl via command:

      ```bash
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

<figure><img src="../../../.gitbook/assets/image (337).png" alt=""><figcaption></figcaption></figure>

* **GET Bucket Website** : Get the bucket's website configuration.
  * Path:`GET /<bucket-name>?cors`
  * For example:`GET`[`https://hcm04.vstorage.vngcloud.vn/demobucket?cors`](https://hcm04.vstorage.vngcloud.vn/demobucket?cors)
  *   Or Curl via command:

      ```bash
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket?cors=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042406Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=7632d687924e286195d06f4024d2307c91ccb6df49f6da27328acdd63da63458'
      ```

<figure><img src="../../../.gitbook/assets/image (338).png" alt=""><figcaption></figcaption></figure>

* **DELETE Bucket Website** : Deletes the bucket's website configuration.
  * Path:`DELETE /<bucket-name>?website`
  * For example:`DELETE`[`https://hcm04.vstorage.vngcloud.vn/demobucket?cors`](https://hcm04.vstorage.vngcloud.vn/demobucket?cors)
  *   Or Curl via command:

      ```bash
      curl --location --request DELETE 'https://hcm04.vstorage.vngcloud.vn/demobucket?cors=null' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042453Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=78fdf2ff9a9ec36927431dc1f42a8d5fdcb8fd4a1a2c48794cd45c555de3d6b9'
      ```

<figure><img src="../../../.gitbook/assets/image (339).png" alt=""><figcaption></figcaption></figure>

***

### **6. API Object Locked** <a href="#id-6.-api-object-locked" id="id-6.-api-object-locked"></a>

{% hint style="info" %}
**Attention:**

* To set Object Locked for a bucket, when initializing the bucket, you need to add the parameter **x-amz-bucket-object-lock-enabled = true**
{% endhint %}

Set Object Locked via API.

*   **Update Object Locked Configuration:** Used to upload objects into a bucket.

    * Path:`PUT /<bucket-name>?object-lock`
    * For example:`PUT` [`https://hcm04.vstorage.vngcloud.vn/demoobjectlocked?object-lock`](https://hcm04.vstorage.vngcloud.vn/demoobjectlocked?object-lock)
    *   Or Curl created via command:

        ```bash
        curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demoobjectlocked?object-lock=null' \
        --header 'Content-MD5: frQ6AD8WUb/ZlO+2+AKIlw==' \
        --header 'X-Amz-Content-Sha256: beaead3198f7da1e70d03ab969765e0821b24fc913697e929e726aeaebf0eba3' \
        --header 'X-Amz-Date: 20240829T085503Z' \
        --header 'Authorization: AWS4-HMAC-SHA256 Credential=c65bce455f431914fe5f39c28e8d56f7/20240829/HCM04/s3/aws4_request, SignedHeaders=content-length;content-md5;content-type;host;x-amz-content-sha256;x-amz-date, Signature=f39c72fe719ac44ea493df3013534510ea44d5f75360186532b514fe38139a8c' \
        --data '<ObjectLockConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/"> 
            <ObjectLockEnabled>Enabled</ObjectLockEnabled>
            <Rule>
                <DefaultRetention> 
                    <Mode>COMPLIANCE</Mode>
                    <Days>1</Days>
                </DefaultRetention>
            </Rule>
        </ObjectLockConfiguration>'
        ```

    <figure><img src="../../../.gitbook/assets/image (340).png" alt=""><figcaption></figcaption></figure>

***

## Working with Objects <a href="#lam-viec-voi-object" id="lam-viec-voi-object"></a>

These are the basic APIs for manipulating objects (files) in S3.

* **PUT Object** : Used to upload objects into a bucket.
  * Path:`PUT /<bucket-name>/<object-key>`
  * For example:`PUT`[`https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt`](https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt)
  *   Or Curl via command:

      ```bash
      curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt' \
      --header 'Content-MD5: h6xLdLBQrPaV94Ve6q8WPQ==' \
      --header 'Content-Type: text/plain' \
      --header 'X-Amz-Content-Sha256: beaead3198f7da1e70d03ab969765e0821b24fc913697e929e726aeaebf0eba3' \
      --header 'X-Amz-Date: 20240829T042534Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=content-length;content-md5;content-type;host;x-amz-content-sha256;x-amz-date, Signature=f0592a78ee6b84a5b7cbc4edaf90e76cacc496a0351c5d10b19b9a574e4e9a1a' \
      --data 'datatest'
      ```

<figure><img src="../../../.gitbook/assets/image (341).png" alt=""><figcaption></figcaption></figure>

* **GET Object** : Get an object from S3.
  * Path:`GET /<bucket-name>/<object-key>`
  * For example:`GET` [`https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt`](https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt)
  *   Or Curl via command:

      ```bash
      curl --location 'https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042558Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=5d1d085388c0464652e30d68b894e4ff1a6ade86c8f04eed4f9fba7c5968676d'
      ```

<figure><img src="../../../.gitbook/assets/image (342).png" alt=""><figcaption></figcaption></figure>

* **DELETE Object** : Delete an object from S3.
  * Path:`DELETE /<bucket-name>/<object-key>`
  * For example:`DELETE` [`https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt`](https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt)
  *   Or Curl via command:

      ```bash
      curl --location --request DELETE 'https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt' \
      --header 'x-amz-bypass-governance-retention: true' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042811Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-bypass-governance-retention;x-amz-content-sha256;x-amz-date, Signature=54babdc95afd251946a37352d569f825cc5bce8c7b900c0c03874fb3554fdf6c'
      ```

<figure><img src="../../../.gitbook/assets/image (343).png" alt=""><figcaption></figcaption></figure>

**Attention:**

* To delete a version object, you need to add the versionId param to this API. For example, to delete the test.txt object with version-id = "z3-o0S5HEC6-XsjEjuHoRwoE-F6X1IF", you can curl the following command:

```bash
curl --location --request DELETE 'https://hcm04.vstorage.vngcloud.vn/demobucket/test.txt?versionId=z3-o0S5HEC6-XsjEjuHoRwoE-F6X1IF' \
--header 'x-amz-bypass-governance-retention: true' \
--header 'versionId: z3-o0S5HEC6-XsjEjuHoRwoE-F6X1IF' \
--header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
--header 'X-Amz-Date: 20240911T065412Z' \
--header 'Authorization: AWS4-HMAC-SHA256 Credential=b98adf996bb003a1bd79748c5e779ccd/20240911/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-bypass-governance-retention;x-amz-content-sha256;x-amz-date, Signature=6a69759b132a6be8f609fb66bca41f06a33e560ca4ff012de01351cc7bcbd05e'
```

* **HEAD Object** : Query object metadata without downloading content.
  * Path:`HEAD /<bucket-name>/<object-key>`
  * For example:`HEAD`[`https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt`](https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt)
  *   Or Curl via command:

      ```bash
      curl --location --head 'https://hcm04.vstorage.vngcloud.vn/demobucket/demoobject.txt' \
      --header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
      --header 'X-Amz-Date: 20240829T042639Z' \
      --header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-date, Signature=0fe5fc5caca290919c3782c74f793c0f7cfe36f4f2c7829de8b895bab51ac7d1'
      ```

<figure><img src="../../../.gitbook/assets/image (344) (1).png" alt=""><figcaption></figcaption></figure>

* **COPY Object** : Copy an object from one S3 location to another.
  * Request: `PUT /<destination-bucket>/<destination-object-key>`with header `x-amz-copy-source`.
  * For example:`PUT` [`https://hcm04.vstorage.vngcloud.vn/demobucket01/demoobject.txt`](https://hcm04.vstorage.vngcloud.vn/demobucket01/demoobject.txt)
  * Or Curl via command:

```bash
curl --location --request PUT 'https://hcm04.vstorage.vngcloud.vn/demobucket01/demoobject.txt' \
--header 'x-amz-copy-source: /demobucket/demoobject.txt' \
--header 'x-amz-object-lock-legal-hold: OFF' \
--header 'X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' \
--header 'X-Amz-Date: 20240829T040428Z' \
--header 'Authorization: AWS4-HMAC-SHA256 Credential=f8502b7bf7ca4773c68899d9efd85474/20240829/HCM04/s3/aws4_request, SignedHeaders=host;x-amz-content-sha256;x-amz-copy-source;x-amz-date;x-amz-object-lock-legal-hold, Signature=bf53eedc8b407de21d94c73191940f2257a6c9759f411e844c912de3c2b26ee9'
```

<figure><img src="../../../.gitbook/assets/image (346).png" alt=""><figcaption></figcaption></figure>
