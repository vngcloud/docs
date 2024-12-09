# Video On Demand Streaming

## **Overview** <a href="#videoondemandstreaming-tongquan" id="videoondemandstreaming-tongquan"></a>

Ensure the best user experience when selecting and viewing videos on devices over the internet.

VNG Cloud's VOD service helps businesses:

* Cost optimization.
* Ensures flexibility and easy compatibility with a variety of terminals.
* Increase customer satisfaction with service.
* Real-time multidimensional data analysis.

***

## **Model** <a href="#videoondemandstreaming-cochephanphoidulieu" id="videoondemandstreaming-cochephanphoidulieu"></a>

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

***

## **Data Distribution Mechanism** <a href="#videoondemandstreaming-cochephanphoidulieu-1" id="videoondemandstreaming-cochephanphoidulieu-1"></a>

### **Input data processing procedure** <a href="#quy-trinh-xu-ly-du-lieu-dau-vao" id="quy-trinh-xu-ly-du-lieu-dau-vao"></a>

The vCDN system connects to **the customer's Storage** to retrieve content, specifically:

* **Supported input formats** :
  * **MP4** (video), **MP3** (audio).
  * **HLS** and **MpegDash** (streaming standards).
* **Options for processing with original format** :
  * **MP4/MP3** : **Converted to HLS** , a popular format for playback on OTT (Over-the-Top) devices.
  * **HLS/MpegDash** : If the data is already in this format, the system keeps it as is (no conversion).
* **Media Segment** :
  * Optional length of each media segment when packaging into HLS.

### **Data processing on Media Preparation Server** <a href="#quy-trinh-xu-ly-du-lieu-tren-media-preparation-server" id="quy-trinh-xu-ly-du-lieu-tren-media-preparation-server"></a>

* **Format conversion** : The system reads the input file from origin and converts:
  * **MP4/MP3 → HLS** .
  * Read SMIL file (if any) to generate **Adaptive Bitrate (ABR)** standard .
* **SMIL support for Adaptive Bitrate** :
  * SMIL is a specification file containing bitrate information and corresponding video versions.
  * The system reads SMIL files from origin and converts them to HLS ABR, ensuring a smooth experience across multiple network speeds.
* **Data Distribution** : After conversion, files are pushed to **Edge Server** to serve viewers.

### **Output data** <a href="#du-lieu-dau-ra" id="du-lieu-dau-ra"></a>

The vCDN system provides popular delivery standards, supports HTTPS protocol and Adaptive Bitrate feature. Details are as follows:

* **Standard output paths**
  *   **MP4** : Stream files directly from origin (MP4 Progressive Streaming).

      ```
      https://<CDN Domain>/<đường dẫn file MP4 trên origin>
      ```
  *   **HLS** : Used for segmented content or has SMIL supporting ABR.

      ```
      https://<CDN Domain>/<đường dẫn file MP4/SMIL trên origin>/index.m3u8
      ```
  *   **MpegDash** :

      ```
      https://<CDN Domain>/<đường dẫn file manifest trên origin>
      ```
* **HTTPS Support**
  * **Default** : All CDNs support HTTPS via system SSL certificates.
  * **Custom** : Users can upload their own SSL certificates to use with custom domains.
* **Adaptive Bitrate Support (HLS SMIL ABR)**
  *   URLs supporting ABR via SMIL files:

      ```
      https://<CDN Domain>/<Đường dẫn tới file SMIL trên origin>/index.m3u8
      ```

## **Service Features** <a href="#videoondemandstreaming-tinhnangdichvu" id="videoondemandstreaming-tinhnangdichvu"></a>

* **Support for direct connection to Origin:** The vCDN system supports direct connection to Object Storage data sources using the S3-compatible protocol standard. This helps customers easily integrate data from popular cloud storage services or from vStorage.
* **Customize caching mechanism:** allows users to configure the level of data caching at Edge Servers, suitable for each type of content.
* **Origin Support when creating CDN:** The vCDN system allows defining data sources from Object Storage or Origin Server specified by the customer. This provides flexibility in integrating data from different sources.
* **HTTPS Support:** By default, all CDNs created support HTTPS to secure data. Users can also **upload their own SSL certificates** to use with their own domains.
* **Auto Redirect from HTTP to HTTPS** : Supports automatic redirection of all HTTP requests to HTTPS to enhance security and improve user experience.
* **Output link security:** Supports advanced security mechanisms to protect content, including: CORS, Whitelist/ Blacklist IP, Geo Block, HTTP Referer Block,...
* **Development Mode Support:** This feature allows you to temporarily disable caching on the Edge Server to support testing or testing content during development. All requests will be returned directly from Origin, allowing content to be updated immediately without clearing the cache.
* **Multi Audio Selection:**
  * **Audio separation function** :
    * Supports splitting and selecting different audio tracks in one MP4 file if the file contains multiple audio formats (e.g. multiple languages ​​or versions).
    * This feature is compatible with **Adaptive Bitrate (ABR)** and uses SMIL files for definition.
  *   **Multi Audio Selection URL Syntax (with ABR)** :

      ```
      https://<CDN Domain>/<Đường dẫn tới file SMIL trên VNGCloud Storage/Origin>/index.m3u8
      ```

