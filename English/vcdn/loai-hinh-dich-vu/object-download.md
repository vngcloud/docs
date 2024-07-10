# Object Download

#### **Overview** <a href="#objectdownload-tongquan" id="objectdownload-tongquan"></a>

The Object Download service from VNG Cloud helps businesses to: optimize costs, ensure flexibility, easily compatible with a variety of end devices, thereby increasing customer satisfaction with the service and enabling multidimensional real-time data analysis.

***

#### **Model** <a href="#objectdownload-cochephanphoidulieu" id="objectdownload-cochephanphoidulieu"></a>

<figure><img src="../../.gitbook/assets/image (159).png" alt=""><figcaption></figcaption></figure>

***

#### **Data Distribution Mechanism** <a href="#objectdownload-cochephanphoidulieu" id="objectdownload-cochephanphoidulieu"></a>

* Input data:
  * VNGCloud's Origin Gateway system will make a connection to the customer's origin server or Storage to retrieve the requested content from the customer in any format such as js, css, image, tff, etc.&#x20;
  * If the requested content is large in size, the Origin Gateway system will create many small requests of 5MB and pull them to the origin in parallel to increase download speed as well as serve users as soon as the first data (Byte) is available. -range download).&#x20;
  * Data from Origin Gateway will be sent to Edges to serve users.
* Output data:&#x20;
  * Support HTTPS protocol: by default all CDNs created on the system support SSL on the CDN domain. However, customers can upload their own Certificate to use with any name (refer to the certificate management section).&#x20;
  * HTTP/2 support: increases connection speed and data transfer in the browser.

***

#### **Feature** <a href="#objectdownload-tinhnangdichvu" id="objectdownload-tinhnangdichvu"></a>

* Output link security features.&#x20;
* Customize the caching mechanism to suit the content type.&#x20;
* CNAME support for CDNs.&#x20;
* Supports HSTS security feature.&#x20;
* Customize maximum cache time.&#x20;
* Supports "developer" mode (Development Mode).&#x20;
* Origin customization support.&#x20;
* Supports HTTPS option when connecting to Origin.&#x20;
* Supporting direct connection to the origin is Object Storage under the AWS S3 standard.

***

#### **Object download CDN Creation Guide** <a href="#objectdownload-huongdankhoitaoobjectdownloadcdn" id="objectdownload-huongdankhoitaoobjectdownloadcdn"></a>

* **Step 1:** Choose the menu Object Download, select the button **Create New**

<figure><img src="../../.gitbook/assets/image (160).png" alt=""><figcaption></figcaption></figure>

* **Step 2:** Enter the detail information:

<figure><img src="../../.gitbook/assets/image (161).png" alt=""><figcaption></figcaption></figure>

* **Step 3:** Enter CDN name.&#x20;
* **Step 4:** Customize CDN features.&#x20;
* **Step 5:** Depending on the user's request, enter basic rule policy information or advanced rule policy information for CDN.&#x20;
* **Step 6**: When filling in the correct and complete information, press the Submit button at the bottom of the interface and wait about 5 minutes for the system to set the CDN for the user.&#x20;
* **Step 7:** Users can access the CDN via vCDN Domain once the CDN has been created.
