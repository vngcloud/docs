# Object Lock

**Object Lock** is a feature that helps protect your data from being deleted or overwritten for a fixed period of time or indefinitely. This feature uses the **WORM** (Write Once, Read Many) model, which means that once an object is uploaded to S3 and locked, it cannot be deleted or changed by anyone, including the root user. Currently, on region HCM04, we have supported you to set up Object Locked in 2 modes: Compliance, Legal Hold and <mark style="color:red;">**do not support Governance mode**</mark> . If you use 3rd party software to set up Object Locked in this Governance mode, the generated S3 key will have full rights to delete object versions on your bucket. The meanings of the locked modes are described below:

* **Retention mode** : prevents deletion and overwriting of object version for a certain period of time. In Retention period, there will be 2 modes:
  * **Compliance mode (supported)** : any user or admin,… cannot overwrite the locked object version. When the preset time expires, the user can delete or overwrite the object normally.
  * **Governance mode (coming soon)** : only users with special permissions (with ByPassGovernance permission), such as root user or S3 Key without Restriction by IAM enabled, can delete or overwrite objects.
* **Legal Hold:** prevents deletion and overwriting of object version indefinitely until user disables. This mode works independently of Retention period. Users with PutObjectLegalHold permission can add or remove legal hold for object.

**To set up Object Locked for a bucket using S3 Browser, when creating a new bucket, you need to select the Enable S3 Objected Lock** option . <mark style="color:red;">**Kee**</mark>**p in mind that you will not be able to enable Object Lock for an existing bucket.**

<figure><img src="../../../../../../.gitbook/assets/image (35) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once the bucket has been successfully created, to configure specific parameters for the object lock feature, please follow the steps below:

## Compliance Mode <a href="#compliance-mode" id="compliance-mode"></a>

Once you have enabled Object Lock for the bucket, you can set up Object Lock for the bucket by following these steps:

1\. In the bucket where object lock needs to be set up, select **Action** and select **Configure object lock retention**

<figure><img src="../../../../../../.gitbook/assets/image (36) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

2\. On the Configure object lock retention screen, select **Enable Object Lock retention policy**

<figure><img src="../../../../../../.gitbook/assets/image (37) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

3\. In **Retention Mode** : currently we only support **Compliance Mode** (this mode will protect the object version from changes or deletion until the retention period expires).

4\. In the **Retention Period** section : select the desired time to keep the objects in your bucket. For example, you choose 30 days, 60 days, 1000 days,...

<figure><img src="../../../../../../.gitbook/assets/image (38) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

5\. Select **Update.**

5\. Now, upload your objects. All uploaded objects will now be kept for the Retention period you have selected. During this period, no one will be able to delete your objects.

For example, in the image above, I configured to keep 60 days,

* If the date I upload the object is 10/25/2024. So this object will be kept until **10/25/2024 + 60 days = 12/24/2024**
* If the date I upload the object is 11/01/2024. So this object will be kept until **10/25/2024 + 60 days = 12/31/2024**

***

## Governance Mode <a href="#governance-mode" id="governance-mode"></a>

* <mark style="color:red;">**Currently, we do not support Governance mode**</mark>. If you use 3rd party software to set Object Locked in this Governance mode, the generated S3 key will have full permission to delete object versions in your bucket.

***

## **Legal Hold** <a href="#legal-hold" id="legal-hold"></a>

**The Object Legal Hold** feature in vStorage allows you to keep a version of an object from being deleted or overwritten. When this feature is enabled, anyone, including the Root User Account, cannot delete or modify that object until the legal hold is turned off.

After enabling Object Lock for the bucket, you can set up **Legal Hold** Object Lock for each object in the bucket by following these steps:

1\. At the object that needs to set object lock, select **Action** and select **Enable object legal hold**

<figure><img src="../../../../../../.gitbook/assets/image (39) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

2\. On the Enable object legal hold screen, select **Enable**

<figure><img src="../../../../../../.gitbook/assets/image (40) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* Legal hold only applies to each version of the object, so if enabled for a specific version, other versions can still be edited or deleted.
* This feature is different from **Retention Policy** because it only stops deleting or editing objects and does not have an end time.
{% endhint %}
