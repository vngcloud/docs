# Working with S3 Keys

## **Overview** <a href="#tong-quan" id="tong-quan"></a>

On the vStorage system, S3 key is a key pair including access key and secret key integrated by vStorage and compatible with S3 client tools such as s3cmd, s3 SDK,...

***

## Root User Account creates a S3 keys <a href="#root-user-account-khoi-tao-s3-keys" id="root-user-account-khoi-tao-s3-keys"></a>

To initialize an S3 key, follow the instructions below:

1. Log in to [https://vstorage.console.vngcloud.vn with ](https://vstorage.console.vngcloud.vn/storage/list)<mark style="background-color:orange;">Root User Account</mark> .
2. Select **Region HAN02.**
3. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FzBejUW7ARqXZMMLNJPI2%252Fimage.png%3Falt%3Dmedia%26token%3D67d600f9-d645-434f-b403-be01af3603e0\&width=37\&dpr=4\&quality=100\&sign=46e8d333\&sv=2)in the project you just created and then select **Identity and Access Management.**
4. Under **List of S3 keys of this project** , select **Generate S3 key** .
5. Select **Copy** or **Download** to download the Access Key/Secret Key information you just generated.

<figure><img src="../../../../.gitbook/assets/image (566).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (567).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (568).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* After clicking to create S3 key, you need to **save the Access Key/Secret Key pair** for use. If you do not save it now, you will not be able to get the Secret Key of this Access Key later.
* <mark style="background-color:orange;">The S3 key initialized by</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">**the Root User Account**</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">will have full access/operation rights on the buckets of this project.</mark>
{% endhint %}

***

## IAM User Account creates a S3 keys <a href="#iam-user-account-khoi-tao-s3-keys" id="iam-user-account-khoi-tao-s3-keys"></a>

To initialize an S3 key, follow the instructions below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) with your <mark style="background-color:orange;">IAM User Account</mark> .
2. Select **Region HAN02.**
3. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FzBejUW7ARqXZMMLNJPI2%252Fimage.png%3Falt%3Dmedia%26token%3D67d600f9-d645-434f-b403-be01af3603e0\&width=37\&dpr=4\&quality=100\&sign=46e8d333\&sv=2)in the project you just created and then select **Identity and Access Management.**
4. Under **List of S3 keys of this project** , select **Generate S3 key** .
5. Select **Copy** or **Download** to download the Access Key/Secret Key information you just generated.

<figure><img src="../../../../.gitbook/assets/image (569).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* After clicking to create S3 key, you need to **save the Access Key/Secret Key pair** for use. If you do not save it now, you will not be able to get the Secret Key of this Access Key later.
* <mark style="background-color:orange;">S3 keys created by</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">**IAM User Account**</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">will have full access/operation rights on buckets/objects according to the permissions of that IAM User Account. For example, if your IAM User Account only has Read Object permission, then S3 keys created by this IAM User Account will also only have Read Object permission.</mark>
{% endhint %}

***

## Work with the S3 API (or 3rd party software) via S3 keys <a href="#thuc-hien-lam-viec-voi-s3-api-hoac-3rd-party-software-thong-qua-s3-keys" id="thuc-hien-lam-viec-voi-s3-api-hoac-3rd-party-software-thong-qua-s3-keys"></a>

### Connect 3rd party softwares to vStorage <a href="#ket-noi-3rd-party-softwares-voi-vstorage" id="ket-noi-3rd-party-softwares-voi-vstorage"></a>

After you have successfully initialized the project and initialized the S3 key, you can now use 3rd party softwares to connect and work with your project. The 3rd party softwares you can choose to use can be S3cmd, Cyberduck, Rclone, S3 Browser, MinIO Client,... In this document, we will guide you to connect S3 Browser with vStorage. S3 Browser is an optimized tool that allows you to share and upload your files. This tool has a relatively simple interface, is easy to use and is compatible with the API of the vStorage storage service.

To integrate the S3 Browser tool with vStorage, you can follow the instructions below:

1. Download the S3 Browser user tool here [https://s3browser.com/download.aspx](https://s3browser.com/download.aspx) .
2. Open the S3 Browser app **.** Select the Account folder, **then select Add new account**

<figure><img src="../../../../.gitbook/assets/image (530).png" alt="" width="295"><figcaption></figcaption></figure>



3. The Add New Account screen appears, now you enter the following information:
   * **Display name:** Display name of the account. Example: Demo\_HAN02
   * **Account type** : Select **S3 Compatible Storage.**
   * **REST Endpoint** : Path to vstorage, for Region HAN02 the path is [han02.vstorage.vngcloud.vn](http://han02.vstorage.vngcloud.vn/)
   * **Access Key ID & Secret Access Key:** This is the S3 key pair you generated in step 2 earlier.
4. Select the **Use Secure transfer (SSL/TLS)** option because vStorage only supports encrypted transmission channels (HTTPS, port 443) to ensure data security, vStorage currently does not support unencrypted transmission channels (HTTP, port 80).
5. Select **Add new account.**

<figure><img src="../../../../.gitbook/assets/image (531).png" alt="" width="375"><figcaption></figcaption></figure>

6. When the connection is successful, the S3 Browser screen will display as follows:

<figure><img src="../../../../.gitbook/assets/image (532).png" alt=""><figcaption></figcaption></figure>



***

## Delete S3 keys <a href="#xoa-s3-keys" id="xoa-s3-keys"></a>

To cancel (delete) one or more previously created S3 keys, follow the instructions below:

1. Log in to [https://vstorage.console.vngcloud.vn with ](https://vstorage.console.vngcloud.vn/storage/list)Root User Account or IAM User Account .
2. Chọn **Region HAN02.**
3. Select the icon  <img src="../../../../.gitbook/assets/image (526).png" alt="" data-size="line"> in the project you just created and then select **Identity and Access Management.**
4. In List **of S3 keys of this project** , select **the S3 key** you want to delete and then select **Delete.**

Once the S3 key is successfully cancelled, you will no longer be able to use this S3 key to access vStorage. Be careful when cancelling (deleting) an S3 account as you will not be able to recover this deleted account.

<figure><img src="../../../../.gitbook/assets/image (570).png" alt=""><figcaption></figcaption></figure>

