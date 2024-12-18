# Development Mode

Currently, vCDN supports “Development Mode”. This mechanism will allow all requests to bypass the cache and go directly to the origin to check the data at the origin directly:

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Overview <a href="#tong-quan" id="tong-quan"></a>

vCDN's "Developer" mode is a special feature that allows developers to test, debug, and update website content quickly and efficiently. When this mode is enabled, all requests from users will not be cached by vCDN but will be routed directly to the origin server. This helps ensure that any changes made on the origin server will be reflected immediately on the website, without waiting for the cache to refresh.

**Some notes when using "Developer" mode:**

* **Use in development environment only:** This mode should be used in development or testing environments. This mode should not be enabled in production environments as it may reduce website performance.
* **Turn off mode when done:** Once you are done with development and testing, remember to turn off this mode to take advantage of caching.
* **Performance impact:** Disabling caching can increase load on the origin server, especially when there are many concurrent requests.
* **Not suitable for high traffic websites:** For high traffic websites, disabling cache completely can cause server overload.

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

* On vCDN, to enable/disable Developer mode, you can select **Enable/Disable** in Development mode:

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>
