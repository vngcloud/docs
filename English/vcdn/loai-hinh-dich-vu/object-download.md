# Object Download

## **Overview** <a href="#objectdownload-tongquan" id="objectdownload-tongquan"></a>

GreenNode's Object Download service helps businesses: optimize costs, ensure flexibility, and easily adapt to a variety of terminal devices, thereby increasing customer satisfaction with the service with the ability to analyze multidimensional data in real time.

***

## **Model** <a href="#objectdownload-cochephanphoidulieu" id="objectdownload-cochephanphoidulieu"></a>

<figure><img src="../../.gitbook/assets/image (159) (1).png" alt=""><figcaption></figcaption></figure>

***

## **Data Distribution Mechanism** <a href="#objectdownload-cochephanphoidulieu-1" id="objectdownload-cochephanphoidulieu-1"></a>

* **Input data** :
  * **GreenNode's Origin Gateway** system will connect to **the customer's origin server** or storage to retrieve the content requested from the client. This content can be in any format, for example: , , images, fonts ( ), etc.`.js.css.tff`
  * If the content is large, **Origin Gateway** will split the content into small requests (5MB) and download them simultaneously (byte-range download). This helps to speed up the download and serve the user as soon as the first data is received.
  * Data from **the Origin Gateway** will then be distributed to **Edge servers** to serve users.
* **Output data** :
  * **HTTPS protocol support** :
    * By default, all CDNs created on the system support SSL on the CDN domain.
    * Customers can also upload their own **Certificates** to use with custom domains. (See the Certificate Management section for instructions).
  * **HTTP/2 Support** :
    * HTTP/2 speeds up connection and data transmission on the browser, providing a smoother experience.

***

## **Service Features** <a href="#objectdownload-tinhnangdichvu" id="objectdownload-tinhnangdichvu"></a>

* **Support for direct connection to Origin:** The vCDN system supports direct connection to Object Storage data sources using the S3-compatible protocol standard. This helps customers easily integrate data from popular cloud storage services or from vStorage.
* **Customize caching mechanism:** allows users to configure the level of data caching at Edge Servers, suitable for each type of content.
* **Origin Support when creating CDN:** The vCDN system allows defining data sources from Object Storage or Origin Server specified by the customer. This provides flexibility in integrating data from different sources.
* **HTTPS Support:** By default, all CDNs created support HTTPS to secure data. Users can also **upload their own SSL certificates** to use with their own domains.
* **Auto Redirect from HTTP to HTTPS** : Supports automatic redirection of all HTTP requests to HTTPS to enhance security and improve user experience.
* **Output link security:** Supports advanced security mechanisms to protect content, including: CORS, Whitelist/ Blacklist IP, Geo Block, HTTP Referer Block,...
* **Development Mode Support:** This feature allows you to temporarily disable caching on the Edge Server to support testing or testing content during development. All requests will be returned directly from Origin, allowing content to be updated immediately without clearing the cache.

***

## **Instructions for create an Object Download CDN** <a href="#objectdownload-huongdankhoitaoobjectdownloadcdn" id="objectdownload-huongdankhoitaoobjectdownloadcdn"></a>

### **Step 1: Create an Object Download** <a href="#buoc-1-tao-object-download" id="buoc-1-tao-object-download"></a>

First, you need to initialize an Object Download according to the following instructions:

