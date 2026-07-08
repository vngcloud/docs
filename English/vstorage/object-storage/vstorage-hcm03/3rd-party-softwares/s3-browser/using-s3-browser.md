# Using S3 Browser

#### Common usecase <a href="#usings3browser-commonusecase" id="usings3browser-commonusecase"></a>

On the interface, you can easily see and perform various operations, including:

* **Add/Delete bucket**
* **Upload/Download file**
* **Create/Delete Folder, File**

<figure><img src="../../../../../.gitbook/assets/image (16) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Below are some commonly used advanced configurations:

1. **Tools → Options**

<figure><img src="../../../../../.gitbook/assets/image (17) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

2. **General**

* **Enable Multipart uploads with part size**: depending on the file size, consider the size for each part to ensure it does not exceed 1000 parts (the maximum number of parts that vStorage supports for each file).

<figure><img src="../../../../../.gitbook/assets/image (18) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Bandwidth Throttling:**

<figure><img src="../../../../../.gitbook/assets/image (19) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Folder for temporary files:**

<figure><img src="../../../../../.gitbook/assets/image (20) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Proxy:**

<figure><img src="../../../../../.gitbook/assets/image (21) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:**

1. Do not use an outdated or excessively new version of S3 Browser on operating systems that are too old or too new, as it may encounter errors.
2. S3 Browser supports cleaning up incomplete segments when uploading large objects (multipart upload). When using S3 Browser to upload large files (multipart upload), the file is divided into multiple segments to be uploaded to the vStorage system. During the file upload process, some segments may be uploaded successfully, while others may not due to issues such as network problems, vStorage system overload, your S3 Browser crashing, hanging, etc. The file is considered unsuccessfully uploaded, and the uploaded segments are considered incomplete or junk segments, occupying your storage space. We recommend removing these junk segments to optimize costs and storage capacity by:
   1. Open the S3 Browser application, select Tools, and then choose Uncompleted Multipart Uploads.
   2. Select one or more parts of the uploaded file and choose Abort or right-click and select Abort.

For more details, refer to: [https://s3browser.com/uncompleted-multipart-uploads.aspx](https://s3browser.com/uncompleted-multipart-uploads.aspx)
{% endhint %}
