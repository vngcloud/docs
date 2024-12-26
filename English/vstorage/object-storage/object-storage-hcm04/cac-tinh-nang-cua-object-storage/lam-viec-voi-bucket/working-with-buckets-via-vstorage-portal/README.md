# Working with buckets via vStorage Portal

Below are the basic features when you work with buckets

## Create a bucket <a href="#khoi-tao-bucket" id="khoi-tao-bucket"></a>

Before you can store data in vStorage, you must create a Bucket. In vStorage, a Bucket is an Object.

To initiate a project, please follow the steps below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) . Select **the project** you want to create **a bucket for.**
2. Select **Create a bucket** .
3. Enter **Bucket name** according to our rules.
4. Select **Enable Object Locked if you want to use Object locked** feature for this bucket.

{% hint style="info" %}
**Attention:**

* To use the **Object locked** feature for a bucket on vStorage, when initializing the bucket, you must select **Enable Object Locked** .
* When you select **Enable Object Locked** , we will automatically enable **Object versioning** for your bucket.
{% endhint %}

<figure><img src="../../../../../../.gitbook/assets/image (27) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## View bucket information <a href="#xem-thong-tin-bucket" id="xem-thong-tin-bucket"></a>

After creating a bucket and uploading objects to that bucket. You can view bucket details and use the features we provide for the bucket including: ACLs, Lifecycle, CORS,...

To view detailed information about a bucket, you can:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .

2\. Select **the project** containing **the bucket** you want to view details for.

3\. Select **the bucket** you want to view details for and select **View detail** .

**4. On the bucket** details page , you can view and use the features we provide for the bucket including:

* **General information** : Provides general information of the bucket such as Name, Owner, Created date, Versioning, Encryption, Object Lock.
* **ACLs** : Provides Read/Write/Read+Write access management information for one or more Root accounts currently on the system that are granted access to the bucket. For details on how to use the feature, see Using [ACLs](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/object-storage-hcm04/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-acls) .
* **CORS** : Provides information about the paths that are allowed to access the bucket's resources. For details on how to use the feature, see Using [CORS.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/object-storage-hcm04/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-cors)
* **Lifecycle** : Provides information about the lifecycles set up for the bucket. For details on how to use the feature, see [Using the lifecycle feature.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/object-storage-hcm04/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-lifecycle)
* **Event notification** : Provides information about event notifications set up for the bucket. For details on how to use this feature, see [Using the Event notification feature.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/object-storage-hcm04/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-event-notification)

<figure><img src="../../../../../../.gitbook/assets/image (28) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Bucket encryption <a href="#su-dung-tinh-nang-bucket-encryption" id="su-dung-tinh-nang-bucket-encryption"></a>

**SSE-S3 (Server-Side Encryption with S3 Managed Keys)** is a server-side data encryption feature provided by Amazon S3. With SSE-S3, your data is automatically encrypted when it is uploaded to S3 and automatically decrypted when you download it.

To use Bucket encryption, please follow the steps below:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .

2\. Select **the project** containing **the bucket** you want to set encryption for.

**3. Select the Action** icon and select **Configure encryption**

<figure><img src="../../../../../../.gitbook/assets/image (29) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

4\. On the SSE-S3 encryption usage confirmation page, please select **Enable ecryption.**

<figure><img src="../../../../../../.gitbook/assets/image (30) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Delete bucket <a href="#xoa-bucket" id="xoa-bucket"></a>

To delete a bucket, please follow the steps below:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .

2\. Select **the project** and select **the bucket** you want to delete.

**3. Select the Action** icon and select **Delete**

<figure><img src="../../../../../../.gitbook/assets/image (31) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

After selecting Delete, the system will automatically switch to the main screen. If you see the bucket you just performed disappears from the list, you have successfully deleted it. The bucket has now been permanently deleted from the system and you cannot restore the bucket as well as the objects stored in the bucket. So make sure to check your data before performing this operation.
