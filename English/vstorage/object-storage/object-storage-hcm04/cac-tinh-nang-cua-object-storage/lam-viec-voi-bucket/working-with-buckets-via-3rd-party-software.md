# Working with buckets via 3rd party software

## Overview <a href="#tong-quan" id="tong-quan"></a>

Bucket is a data bucket (Object) in vStorage, which can be understood as a folder in the operating system. You can manage files and folders using 3rd party softwares that are compatible with S3. The 3rd party softwares you can choose to use are S3cmd, Cyberduck, Rclone, S3 Browser, MinIO Client,... In this document, we will guide you to connect S3 Browser to vStorage and use S3 Browser to work with buckets. S3 Browser is an optimized tool that allows you to share and upload your files. This tool has a relatively simple interface, is easy to use and is compatible with the API of the vStorage storage service.

After you have successfully initialized the project and initialized the S3 key, you can now use 3rd party softwares to connect and work with your project. The 3rd party softwares you can choose to use can be S3cmd, Cyberduck, Rclone, S3 Browser, MinIO Client,... In the scope of this document, we will guide you to connect S3 Browser with vStorage. S3 Browser is an optimized tool that allows you to share and upload your files. This tool has a relatively simple interface, is easy to use and is compatible with the API of the vStorage storage service.

## Integrate S3 Browser with vStorage <a href="#tich-hop-s3-browser-voi-vstorage" id="tich-hop-s3-browser-voi-vstorage"></a>

To integrate the S3 Browser tool with vStorage, you can follow the instructions below:

