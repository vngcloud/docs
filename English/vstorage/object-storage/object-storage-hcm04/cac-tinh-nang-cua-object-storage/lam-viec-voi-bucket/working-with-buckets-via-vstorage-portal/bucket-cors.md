# Bucket CORS

## **Overview** <a href="#tong-quan" id="tong-quan"></a>

**CORS (Cross-Origin Resource Sharing)** on ​​vStorage allows applications from a different domain (origin) to access resources in your bucket. This feature is useful when you want to access objects in your bucket from a web application running on a different domain, such as a frontend application that wants to load images from an S3 bucket.

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .

2\. Select **the project** containing **the bucket** you want to set up CORS for.

**3. Select the Action** icon and select **Set CORS.**

<figure><img src="../../../../../../.gitbook/assets/image (325).png" alt=""><figcaption></figcaption></figure>

4\. Here, you import the CORS configuration file. The CORS Configuration in vStorage is a JSON file with a list of rules that you want to apply. Each rule will include:

* **AllowedMethods** : Allowed HTTP methods, like `GET`, `PUT`, `POST`, `DELETE`, `HEAD`.
* **AllowedOrigins** : Domains allowed to access the bucket.
* **AllowedHeaders** : The types of headers that the application can send in the request.
* **ExposeHeaders** : The headers that the application can see in the response from S3.
* **MaxAgeSeconds** : The time in seconds that the browser should cache the results of a request before sending another request.

<figure><img src="../../../../../../.gitbook/assets/image (326).png" alt=""><figcaption></figcaption></figure>

5\. Select **Update** to save the configuration for CORS.

***

## Example <a href="#vi-du-minh-hoa" id="vi-du-minh-hoa"></a>

### **Example 1:** CORS allows a specific domain to access with the GET method <a href="#vi-du-1-cors-cho-phep-mot-domain-cu-the-truy-cap-voi-phuong-thuc-get" id="vi-du-1-cors-cho-phep-mot-domain-cu-the-truy-cap-voi-phuong-thuc-get"></a>

* Allow a specific domain to access objects in your bucket via the `GET`.

```bash
[
  {
    "AllowedOrigins": ["https://example.com"],
    "AllowedMethods": ["GET"],
    "AllowedHeaders": ["*"],
    "MaxAgeSeconds": 3000
  }
]
```

### **Example 2:** CORS for multiple domains and multiple HTTP methods <a href="#vi-du-2-cors-cho-nhieu-domain-va-nhieu-phuong-thuc-http" id="vi-du-2-cors-cho-nhieu-domain-va-nhieu-phuong-thuc-http"></a>

* Allows multiple domains to be accessed with different methods, including `GET`, `POST`, and `DELETE`.

```bash
[
  {
    "AllowedOrigins": ["https://example.com", "https://anotherdomain.com"],
    "AllowedMethods": ["GET", "POST", "DELETE"],
    "AllowedHeaders": ["Authorization", "Content-Type"],
    "ExposeHeaders": ["x-amz-request-id", "x-amz-id-2"],
    "MaxAgeSeconds": 3600
  }
]
```

{% hint style="info" %}
**Attention:**

* **Security**: Allow only trusted origins to avoid security risks.
* **CORS does not replace S3 permissions**: CORS only specifies which requests from other domains will be allowed, but actual access to the bucket is still controlled via **Bucket Policy**, **ACL**, or **IAM Policy**.
{% endhint %}
