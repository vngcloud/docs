# Access Management

## Access account <a href="#tai-khoan-truy-cap" id="tai-khoan-truy-cap"></a>

In region HCM04, you can use 2 types of accounts to access vStorage. Details of these 2 types include:

* **Root user account: Is the** [first initial](https://register.vngcloud.vn/signup) account to access VNG Cloud with full access to all resource services on VNG Cloud.
* **S3 key:** Is a pair of s3 keys with access key and secret key integrated by vStorage for compatibility with S3 client tools such as s3cmd, s3 SDK,...

### Root user account <a href="#root-user-account" id="root-user-account"></a>

#### **Create Root User Account**

To create a Root user account, please register an account at the registration page [https://register.vngcloud.vn/signup](https://register.vngcloud.vn/signup) .

After you create a Root user account, you collect the following information to access and work with resources using the Root user account:

* The email address used to create the Root user account.
* Password for the Root user account.

To log in to vStorage with the Root account, see [Accessing resources using the Root user account](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-truy-cap-tai-nguyen-vstorage/truy-cap-tai-nguyen-su-dung-tai-khoan-nguoi-dung-root) .

***

#### **Cancel Root User Account**

To cancel your Root account, you need to contact us by creating a ticket to request account cancellation. For more details, see [Account Cancellation Instructions](https://docs.vngcloud.vn/vng-cloud-document/v/vn/huong-dan-su-dung-tai-khoan/huong-dan-huy-tai-khoan) .

### S3 key <a href="#s3-key" id="s3-key"></a>

To initialize an S3 key, follow the instructions below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .
2. Select **Region HCM04.**
3. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FzBejUW7ARqXZMMLNJPI2%252Fimage.png%3Falt%3Dmedia%26token%3D67d600f9-d645-434f-b403-be01af3603e0\&width=37\&dpr=4\&quality=100\&sign=46e8d333\&sv=2)in the project you just created and then select the S3 key item.
4. In the S3 key section, select **Generate S3 key** .
5. Select **Copy** or **Download** to download the Access Key/Secret Key information you just generated.

![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FpeK1OHEtz5jcXW5k9c8F%252Fimage.png%3Falt%3Dmedia%26token%3D00782bb7-32ee-47e5-8f6e-a15cfe606155\&width=768\&dpr=4\&quality=100\&sign=c5389514\&sv=2)![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FdQZHbhKQU50qaLir3Vax%252Fimage.png%3Falt%3Dmedia%26token%3D7cf6496e-0c94-4dbf-ab68-584081d619a4\&width=768\&dpr=4\&quality=100\&sign=288ea5d5\&sv=2)

{% hint style="info" %}
**Attention:**

* After clicking create S3 key, you need to **save the Access Key/Secret Key pair** for use. If you do not save it now, you will not be able to get the Secret Key of this Access Key later.
{% endhint %}

## Access Management <a href="#quan-ly-truy-cap" id="quan-ly-truy-cap"></a>

On region HCM04, we provide you with individual access permissions to each bucket or object as described in the diagram below. Details include:

<details>

<summary>ACLs access permissions </summary>

You can grant Read, Write or Read and Write permissions to 1 or all other Root users. (Root users granted access via ACLS must be authorized accounts on our VNG Cloud system). For more information, see Using [ACLs.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/object-storage-hcm04/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-acls)

</details>

<details>

<summary>CORS resource sharing</summary>

You can allow a website to access resources in the bucket. For more information, see [Using CORS.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/object-storage-hcm04/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-cors)

</details>

<details>

<summary>Decentralization via Bucket policy</summary>

You can manage access to your buckets through JSON rules. For more information, see [Using Bucket Policy.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/object-storage-hcm04/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-bucket-policy)

</details>

<details>

<summary>Share object</summary>

You can share an object with another user or share it publicly. For more information, see [Sharing objects.](https://docs.vngcloud.vn/vng-cloud-document/vn/vstorage/object-storage/object-storage-hcm04/cac-tinh-nang-cua-object-storage/lam-viec-voi-object-va-directory)

</details>