1. Download the S3 Browser user tool here [https://s3browser.com/download.aspx](https://s3browser.com/download.aspx) .
2. Open the S3 Browser app **.** Select the Account folder **, then select Add new account**

<figure><img src="../../../../../.gitbook/assets/image (8) (1) (1) (1) (1) (1).png" alt="" width="443"><figcaption></figcaption></figure>

3. The Add New Account screen appears, now you enter the following information:

* **Display name:** Display name of the account. Example: Demo\_HCM04
* **Account type** : Select **S3 Compatible Storage.**
* **REST Endpoint** : Path to vstorage, for Region HCM04 the path is [hcm04.vstorage.vngcloud.vn](http://hcm01.vstorage.vngcloud.vn/)
* **Access Key ID & Secret Access Key:** This is the S3 key pair you generated in step 2 earlier.

4. Select the **Use Secure transfer (SSL/TLS)** option because vStorage only supports encrypted transmission channels (HTTPS, port 443) to ensure data security, vStorage currently does not support unencrypted transmission channels (HTTP, port 80).
5. Select **Add new account.**

<figure><img src="../../../../../.gitbook/assets/image (9) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

6. When the connection is successful, the S3 Browser screen will display as follows:

<figure><img src="../../../../../.gitbook/assets/image (10) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Using features on S3 Browser

## Basic use cases <a href="#cac-usecase-co-ban" id="cac-usecase-co-ban"></a>

Below are instructions for some common use cases you can perform on S3 Browser:

### **Create / Delete bucket** <a href="#tao-xoa-bucket" id="tao-xoa-bucket"></a>

* Create and delete a bucket by selecting the **New bucket** button . Now enter **the Bucket name** and select **Create new bucket.**

### **Upload / Download file** <a href="#upload-download-file" id="upload-download-file"></a>

* After creating a bucket, select the bucket you want to upload/download files to. Next, select **Upload/Download** depending on your upload/download needs.

### **Create / Delete Folder** <a href="#tao-xoa-folder" id="tao-xoa-folder"></a>

* You can also create/delete folders by selecting **New Folder** or **Delete** .

<figure><img src="../../../../../.gitbook/assets/image (11) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Advanced use cases <a href="#cac-usecase-nang-cao" id="cac-usecase-nang-cao"></a>

Here are instructions for advanced features you can do on S3 Browser:

### **ACL** <a href="#acl" id="acl"></a>

**ACLs** are a feature on S3 that allows you to control access permissions for each object in your S3 bucket. They define which users or groups of users can access the object and what actions they can perform, such as downloading, uploading, deleting, or overwriting the object.

To set up ACL for a bucket using S3 Browser, right-click on the bucket, then select Edit Permission (ACL). In the permission section, check the permissions you want to grant to the user. For more details, see [https://s3browser.com/share-s3-bucket-edit-acls.aspx](https://s3browser.com/share-s3-bucket-edit-acls.aspx)

<figure><img src="../../../../../.gitbook/assets/image (22) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **SSE-S3** <a href="#sse-s3" id="sse-s3"></a>

SSE-S3 (Server-Side Encryption with S3 Managed Keys) is a server-side data encryption feature provided by Amazon S3. With SSE-S3, your data is automatically encrypted when uploaded to S3 and automatically decrypted when you download it. **To implement this feature on S3 Browser, you need to use S3 Browser Pro version. If your application does not currently support the implementation of the feature, please submit a request to use the feature via a ticket to VNGCloud.** For more details, please visit [https://s3browser.com/amazon-s3-server-side-encryption.aspx](https://s3browser.com/amazon-s3-server-side-encryption.aspx)

### **SSE-C** <a href="#sse-c" id="sse-c"></a>

**SSE-C** (Server-Side Encryption with Customer-Provided Keys) is a server-side data encryption feature provided by Amazon S3. Like SSE-S3, SSE-C encrypts your data automatically when it is uploaded to S3 and decrypts it automatically when you download it. However, with SSE-C, you provide and manage your own encryption keys, instead of using keys managed by AWS. **To implement this feature on S3 Browser, you need to use S3 Browser Pro. If your application does not currently support the implementation of the feature, please submit a request to use the feature via a ticket to VNGCloud.** For more details, please visit [https://s3browser.com/amazon-s3-server-side-encryption.aspx](https://s3browser.com/amazon-s3-server-side-encryption.aspx)

### **Object Locked** <a href="#object-locked" id="object-locked"></a>

**Object Lock** is a feature that protects your data from being deleted or overwritten for a fixed period of time or indefinitely. It uses the **WORM** (Write Once, Read Many) model, which means that once an object is uploaded to S3 and locked, it cannot be deleted or changed by anyone, including the root user.

To set up Object Locked for a bucket using S3 Browser, when creating a new bucket, you need to select the **Enable S3 Objected Lock option.**

<figure><img src="../../../../../.gitbook/assets/image (21) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Next, when the bucket is successfully created, right-click on the bucket, then select **Object Locked** . You can set the object locked in both **Retention** and **Legal Hold** modes through S3 Browser. For more details, please visit [https://s3browser.com/amazon-s3-object-lock.aspx](https://s3browser.com/amazon-s3-object-lock.aspx)

<figure><img src="../../../../../.gitbook/assets/image (20) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **Versioning** <a href="#versioning" id="versioning"></a>

Versioning is a feature that supports storing multiple past versions of objects stored in a bucket. You can use versioning to save, retrieve, and restore any version of an object stored in your bucket. When versioning is enabled, when uploading/deleting an object, instead of deleting the object from the system, we will move the deleted or overwritten objects to the versioning version. From there, you can easily restore mistakenly deleted objects or download old versions of data when needed.

To set up Versioning for a bucket using S3 Browser, right-click on the bucket, then select **Edit Versioning Settings** . For more details, see [https://s3browser.com/amazon-s3-versioning.aspx](https://s3browser.com/amazon-s3-versioning.aspx)

<figure><img src="../../../../../.gitbook/assets/image (19) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **Lifecycle rotation** <a href="#lifecycle-rotation" id="lifecycle-rotation"></a>

**Lifecycle rotation** is a feature that manages the lifecycle of objects in a bucket. This feature allows you to automate actions such as deleting objects after a certain period of time.

To set up Lifecycle rotation for a bucket using S3 Browser, right-click on the bucket, then select **Lifecycle Configuration** . For more details, see [https://s3browser.com/bucket-lifecycle-configuration.aspx](https://s3browser.com/bucket-lifecycle-configuration.aspx)

<figure><img src="../../../../../.gitbook/assets/image (18) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **Lifecycle transit** <a href="#lifecycle-transit" id="lifecycle-transit"></a>

Currently on region HCM04 we only support you to create Project with Storage Class **Instant Archive Type** . Because there is only 1 storage class, currently the Lifecycle transit feature will not work.

### **CORS** <a href="#cors" id="cors"></a>

CORS (Cross-Origin Resource Sharing) is a security mechanism that allows websites hosted on one domain to access resources from another domain. When you use S3 to host static content and want to access that content from a website hosted on another domain, you need to configure CORS for your S3 bucket.

To set up CORS for a bucket using S3 Browser, right-click on the bucket, then select **CORS Configuration** . For more details, see [https://s3browser.com/s3-bucket-cors-configuration.aspx](https://s3browser.com/s3-bucket-cors-configuration.aspx)

<figure><img src="../../../../../.gitbook/assets/image (17) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **Public/ Private bucket** <a href="#public-private-bucket" id="public-private-bucket"></a>

**Public buckets** are a feature that allows users to share buckets publicly in the cloud. Users from outside the internet can access the bucket through a URL without having to authenticate access to the system. Public access poses a security risk, so if your scenario does not require such access, we recommend that you do not enable public access to the bucket. At any point, if you no longer want the bucket to be public, you can make the bucket private.

To set a bucket to public using S3 Browser, right-click on the bucket, then select **Public Access block Configuration** . For more details, see [https://s3browser.com/amazon-s3-public-access-block-configuration.aspx](https://s3browser.com/amazon-s3-public-access-block-configuration.aspx)

<figure><img src="../../../../../.gitbook/assets/image (16) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **Bucket policy** <a href="#bucket-policy" id="bucket-policy"></a>

**A Bucket Policy** is a type of access policy used to control access to a specific S3 bucket. It allows you to define which users or groups can access the bucket and what operations they can perform, such as uploading, downloading, deleting, or listing objects in the bucket.

To set up a bucket policy using S3 Browser, right-click on the bucket, then select **Edit Bucket Policy** . For more details, see [https://s3browser.com/working-with-amazon-s3-bucket-policies.aspx?v=11.7.5\&fam=x64#amazon-s3-bucket-policies-examples](https://s3browser.com/working-with-amazon-s3-bucket-policies.aspx?v=11.7.5\&fam=x64#amazon-s3-bucket-policies-examples)

<figure><img src="../../../../../.gitbook/assets/image (334).png" alt=""><figcaption></figcaption></figure>