***

## Instructions for create a VOD CDN <a href="#videoondemandstreaming-huongdankhoitaovodcdn" id="videoondemandstreaming-huongdankhoitaovodcdn"></a>

### **Step 1: Create a VOD** <a href="#buoc-1-tao-vod" id="buoc-1-tao-vod"></a>

First, you need to initialize a VOD following these instructions:

1. Access vCDN Portal at [https://vcdn.vngcloud.vn](https://vcdn.vngcloud.vn/live-entrypoint/list.html)
2. Select **Video On Demand** , then select **Create new.**

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

3. Continue to enter/select:

* **CDN Info:**
  * **CDN Name:** Enter the identifier name for the CDN you want to create.
  * **VOD Type:** Select the VOD type you want to use. Currently vCDN supports 3 types of VOD including:
    * **CDN Packaging:** The vCDN system will package media from the customer's original video file.
    * **Origin Packaging:** Customer's origin packaging, vCDN only serves
    * **MP4:** vCDN serves original mp4 files directly from origin to end-user
  * **Segment Size:** Select the "hash" time of "ts" files with VoD service type as CDN Packaging.

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

*   **Security:**

    * **HTTPS (HTTP/2)** : Enable or disable HTTPS security for the CDN stream. You can create a new **Certificate** by selecting **Add new** .
    * **Always Use HTTPS:** Enable or disable automatic redirection of all HTTP requests to HTTPS for increased security and improved user experience.
    * **Minimum TLS Version** : The lowest version of the TLS protocol allowed. We support TLS 1.0, TLS 1.1, TLS 1.2, TLS 1.3 protocols. Please choose to use higher versions (TLS 1.2 or 1.3) to ensure security.
    * **Token Configuration** :
      * **Token Type** : Select the token type used to authenticate viewers. You can choose token type Akamai, SBD or VNG.

    <figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

    * **Access Filter:**
      * **IP Address CIDR** : Limit access based on IP address by selecting **Allow** / **Block** and entering the corresponding IP address or CIDR.
      * **HTTP Referer** : Limit access from specific websites by selecting **Allow/ Block** and entering the corresponding domain.
      * **Geo Location:** Limit access by country/region by selecting **Allow/ Block** and entering the corresponding Geo Location code. You can refer to the corresponding country code value at [https://en.wikipedia.org/wiki/List\_of\_ISO\_3166\_country\_codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) .
    * **CORS Configuration**
      * **Simple** : When selecting Simple, you only need to specify specific domains that are allowed access through **Allow Origin.**
      * **Advance** : When selecting Advance, in addition to specifying a specific domain, you need to configure more details about **Allow Header, Allow Method, Expose Header, Allow Credentials** allowed.

    <figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

    * **Caching:**
      * **Caching Level** : Determines the CDN cache level. With VOD, vCDN is providing 3 cache levels including: URL without query string only, Skip Query String of URL, URL With Query String.
      * **Server Cache Expiration (TTL):** The amount of time that the vCDN system will cache your resources. During this time, the vCDN system will not access the origin server but respond to requests from the vCDN cache. You can choose this time from 30 minutes to 1 year depending on your system's needs.
      * **Browser Cache Expiration:** The time vCDN asks the user's browser to cache files locally.
      * **Development mode:** This feature allows you to temporarily disable caching on the Edge Server to support testing or testing content during development. All requests will be returned directly from Origin, allowing content to be updated immediately without clearing the cache.

    <figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

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

    <figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>



    <figure><img src="../../.gitbook/assets/image (38).png" alt="" width="375"><figcaption></figcaption></figure>

    <figure><img src="../../.gitbook/assets/image (39).png" alt="" width="348"><figcaption></figcaption></figure>



4. Select **Submit** to complete VOD creation.

#### **Step 2: Access VOD** <a href="#buoc-2-truy-cap-vod" id="buoc-2-truy-cap-vod"></a>

Once you have completed the VOD initialization, you can access the VOD CDNs via the links below:

* **MP4:**

```
https:// <CDN Domain>/<đường dẫn file MP4 trên origin>
```

* **MP3:**

```
https:// <CDN Domain>/<đường dẫn file MP3 trên origin >
```

* **HLS:**

```
https:// <CDN Domain>/<đường dẫn file MP4/SMIL trên origin>/index.m3u8
```

* **MpegDash:**

```
https:// <CDN Domain>/<đường dẫn file manifest trên origin>
```
