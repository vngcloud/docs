# Data Security stored on vStorage

Encrypting the content of stored files (objects) is an effective data security solution. By encrypting data at rest, the data is transformed into a form that cannot be read by those without access. This helps protect data from unauthorized access, even if an attacker can access the system's storage gateway.

VNG Cloud currently provides the following mechanisms for encrypting the content of stored files (objects) on the vStorage service:

* **Client-side encryption:** In this mechanism, the user is responsible for managing the key and workload of the encryption process. Data will be encrypted on the user's machine or application layer.
* **Server-side encryption**: VNGCloud provides the feature to encrypt file content (objects) stored on the vStorage service using the encrypt endpoint. When customers upload files through this endpoint, the data is automatically encrypted before being stored. This mechanism provides high security benefits for sensitive data. Specifically, you can use vStorage endpoint with the following parameters:

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><p><strong>Farm</strong></p><p><strong>Farm ID</strong></p><p></p><p><strong>Authentication endpoint</strong></p><p></p><p><strong>vStorage endpoint</strong></p><p></p><p><strong>Mục đích sử dụng</strong></p></td><td></td><td></td></tr><tr><td><p>HCM03</p><p>8b1e9c9b-7123-54a5-ua8f-2d67d71c9212</p><p>https://hcm03.auth.vstorage.vngcloud.vn/v3</p><p>https://hcm03-encrypt-vstorage.vngcloud.vn</p><p>Khi sử dụng encryption endpoint này, dữ liệu của bạn sẽ được tự động mã hóa khi tải tệp tin lên vStorage theo đúng chuẩn mã hóa AES-256.</p></td><td></td><td></td></tr></tbody></table>

{% hint style="info" %}
**Note:**

* When you upload a file through the encryption endpoint, the file is encrypted before being stored on vStorage. Now, to download the file, you can use any vStorage endpoint of the HCM03 farm and the downloaded file will already be decrypted.
* Uploading files through the encryption endpoint will make your files more secure but may reduce upload speeds. Average upload speeds when using encryption endpoints can be reduced by 5% to 10% compared to uploads using conventional endpoints.
{% endhint %}
