# Step 5: Integrate 3rd party softwares with vStorage

After you have successfully initialized the project and initialized the S3 key, you can now use 3rd party softwares to connect and work with your project. The 3rd party softwares you can choose to use can be S3cmd, Cyberduck, Rclone, S3 Browser, MinIO Client,... In this document, we will guide you to connect S3 Browser with vStorage. S3 Browser is an optimized tool that allows you to share and upload your files. This tool has a relatively simple interface, is easy to use and is compatible with the API of the vStorage storage service.

To integrate the S3 Browser tool with vStorage, you can follow the instructions below:

1. Download the S3 Browser user tool here [https://s3browser.com/download.aspx](https://s3browser.com/download.aspx) .
2. Open the S3 Browser app **.** Select the Account folder **, then select Add new account**

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1).png" alt="" width="443"><figcaption></figcaption></figure>

3. The Add New Account screen appears, now you enter the following information:

* **Display name:** Display name of the account. Example: Demo\_HCM04
* **Account type** : Select **S3 Compatible Storage.**
* **REST Endpoint** : Path to vstorage, for Region HCM04 the path is [hcm04.vstorage.vngcloud.vn](http://hcm01.vstorage.vngcloud.vn/)
* **Access Key ID & Secret Access Key:** This is the S3 key pair you generated in step 2 earlier.

4. Select the **Use Secure transfer (SSL/TLS)** option because vStorage only supports encrypted transmission channels (HTTPS, port 443) to ensure data security, vStorage currently does not support unencrypted transmission channels (HTTP, port 80).
5. Select **Add new account.**

<figure><img src="../../../../.gitbook/assets/image (9) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

6. When the connection is successful, the S3 Browser screen will display as follows:

<figure><img src="../../../../.gitbook/assets/image (10) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
