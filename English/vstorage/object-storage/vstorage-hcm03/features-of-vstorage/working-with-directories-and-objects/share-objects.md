# Share objects

By default, all objects in vStorage are private. Only the owners of these objects have access to them. However, object owners can optionally share them with other users by creating temporary URLs. Here we provide you with 2 types of URLs, including:

* Temporary URL: uses authentication information from your OpenStack Swift account.
* Presigned URL: uses authentication information from your S3 key.

When you create a Temporary URL or Presigned URL for one of your objects, you must provide your security authentication information, then specify the container name, object name, and the expiration date and time of the corresponding URL. These URLs are only valid for the specified period. Anyone receiving these URLs can View or Download the object. We advise you to carefully consider the objects you want to share as well as the time you want to share your resources with those objects. For more details on securing URLs, see Access Control.

To share objects, follow the instructions below:

{% tabs %}
{% tab title="Using vStorage Portal" %}
To share an object within a container, you can follow the steps below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).
2. Select the **project** and **container**, then choose one or more **objects** you want to share.
3. Choose ![](http://docs.vngcloud.vn/download/thumbnails/67994213/image2023-3-6_10-50-12.png?version=1\&modificationDate=1701065525000\&api=v2) or select the icon ![](http://docs.vngcloud.vn/download/thumbnails/67994213/image2023-2-6_10-20-54.png?version=1\&modificationDate=1701065525000\&api=v2) at the object you want to share and select ![](http://docs.vngcloud.vn/download/thumbnails/67994213/image2023-11-27_13-17-4.png?version=1\&modificationDate=1701065827000\&api=v2).
4. Choose the **Protocol** as:
5. **OpenStack Swift** if you want to create a **Temporary URL**.
6. **S3** if you want to create a **Presigned URL**.

5\. Select **Mode**:

* If the **Protocol** is **OpenStack Swift**, you can choose **Mode** as **Download** or **View**.
* If the **Protocol** is **S3**, the **Presigned URL** path will be used by default to **View** the object.

6\. If you choose the S3 Protocol, you need to enter the **S3 key** information here. S3 key information can be obtained in IAM. You can choose Click [here](https://iam.console.vngcloud.vn/vstorage-credentials/s3) to go to IAM and manage s3 keys. to view detailed information about created S3 key pairs and create new S3 key pairs for use. For more details, refer to [Create a S3 key](../../identity-and-access-management/managing-vstorage-access-account/service-account/vstorage-credentials/create-a-s3-key.md).

7\. Enter the **Expiration time** you want to share the object, meaning the time the access path (Temporary URL) to the object is valid. You can limit the number of **days, hours, and minutes** that the access path to the object exists.

8\. Choose **Generate**.

9\. Choose ![](http://docs.vngcloud.vn/download/thumbnails/67994213/image2023-3-6_10-51-24.png?version=1\&modificationDate=1701065525000\&api=v2) to copy each URL for each object. We generate a separate URL for each object.

If you share an object through Temporary URL or Presigned URL in View mode, you will receive a URL. Copy this URL and paste it into any browser you are using. When you paste the URL and open it:

* If your browser supports directly opening this type of object, you can view the object directly in the browser. While the object is open in the browser, the expiration time of the URL is still counted. If your URL is still valid, you can right-click and download the object (download from the browser to your personal device rather than from vStorage to your personal device). If your URL has expired, you cannot right-click to download the object, and when you reload the browser, the displayed object data will also disappear.
* If your browser does not support directly opening this type of object, we automatically switch the object sharing mechanism to Download, and the system will automatically download this object to your personal device.
* For details on which browsers support directly opening this type of object, refer to: [![](https://fileinfo.com/svg/favicon.svg)FileInfo.com - The File Format Database](https://fileinfo.com/) .

To share the entire object in a container, instead of creating multiple URLs for each object, you can share the entire container using the Turn container public feature. For details, see [Make container public](http://docs.vngcloud.vn/display/VSEN/Make+container+public).
{% endtab %}

{% tab title="Using vStorage API" %}
In addition to the traditional management interface, we also provide an API that allows you to integrate with your applications and tools using vStorage for data storage.

1. [Khởi tạo tài khoản Service Account](broken-reference) nếu chưa có
2. Lấy thông tin access token. Tham khảo tại [Chứng thực với Service Account](broken-reference)
3. If you want to create a **Presigned URL**, you need to enter the **S3 key** information. S3 key information can be obtained in IAM. You can choose Click [here](https://iam.console.vngcloud.vn/vstorage-credentials/s3) to go to IAM and manage s3 keys. to view detailed information about created S3 key pairs and create new S3 key pairs for use. For more details, refer to [Create a S3 key](../../identity-and-access-management/managing-vstorage-access-account/service-account/vstorage-credentials/create-a-s3-key.md).
4. To obtain Temporary URL or Presigned URL for sharing objects through vStorage API, please refer to the [API download/share object](https://docs.api.vngcloud.vn/service-docs/vstorage-api.html#tag/object/operation/retrieveDownloadObjectTempURLUsingPOST).

**Example 1: Create object temporary URL**

```json
Request:
curl -X POST 'https://hcm03-api.vstorage.vngcloud.vn/api/v1/projects/77bd99c393dc4bf5a796b0c327cd70bd/containers/test/objects/2009009063434563310.jpg/download_tempurls'
-H 'Authorization: Bearer access_token'
-H 'Content-Type: application/json'
-d '{"timeExpire":3600,"urlType":"swift","viewMode":"view"}'
Response:
{
    "errorMsg": null,
    "code": 200,
    "success": true,
    "data": {
        "2009009063434563310.jpg": "https://hcm03.vstorage.vngcloud.vn/v1/AUTH_77bd99c393dc4bf5a796b0c327cd70bd/test/2009009063434563310.jpg?temp_url_sig=465d7f6f07536c4fdcd70b8a53516fe53874bf5f&temp_url_expires=1763095206&inline"
    }
}
```

**Example 2: Create object presigned URL**

```json
Request:
curl -X POST 'https://hcm03-api.vstorage.vngcloud.vn/api/v1/projects/77bd99c393dc4bf5a796b0c327cd70bd/containers/test/objects/2009009063434563310.jpg/download_tempurls'
-H 'Authorization: Bearer ***'
-H 'Content-Type: application/json'
-d '{"timeExpire":3600,"urlType":"s3","viewMode":"view","accessKey":"d461f281e569d814dfd491ee989dba28","secretKey":"***"}'
Response:
{
    "errorMsg": null,
    "code": 200,
    "success": true,
    "data": {
        "2009009063434563310.jpg": "https://test.hcm03.vstorage.vngcloud.vn/2009009063434563310.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20251114T034634Z&X-Amz-SignedHeaders=host&X-Amz-Expires=3600&X-Amz-Credential=d461f281e569d814dfd491ee989dba28%2F20251114%2FHCM03%2Fs3%2Faws4_request&X-Amz-Signature=4d5ef43478c90eb681e40ec8e77d2d1b0e6f5e7757f0ba5b8b48a651dd438e3e"
    }
}
```
{% endtab %}

{% tab title="Using 3rd party softwares" %}
vStorage is also compatible with tools using the S3 protocol on your end. You can easily use familiar tools such as Rclone, s3cmd, Cyberduck, etc.

To obtain Temporary URL or Presigned URL for sharing objects through 3rd party software, please refer to the [3rd Party Softwares](http://docs.vngcloud.vn/display/VSEN/3rd+Party+Softwares).
{% endtab %}
{% endtabs %}