1. Access vCDN Portal at [https://vcdn.vngcloud.vn](https://vcdn.vngcloud.vn/live-entrypoint/list.html)
2. Select **Object Download** , then select **Create new.**

<figure><img src="../../.gitbook/assets/image (41) (1).png" alt=""><figcaption></figcaption></figure>

3. Continue to enter/select:

* **CDN Info:**
  * **CDN Name:** Enter the identifier name for the CDN you want to create.

<figure><img src="../../.gitbook/assets/image (42) (1).png" alt=""><figcaption></figcaption></figure>

* **Origin:**
  * **HTTP Origin** : Server supports HTTP protocol.
    * **Fail-Over Error Code:** List of HTTP error codes (e.g. 500, 502, 503, 504) that, if encountered, will trigger a fail-over to another Origin.
    * **Origin Load Balancing:** Load balancing mechanism between designated Origin Servers.
    * **Origin Host Header:** Header used when sending requests from vCDN to Origin Server.
    * **IP Address:** The IP address of the Origin Server (e.g. IPv4 like 1.1.1.1 or IPv6).
    * **Weight:** Defines the priority of each Origin Server when load balancing (the higher the value, the more traffic received).
  * **S3 Origin** : Data source on S3-compatible Object Storage system.
    * **Access key:** The access key is retrieved from your Object Storage system.
    * **Secret key:** Secret key corresponds to the Access key entered above.
    * **Bucket:** The name of the bucket containing the contents on S3.
    * **Region:** The region where your bucket is stored.
    * **Endpoint** : The URL path to connect to the S3 service.
    * **S3 Signature:** The S3 Signature used. You can choose to use Signature v2 or v4.
    * **Use SSL:** Select to use SSL to encrypt the connection between vCDN and S3 Origin.
  * **Host Origin** : Data from a specific host.
    * **Origin Host Header:** Header sent to the Origin Server in the HTTP request.
    * **Use SSL:** Enable SSL to encrypt the connection to Host Origin.
    * **Host Origin**

<figure><img src="../../.gitbook/assets/image (43) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (44) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (45) (1).png" alt=""><figcaption></figcaption></figure>

*   **Security:**

    * **HTTPS (HTTP/2)** : Enable or disable HTTPS security for the CDN stream. You can create a new **Certificate** by selecting **Add new** .
    * **HTTP Strict Transport Security (HSTS)** : Enforces a web security policy for your website, sending HSTS headers with all HTTPS requests. If configured incorrectly, HSTS can make your website inaccessible for long periods of time.
    * **Max Age Header (max-age):** Specifies how long HSTS headers are cached in the browser.
    * **Apply HSTS policy to subdomains (includeSubDomains):** Every domain will inherit the same HSTS headers. If any of your domains don't support HTTPS, they won't be accessible.
    * **Preload:** Allows the browser to preload the HSTS configuration automatically. Preloading can make a non-HTTPS-enabled site completely inaccessible.
    * **Relative Canonical URL:** A canonical URL allows you to tell search engines that similar URLs are actually the same content. This is useful when you have a product or content that can be found on multiple URLs or even multiple websites.
    * **No-Sniff Header:** Send the "X-Content-Type-Options: nosniff" header to prevent Internet Explorer and Google Chrome from checking MIME types other than the declared Content-Type.

    <figure><img src="../../.gitbook/assets/image (46) (1).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../../.gitbook/assets/image (47) (1).png" alt=""><figcaption></figcaption></figure>

    * **Token Configuration** :
      * **Token Type** : Select the token type used to authenticate viewers. You can choose token type Akamai, SBD or VNG.

    <figure><img src="../../.gitbook/assets/image (48) (1).png" alt=""><figcaption></figcaption></figure>

    * **Access Filter:**
      * **IP Address CIDR** : Limit access based on IP address by selecting **Allow** / **Block** and entering the corresponding IP address or CIDR.
      * **HTTP Referer** : Limit access from specific websites by selecting **Allow/ Block** and entering the corresponding domain.
      * **Geo Location:** Limit access by country/region by selecting **Allow/ Block** and entering the corresponding Geo Location code. You can refer to the corresponding country code value at [https://en.wikipedia.org/wiki/List\_of\_ISO\_3166\_country\_codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) .
    * **CORS Configuration**
      * **Simple** : When selecting Simple, you only need to specify specific domains that are allowed access through **Allow Origin.**
      * **Advance** : When selecting Advance, in addition to specifying a specific domain, you need to configure more details about **Allow Header, Allow Method, Expose Header, Allow Credentials** allowed.

    <figure><img src="../../.gitbook/assets/image (49) (1).png" alt=""><figcaption></figcaption></figure>

    * **Always Use HTTPS:** Enable or disable automatic redirection of all HTTP requests to HTTPS for increased security and improved user experience.
    * **Small Object:** When you enable this option, if the content is large, **Origin Gateway** will split the content into small requests (5MB) and download them simultaneously (byte-range download). This helps to speed up the download and serve the user as soon as the first data is received.
    * **Minimum TLS Version** : The lowest version of the TLS protocol allowed. We support TLS 1.0, TLS 1.1, TLS 1.2, TLS 1.3 protocols. Please choose to use higher versions (TLS 1.2 or 1.3) to ensure security.

    <figure><img src="../../.gitbook/assets/image (50) (1).png" alt=""><figcaption></figcaption></figure>

    * **Caching:**
      * **Caching Level** : Determines the CDN cache level. With VOD, vCDN is providing 3 cache levels including: URL without query string only, Skip Query String of URL, URL With Query String.
      * **Server Cache Expiration (TTL):** The amount of time that the vCDN system will cache your resources. During this time, the vCDN system will not access the origin server but respond to requests from the vCDN cache. You can choose this time from 30 minutes to 1 year depending on your system's needs.
      * **Browser Cache Expiration:** The time vCDN asks the user's browser to cache files locally.
      * **Development mode:** This feature allows you to temporarily disable caching on the Edge Server to support testing or testing content during development. All requests will be returned directly from Origin, allowing content to be updated immediately without clearing the cache.

    <figure><img src="../../.gitbook/assets/image (51) (1).png" alt=""><figcaption></figcaption></figure>

    * **Page Rules:** This feature helps customers optimize conditions and options to help the website demonstrate many different purposes. To create Page rules, please select **Create Page Rule** , a popup will appear, now you need to select:
      * **URL pattern:** need to apply pagerule, support declaration type “\*” represents a string of characters. For example: /trang\_landing\_cu.html. After entering URL pattern, select **Add new rule** . Each Rule when satisfying the condition of the requested URI will be able to optionally execute one of the following actions:
        * Always Use HTTPS
        * Server Cache TTL
        * Browser Cache TTL
        * Bypass Cache By Cookie
        * Bypass Cache By Device Type
        * Forwarding URL
        * Response Header Override
        * Resolve Origin Override
        * Origin Base Directory
        * Deny Access
      * Select **Save changes** to save the changes.

    <figure><img src="../../.gitbook/assets/image (52) (1).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../../.gitbook/assets/image (53) (1).png" alt="" width="375"><figcaption></figcaption></figure>

    <figure><img src="../../.gitbook/assets/image (54) (1).png" alt="" width="348"><figcaption></figcaption></figure>

4. Select **Submit** to complete the creation of the Object Download.

### **Step 2: Download the file** <a href="#buoc-2-tai-tep-xuong" id="buoc-2-tai-tep-xuong"></a>

Once you have completed the Object Download initialization, you can download the file using the links below:

```
https:// <CDN Domain>/<đường dẫn file trên origin>
```

If you are using an S3 origin, note that your origin file path will include the bucket name.

For example:

```
https:// <CDN Domain>/<tên bucket>/<tên object>
```
