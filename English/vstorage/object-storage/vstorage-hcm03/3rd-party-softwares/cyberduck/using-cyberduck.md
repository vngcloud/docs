# Using Cyberduck

#### Common usecase <a href="#usingcyberduck-commonusecase" id="usingcyberduck-commonusecase"></a>

**Create a container**

1. At the main screen of **Cyberduck**, right-click in the blank area and select **New Folder**. Alternatively, you can press the key combination **Ctrl + Shift + N**.
2. Enter the **container name**. The container name you enter must comply with our guidelines. For details, refer to the \[Container Naming Restrictions]\(#).

![](https://contabo.com/blog/wp-content/uploads/2022/12/image-7.png)

![](https://docs.vngcloud.vn/download/attachments/69468442/image2023-7-14\_14-15-57.png?version=1\&modificationDate=1703485380000\&api=v2)

**Upload an object into a container**

1. At the main screen of **Cyberduck**, select the **container** to which you want to upload the file.
2. Choose **Upload**.
3. Select the file or folder from your computer, then choose **Choose**.
4. The file upload process begins. When the upload is complete, Cyberduck will notify you that the file has been uploaded successfully.

![](https://contabo.com/blog/wp-content/uploads/2022/12/image-9.png)

**Delete an object**

1. At the main screen of **Cyberduck**, select the **container** containing the **object** you want to delete.
2. On the object you want to delete, right-click, then choose **Delete**.
3. On the confirmation delete screen, proceed to select **Delete**.

<figure><img src="../../../../../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Advanced usecase <a href="#usingcyberduck-advancedusecase" id="usingcyberduck-advancedusecase"></a>

**Share object via Presign URL**

1. On the main screen of **Cyberduck**, select the **container** containing the **object** you want to share via the Presign URL.
2. For the object you want to share, right-click, then choose **Copy URL** if you want to copy the Presign URL or choose **Open URL** if you want to open the Presign URL directly in the browser.
3. Choose one of the methods for the **Presign URL** that you prefer.

<figure><img src="../../../../../.gitbook/assets/image (9) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (10) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



{% hint style="info" %}
**Note:**

* Do not use Cyberduck versions that are too old or too new on operating systems that are too old or too new, as it may result in errors.
* When using Cyberduck to perform Copy/Move/Rename operations on objects in the vStorage system, it may cause errors. We recommend not using these features.
* Cyberduck does not support cleaning up incomplete segments when uploading large objects (Multipart upload). When using Cyberduck (s3, swift) to upload a large file (multipart upload), the file is divided into multiple segments to upload to the vStorage system. During the file upload process, some segments may be uploaded, and some may not be uploaded due to errors such as network issues, overloaded vStorage system, your Cyberduck being stopped, hanging, etc. The file is then considered unsuccessfully uploaded, and the uploaded segments are considered incomplete or garbage segments, occupying your storage capacity. Currently, Cyberduck does not support the feature of cleaning up these garbage segments. Therefore, we recommend carefully considering before using this tool.
{% endhint %}
