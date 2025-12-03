# Web Accelerator

**Overview**

Web Accelerator is a solution to speed up content display and user experience.

***

## **Model** <a href="#webaccelerator-cochephanphoidulieu" id="webaccelerator-cochephanphoidulieu"></a>

<figure><img src="../../.gitbook/assets/image (55) (1).png" alt=""><figcaption></figcaption></figure>

***

## **Data Distribution Mechanism** <a href="#webaccelerator-cochephanphoidulieu-1" id="webaccelerator-cochephanphoidulieu-1"></a>

The Web Accelerator service caches all objects that pass through it, including not only static content such as images, javascript, css, but also HTML code and API. It also performs automatic optimization mechanisms for source code and images.

***

## **Service Features** <a href="#webaccelerator-tinhnangdichvu" id="webaccelerator-tinhnangdichvu"></a>

* **CNAME Support** : Allows you to use custom domain names.
* **Custom Origin Support** : Allows configuration of data origin.
* **Optimize terminal file size** : Reduce file size for faster loading.
* **HSTS Security Mode** : Protects your website from attacks.
* **Customize cache features** : Manage cache on demand.
* **Automatically redirect from HTTP to HTTPS** : Secure redirection.
* **Change HTTP links to HTTPS in source code** : Make sure all links are secure.
* **Edit Created CDN** : Allows to change CDN configuration.

***

## **Instructions for create a Web Accelerator CDN** <a href="#objectdownload-huongdankhoitaoobjectdownloadcdn" id="objectdownload-huongdankhoitaoobjectdownloadcdn"></a>

### **Step 1: Create Web Accelerator** <a href="#buoc-1-tao-web-accelerator" id="buoc-1-tao-web-accelerator"></a>

First, you need to initialize a Web Accelerator following these instructions:

1. Access vCDN Portal at [https://vcdn.vngcloud.vn](https://vcdn.vngcloud.vn/live-entrypoint/list.html)
2. Select **Web Accelerator** , then select **Create new.**
3. Continue to enter/select:

* **CDN Info:**
  * **CDN Name:** Enter the identifier name for the CDN you want to create.

<figure><img src="../../.gitbook/assets/image (56) (1).png" alt=""><figcaption></figcaption></figure>

* **HTTP Origin** : Server supports HTTP protocol.
  * **Fail-Over Error Code:** List of HTTP error codes (e.g. 500, 502, 503, 504) that, if encountered, will trigger a fail-over to another Origin.
  * **Origin Load Balancing:** Load balancing mechanism between designated Origin Servers.
  * **Origin Host Header:** Header used when sending requests from vCDN to Origin Server.
  * **IP Address:** The IP address of the Origin Server (e.g. IPv4 like 1.1.1.1 or IPv6).
  * **Weight:** Defines the priority of each Origin Server when load balancing (the higher the value, the more traffic received).

<figure><img src="../../.gitbook/assets/image (57) (1).png" alt=""><figcaption></figcaption></figure>

* **Crypto:**
  * **HTTPS (HTTP/2)** : Enable or disable HTTPS security for the CDN stream. You can create a new **Certificate** by selecting **Add new** .
  * **HTTP Strict Transport Security (HSTS)** : Enforces a web security policy for your website, sending HSTS headers with all HTTPS requests. If configured incorrectly, HSTS can make your website inaccessible for long periods of time.
  * **Max Age Header (max-age):** Specifies how long HSTS headers are cached in the browser.
  * **Apply HSTS policy to subdomains (includeSubDomains):** Every domain will inherit the same HSTS headers. If any of your domains don't support HTTPS, they won't be accessible.
  * **Preload:** Allows the browser to preload the HSTS configuration automatically. Preloading can make a non-HTTPS-enabled site completely inaccessible.
  * **Relative Canonical URL:** A canonical URL allows you to tell search engines that similar URLs are actually the same content. This is useful when you have a product or content that can be found on multiple URLs or even multiple websites.
  * **No-Sniff Header:** Send the "X-Content-Type-Options: nosniff" header to prevent Internet Explorer and Google Chrome from checking MIME types other than the declared Content-Type.

<figure><img src="../../.gitbook/assets/image (58) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (59) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Caching:**
  * **Caching Level** : Determines the CDN cache level. With VOD, vCDN is providing 3 cache levels including: URL without query string only, Skip Query String of URL, URL With Query String.
  * **Server Cache Expiration (TTL):** The amount of time that the vCDN system will cache your resources. During this time, the vCDN system will not access the origin server but respond to requests from the vCDN cache. You can choose this time from 30 minutes to 1 year depending on your system's needs.
  * **Browser Cache Expiration:** The time vCDN asks the user's browser to cache files locally.
  * **Development mode:** This feature allows you to temporarily disable caching on the Edge Server to support testing or testing content during development. All requests will be returned directly from Origin, allowing content to be updated immediately without clearing the cache.

<figure><img src="../../.gitbook/assets/image (62) (1).png" alt=""><figcaption></figcaption></figure>

* **File Size Optimization:**
  * **Image Optimizer:** Optimize image size and format, thereby reducing page load time and traffic.
  * **Auto Minify:** Minify HTML, CSS, JS by removing spaces and comments.
  * **Brotli:** A more efficient content compression algorithm than Gzip. Using Brotli compression reduces file transfer size, improves speed, and saves traffic.
*   **Page Rules:** This feature helps customers optimize conditions and options to help the website demonstrate many different purposes. To create Page rules, please select **Create Page Rule** , a popup will appear, now you need to select:

    * **URL pattern:** need to apply pagerule, support declaration type “\*” represents a string of characters. For example: /trang\_landing\_cu.html. After entering URL pattern, select **Add new rule** . Each Rule when satisfying the condition of the requested URI will be able to optionally execute one of the following actions:
      * Always Use HTTPS
      * Auto Minify
      * Automatic HTTPS Rewrites
      * Server Cache TTL
      * Browser Cache TTL
      * Bypass Cache By Cookie
      * Cache By Device Type
      * Bypass Cache By Device Type
      * Forwarding URL
      * Response Header Override
      * Brotli
      * Gzip
      * Resolve Origin Override
      * Origin Base Directory
      * Deny Access
    * Select **Save changes** to save the changes.

    <figure><img src="../../.gitbook/assets/image (63) (1).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../../.gitbook/assets/image (53) (1) (2).png" alt="" width="375"><figcaption></figcaption></figure>

    <figure><img src="../../.gitbook/assets/image (54) (1) (2).png" alt="" width="348"><figcaption></figcaption></figure>

4. Select **Submit** to complete creating the Web Accelerator.

### **Step 2: Check, monitor and supervise** <a href="#buoc-2-kiem-tra-theo-doi-va-giam-sat" id="buoc-2-kiem-tra-theo-doi-va-giam-sat"></a>

Once you have initialized Web Accelerator, you can test and monitor your page load speed via vCDN.
