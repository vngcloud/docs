# Video On Demand Streaming

**Overview**

Ensure the best user experience when selecting and watching videos on devices over the internet. VNG Cloud's VOD service helps businesses:&#x20;

* Cost optimization.&#x20;
* Ensuring flexibility and easy compatibility with a variety of terminal devices.&#x20;
* Increase customer satisfaction with service.&#x20;
* Analyze multidimensional data in real time.

***

#### **Model** <a href="#videoondemandstreaming-cochephanphoidulieu" id="videoondemandstreaming-cochephanphoidulieu"></a>

<figure><img src="../../.gitbook/assets/image (156).png" alt=""><figcaption></figcaption></figure>

***

**Data Distribution Mechanism**

* Input data:
  * VNGCloud's Media Preparation system will connect to the customer's Storage server to retrieve content in MP4, MP3, HLS, MpegDash formats (formats that support play on the internet environment).&#x20;
  * Optional length of each media segment when packaging into HLS.&#x20;
  * Server Media Preparation will convert files in MP4 and MP3 formats into HLS format, a format that supports playback on OTT devices. For content on Origin that is HLS/MpegDash, the format will remain as the original data.&#x20;
  * After converting the format, the file will be transferred to Edge servers.
* Output data:
  * Supports output standards with content types such as:
    * MP4: https:// /.&#x20;
    * HLS: https:// /\<MP4/SMIL file path on origin>/index.m3u8.&#x20;
    * MpegDash: : https:// /\<manifest file path on origin?.
  * Support HTTPS protocol: by default all CDNs created on the system support SSL on the CDN domain. However, customers can upload their own Certificate to use with any name (refer to the certificate management section).&#x20;
  * Support MP4 Progressive play standard: stream MP4 files directly from the origin.&#x20;
  * Support for Adaptive Bitrate packaging through the definition of a smil file (Packaging application specification file) placed with MP4 files on the Origin server. The Media Preparation system will read the content of the smil file and convert MP4 files into HLS standard that supports Adaptive Bitrate. The output link syntax is as follows:&#x20;
    * HLS (smil ABR): https:// //index.m3u8.

***

#### **Feature** <a href="#videoondemandstreaming-tinhnangdichvu" id="videoondemandstreaming-tinhnangdichvu"></a>

* Supporting direct connection to the origin is Object Storage under the AWS S3 standard.&#x20;
* Customize the caching mechanism to suit the content type: Caching level.&#x20;
* Origin support when creating CDN.&#x20;
* Supports HTTPS option.&#x20;
* Supports output link security features: Customize cache time.&#x20;
* Supports automatic redirection from HTTP to HTTPS. Supports "developer" mode (Development Mode)&#x20;
* Multi Audio Selection: feature that supports separating Audio in MP4 files (in case there are multiple Audio formats in the file), this feature is supported in parallel with the Adaptive bitrate feature using smil files. The output link syntax is similar to the Adaptive Bitrate feature&#x20;
  * HLS (smil ABR): https:// /\<Path to smil file on VNGCloud Storage/Origin >/index.m3u8.

***

#### **VOD CDN Creation Guide** <a href="#videoondemandstreaming-huongdankhoitaovodcdn" id="videoondemandstreaming-huongdankhoitaovodcdn"></a>

* **Step 1:** Create VOD CDN via select the menu Video On Demand, select the button **Create New.**

<figure><img src="../../.gitbook/assets/image (157).png" alt=""><figcaption></figcaption></figure>

* **Step 2**: Creata a CDN

<figure><img src="../../.gitbook/assets/image (158).png" alt=""><figcaption></figcaption></figure>

* **Step 3**: Enter the CDN Name.
* **Step 4**: Choose the VOD type, includes
  * CDN Packaging (The vCDN system will package media from the customer's original video file).&#x20;
  * Origin packaging (customer's own packaging, vCDN only serves).&#x20;
  * MP4 (vCDN serves the original mp4 file directly from the origin to the end-user).
* **Step 5**: Select the segment size of the files "ts" with VoD Type is CDN Packaging.&#x20;
* **Step 6**: Optional VOD service features&#x20;
* **Step 7**: Depending on the user's request, enter basic rule policy information or advanced rule policy information for CDN.&#x20;
* **Step 8**: When filling in the correct and complete information, press the Submit button at the bottom of the interface and wait about 5 minutes for the system to set the CDN for the user.&#x20;
* **Step 9**: Users can access the CDN via vCDN Domain once the CDN has been created..

***

Once the CDN configuration is complete, users can access VoD CDNs via the links below:

* MP4: https:// \<CDN Domain>/<đường dẫn file MP4 trên origin>.
* MP3: https:// \<CDN Domain>/<đường dẫn file MP3 trên origin >.
* HLS: https:// \<CDN Domain>/<đường dẫn file MP4/SMIL trên origin>/index.m3u8.
* MpegDash: : https:// \<CDN Domain>/<đường dẫn file manifest trên origin>.
