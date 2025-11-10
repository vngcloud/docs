# Bucket Lifecycle

## **Overview** <a href="#tong-quan" id="tong-quan"></a>

**Lifecycle** on vStorage is a feature that helps you manage the lifecycle of objects in your bucket, thereby optimizing storage costs. With Lifecycle, you can configure rules in 2 types:

* **Transition rule:** Rules support moving objects between storage classes. You can set up one or more lifecycle rules to move objects if the object has not changed for N days.
* **Expiration rule**: Rules support deleting objects based on constraints. You can set up one or more lifecycle rules to delete objects after a certain period of time since the object exists on the vStorage system.

<figure><img src="../../../../../../.gitbook/assets/image (621).png" alt=""><figcaption></figcaption></figure>

Refer to the table below to understand how each storage class works:

<table data-full-width="true"><thead><tr><th>Item</th><th>Gold Class</th><th>Instant Archive</th><th>Archive</th></tr></thead><tbody><tr><td><strong>Designed for</strong></td><td>For frequently accessed data that requires low latency and high throughput with retrieval in <strong>milliseconds (10m object/ 1H)</strong>.</td><td>For long-term storing data with retrieval in <strong>miliseconds (5m object/ 1H)</strong>.</td><td>For long-term data archiving that is accessed once or twice in a year with retrieval within <strong>hour (5m object/ 12H and 10m object/ 24H).</strong></td></tr><tr><td><strong>Durability</strong></td><td>99.999999999%</td><td>99.999999999%</td><td>99.999999999%</td></tr><tr><td><strong>Availability</strong></td><td>99.99%</td><td>99.99%</td><td>99.99%</td></tr><tr><td><strong>Min storage quota</strong></td><td>No</td><td>No</td><td>5 TB</td></tr><tr><td><strong>Min storage duration</strong></td><td>No</td><td>No</td><td>90 days</td></tr><tr><td><strong>Min billable object size</strong></td><td>0</td><td>0</td><td>128 KB</td></tr><tr><td><strong>Free traffic</strong></td><td>Quota x 10</td><td>Quota x 2</td><td>Quota x1</td></tr><tr><td><strong>Free request</strong></td><td>Free request on Gold Class performance</td><td>Free request on Instant Archive Class performance</td><td>Free request on Archive Class performance</td></tr></tbody></table>

***

## With Transition rule

Follow the instructions below to set up a transition rule:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list), then select Region **HAN02**

2\. Select **the project** containing **the bucket** you want to set up the lifecycle for. For example, I have a bucket `demo-project` that has been initialized to create Storage Class Gold as shown below.

<figure><img src="../../../../../../.gitbook/assets/image (622).png" alt=""><figcaption></figcaption></figure>

3\. Select the **Action** icon and select **Configure Lifecycle.**

<figure><img src="../../../../../../.gitbook/assets/image (623).png" alt=""><figcaption></figcaption></figure>

4\. The **Lifecycle** screen is displayed. Select **Create a lifecycle rule**.

<figure><img src="../../../../../../.gitbook/assets/image (624).png" alt=""><figcaption></figcaption></figure>

5\. Enter **a Rule name** . The Rule names we allow you to enter include letters (az, AZ, 0-9, '\_', '-', space). The length of your **Rule name** must be between 5 and 50.

6\. Select **Rule type**: **Transition**

<figure><img src="../../../../../../.gitbook/assets/image (625).png" alt=""><figcaption></figcaption></figure>

7\. Enter **Filter**. This filter is applied to a specific lifecycle rule. I**f you want to apply the lifecycle rule you are creating to all objects in this bucket, leave this field blank.** Or you can filter the objects you want to apply the lifecycle rule to through the prefix.

8\. Select the action that happens to the object in the bucket you choose, including:

*   **Transition current version of objects:**

    * When enabled, this rule automatically moves the current version of an object from the current storage class to an selected lower storage class a certain period of time.
    * You can enter a number of days in the "**After \_\_\_ days from object creation**" section to define the number of days from object creation that the current version will be moved.

    <figure><img src="../../../../../../.gitbook/assets/image (626).png" alt=""><figcaption></figcaption></figure>

**Transition noncurrent version of objects:**

* This rule applies to **noncurrent versions** of objects if you have Versioning enabled.
* You can configure to move old versions after a number of days since they become noncurrent version, by filling in "**After \_\_\_ days become noncurrent version**".

<figure><img src="../../../../../../.gitbook/assets/image (627).png" alt=""><figcaption></figcaption></figure>

## Với Expiration rule

Expiration rule is a set of rules that automatically delete objects when they expire. Follow the instructions below to set up a expiration rule:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).

2\. Select **the project** containing **the bucket** you want to set up the lifecycle for.

3\. Select the **Action** icon and select **Configure Lifecycle.**

<figure><img src="../../../../../../.gitbook/assets/image (628).png" alt=""><figcaption></figcaption></figure>

4\. The **Lifecycle** screen is displayed. Select **Create a lifecycle rule**.

<figure><img src="../../../../../../.gitbook/assets/image (629).png" alt=""><figcaption></figcaption></figure>

5\. Enter **a Rule name** . The Rule names we allow you to enter include letters (az, AZ, 0-9, '\_', '-', space). The length of your **Rule name** must be between 5 and 50.

6\. Select Rule type: Expiration

7\. Enter **Filter**. This filter is applied to a specific lifecycle rule. I**f you want to apply the lifecycle rule you are creating to all objects in this bucket, leave this field blank.** Or you can filter the objects you want to apply the lifecycle rule to through the prefix.

<figure><img src="../../../../../../.gitbook/assets/image (630).png" alt=""><figcaption></figcaption></figure>

8\. Select the action that happens to the object in the bucket you choose, including:

* **Expire current version of objects**:
  * When enabled, this rule will automatically delete **the current version** of the object after a certain period of time.
  * You can enter a number of days in the "**After \_\_\_ days from object creation**" section to define the number of days from object creation that the current version will expire and be deleted.
* **Permanently delete noncurrent versions**:
  * This rule applies to **noncurrent versions** of objects if you have Versioning enabled.
  * You can configure to delete old versions after a number of days since they become noncurrent version, by filling in "**After \_\_\_ days become noncurrent version**".
* **Delete incomplete multipart uploads**:
  * When you upload a large object using a multipart upload, but the upload does not complete, the uploaded parts are retained in S3.
  * This rule allows to automatically delete parts of **multipart uploads that are not completed** after a period of time since the upload was started.
  * You can enter a number of days in the "After \_\_\_ days from object creation" section to specify the period of time before incomplete parts of a multipart upload are deleted.
* **Delete expired object delete marker**:
  * This rule only applies if you have Versioning enabled and have object delete markers in the bucket.
  * When enabled, it will remove expired **delete markers , improving performance by cleaning up markers that are no longer needed. (This option can usually only be enabled when there are expired delete markers in the bucket.)**

<figure><img src="../../../../../../.gitbook/assets/image (631).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* The object processing in a lifecycle rule run depends on **the number of objects** in the bucket that your lifecycle rule is set up in and **the workload** of our system. If the bucket has **many objects** or the system is under high load, the processing will be **slow and spread over the next days** . If the bucket has **few objects** or the system is under low load, the processing will be **fast and can be completed in a day** . To ensure efficient and fast object processing, you should split the lifecycle rule runs into smaller ones and use Filters to reduce the number of objects to be processed.
* With **Transition rule**: you are only allowed to move data down to a lower storage class, it cannot automatically move back up to a higher class.
{% endhint %}
