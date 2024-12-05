# Bucket Lifecycle

## **Overview** <a href="#tong-quan" id="tong-quan"></a>

**Lifecycle** on vStorage is a feature that helps you manage the lifecycle of objects in your bucket, thereby optimizing storage costs. With Lifecycle, you can configure rules to automatically delete objects when they are no longer needed.

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .

2\. Select **the project** containing **the bucket** you want to set up the lifecycle for.

**3. Select the Action** icon and select **Configure Lifecycle.**

<figure><img src="../../../../../../.gitbook/assets/image (330).png" alt=""><figcaption></figcaption></figure>

**4. The Lifecycle** screen is displayed. Select **Create a lifecycle rule** .

<figure><img src="../../../../../../.gitbook/assets/image (331).png" alt=""><figcaption></figcaption></figure>

5\. Enter **a Rule name** . The Rule names we allow you to enter include letters (az, AZ, 0-9, '\_', '-', space). The length of your **Rule name** must be between 5 and 50.

6\. Select Rule type: currently, we only support 1 type of rule Expiration: Rule that supports deleting objects according to constraints.

7\. Enter **Filter** . This filter is applied to a specific lifecycle rule. **Each lifecycle rule can only have one filter, if you want to apply the lifecycle rule you are creating to all objects in this bucket, leave this field blank.** Or you can filter the objects you want to apply the lifecycle rule to through the prefix.

<figure><img src="../../../../../../.gitbook/assets/image (332).png" alt=""><figcaption></figcaption></figure>

8\. Select the action that happens to the object in the bucket you choose, including:

* **Expire current version of objects** :
  * When enabled, this rule will automatically delete **the current version** of the object after a certain period of time.
  * You can enter a number of days in the "After \_\_\_ days from object creation" section to define the number of days from object creation that the current version will expire and be deleted.
* **Permanently delete noncurrent versions** :
  * This rule applies to **noncurrent versions** of objects if you have Versioning enabled.
  * You can configure to delete old versions after a number of days since they become noncurrent version, by filling in "After \_\_\_ days become noncurrent version".
* **Delete incomplete multipart uploads** :
  * When you upload a large object using a multipart upload, but the upload does not complete, the uploaded parts are retained in S3.
  * This rule allows to automatically delete parts of **multipart uploads that are not completed** after a period of time since the upload was started.
  * You can enter a number of days in the "After \_\_\_ days from object creation" section to specify the period of time before incomplete parts of a multipart upload are deleted.
* **Delete expired object delete marker** :
  * This rule only applies if you have Versioning enabled and have object delete markers in the bucket.
  * When enabled, it will remove expired **delete markers , improving performance by cleaning up markers that are no longer needed. (This option can usually only be enabled when there are expired delete markers in the bucket.)**

<figure><img src="../../../../../../.gitbook/assets/image (333).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* The object processing in a lifecycle rule run depends on **the number of objects** in the bucket that your lifecycle rule is set up in and **the workload** of our system. If the bucket has **many objects** or the system is under high load, the processing will be **slow and spread over the next days** . If the bucket has **few objects** or the system is under low load, the processing will be **fast and can be completed in a day** . To ensure efficient and fast object processing, you should split the lifecycle rule runs into smaller ones and use Filters to reduce the number of objects to be processed.
{% endhint %}
