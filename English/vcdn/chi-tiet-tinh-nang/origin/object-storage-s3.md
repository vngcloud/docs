# Object Storage S3

## Overview <a href="#tong-quan" id="tong-quan"></a>

**S3 Origin** is a type of origin used in vCDN to serve content from object storage services such as **Amazon S3** or similar solutions (e.g. VNG Cloud's vStorage). When using S3 Origin, content is delivered from your S3 bucket through the CDN network, improving access speed and reducing load on the origin system.

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

Currently, vCDN supports you to connect directly to an S3-compatible Object Storage origin. To connect, you need to enter the following information:

<figure><img src="../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

* **Access key:** The access key is retrieved from your Object Storage system.
* **Secret key:** Secret key corresponds to the Access key entered above.
* **Bucket:** The name of the bucket containing the contents on S3.
* **Region:** The region where your bucket is stored.
* **Endpoint** : The URL path to connect to the S3 service.
* **S3 Signature:** The S3 Signature used. You can choose to use Signature v2 or v4.
* **Use SSL:** Select to use SSL to encrypt the connection between vCDN and S3 Origin.
