# Bucket Versioning

Versioning is a feature that supports storing multiple past versions of objects stored in a bucket. With versioning, you can easily manage the history of data changes and protect data from loss due to accidental operations. Enabling versioning is an effective method to control and restore data in emergency situations.

To use versioning, please follow these steps:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).

2\. Select **the project** containing **the bucket** you want to set up versioning for.

**3. Select the Action** icon and select **Configure versioning**

{% hint style="info" %}
**Attention:**

* When **Object Lock** is enabled on a bucket in vStorage, **versioning** is **automatically enabled and cannot be disabled** on that bucket.
{% endhint %}

<figure><img src="../../../../../../.gitbook/assets/image (32) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

4\. At the versioning confirmation screen, please select **Enable versioning**.

<figure><img src="../../../../../../.gitbook/assets/image (33) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

After versioning is enabled, every time you upload an object with the same name, vStorage will create a new version for that object, and the old version will still be saved. You can select Show versions to view information about the object's versions.

<figure><img src="../../../../../../.gitbook/assets/image (34) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

Common operations with versioning include:

* **Upload new version of object** : When you upload a file with the same name to a bucket with versioning enabled, vStorage will retain previous versions of this file.
* **Delete specific version**:
  * In a bucket with versioning enabled, each object has a "version ID". To delete a specific version, simply find the correct version of the object and select delete.
  * If you delete the "current" version, vStorage will keep a "delete marker", marking the object as deleted but not deleting the old versions.
* **Restore an old object version to the current version** : you can select Restore at the version you want to restore to bring this object version to the latest version of the object.
  * Restoring an old version does not delete the current version or any other versions.
  * The version you want to restore will be copied as the latest version, preserving every version in the bucket.
{% endhint %}
