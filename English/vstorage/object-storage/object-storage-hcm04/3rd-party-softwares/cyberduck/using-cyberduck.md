# Using Cyberduck

## Some common use cases <a href="#sudungcongcucyberduck-motsousecasethongthuong" id="sudungcongcucyberduck-motsousecasethongthuong"></a>

**Create a new bucket**

1. **On the Cyberduck** main screen , right-click on the blank page area and select **New Folder.** Or you can press **Ctrl + Shift + N.**
2. Enter a **bucket** name . The bucket name you enter must comply with our regulations. For details, please refer to [Container Limits .](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-bucket/pham-vi-gioi-han-bucket)

<figure><img src="../../../../../.gitbook/assets/image (429).png" alt=""><figcaption></figcaption></figure>

**Upload files to a bucket**

1. **On the Cyberduck** main screen , select **the bucket** you want to upload the file to.
2. Select **Upload** .
3. Select a file or folder from your computer then select **Choose** .
4. The file upload process begins. When the upload is complete, Cyberduck will notify you that the file was uploaded Successfully.

<figure><img src="../../../../../.gitbook/assets/image (431).png" alt=""><figcaption></figcaption></figure>

**Delete an object in a bucket**

1. **On the Cyberduck** main screen , select **the bucket containing the object** you want to delete.
2. At the object you want to delete, right-click and then select **Delete** .

<figure><img src="../../../../../.gitbook/assets/image (433).png" alt=""><figcaption></figcaption></figure>

1. On the delete confirmation screen, continue to select **Delete** .

***

## Some advanced use cases <a href="#mot-so-use-case-nang-cao" id="mot-so-use-case-nang-cao"></a>

**Share objects via Presigned URL**

1. **On the Cyberduck** main screen , select **the bucket containing the object** you want to share via Presigned URL.
2. At the object you want to share, right-click then select **Copy URL** if you want to copy the Presign URL or select **Open URL** if you want to open the Presign URL directly on the browser.
3. Select one of the methods for **Presign URL** that you want.

<figure><img src="../../../../../.gitbook/assets/image (434).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (436).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* Do not use an old/new version of Cyberduck on operating systems with an old/new version because errors may occur.
* When you use Cyberduck to Copy/ Move/ Rename objects on the vStorage system, it may cause errors. We recommend that you do not use these features.
* Cyberduck does not support cleaning incomplete segments when uploading large objects (Multipart upload). When you use Cyberduck (s3, swift) to upload large files (multipart upload), the file is divided into multiple segments to upload to the vStorage system. During the file upload process, some segments may be uploaded, some segments may not be uploaded due to errors such as network problems, vStorage system overload, your Cyberduck stops running, hangs, etc. The file is then considered as an unsuccessful upload, the uploaded segments are considered as incomplete segments or garbage segments and are occupying your storage space. Currently, Cyberduck does not support cleaning these garbage segments. Therefore, we recommend that you consider carefully before using this tool.
{% endhint %}
