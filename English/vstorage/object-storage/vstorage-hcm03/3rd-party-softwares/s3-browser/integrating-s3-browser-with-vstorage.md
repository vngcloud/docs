# Integrating S3 Browser with vStorage

To integrate the S3 Browser tool with vStorage, you can follow the instructions below:

1. Download the S3 Browser user tool [here](https://s3browser.com/download.aspx).
2.  Open the **S3 Browser application → Account → Add new account**

    <figure><img src="../../../../../.gitbook/assets/image (12) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
3. Fill in the login information as follows:

* **Display name:** Display name of the account.
* **Account type:** Choose S3 Compatible Storage.
* **REST Endpoint:** Path to vstorage, [hcm01.vstorage.vngcloud.vn](http://hcm01.vstorage.vngcloud.vn/) (region HCM01 - Ho Chi Minh) or [han01.vstorage.vngcloud.vn](http://han01.vstorage.vngcloud.vn/) (Region HAN01 - Hanoi).
* **Access Key ID & Secret Access Key:** The key pair provided on the vStorage Portal.

4\. Choose **Use Secure transfer (SSL/TLS)** because vStorage only supports encrypted channels (HTTPS, port 443) to ensure data security, and does not support unencrypted channels (HTTP, port 80).

5\. Finally, click on the advanced settings part **Advanced S3-Compatible Storage Settings** in the bottom-left corner of the window.

<figure><img src="../../../../../.gitbook/assets/image (13) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Signature version:** vStorage supports both Signature V2 and Signature V4, but it is recommended to use Signature V4 because AWS S3 no longer supports Signature V2.
* **Addressing model:** vStorage supports both Path Style and Virtual hosted style. The difference between the two is the request path when sending it to the vstorage gateway. For path style, it is [`https://hcm01.vstorage.vngcloud.vn/v1/AUTH_{project_id}/{bucket}/{file`](https://hcm01.vstorage.vngcloud.vn/v1/AUTH_%7Bproject_id%7D/%7Bbucket%7D/%7Bfile)`}`, while for Virtual hosted style, it will be `https://{bucket}.`[`hcm01.vstorage.vngcloud.vn/{file`](http://hcm01.vstorage.vngcloud.vn/%7Bfile)`}`.
* Choose **Override storage region:** Fill in the value of Default region = HCM01 or HAN01.
* Close -> Save changes

<figure><img src="../../../../../.gitbook/assets/image (14) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

6\. If the S3 Browser connects successfully, the result will look like this:

<figure><img src="../../../../../.gitbook/assets/image (15) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
