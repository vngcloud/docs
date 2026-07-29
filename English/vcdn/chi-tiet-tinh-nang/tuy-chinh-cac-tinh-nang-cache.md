# Caching

## Overview <a href="#tong-quan" id="tong-quan"></a>

**Caching** is a core function of the vCDN system, which helps speed up content access by temporarily storing copies of data (such as static files, images, videos, or API data) on edge servers closer to the end user. This not only reduces page load times but also reduces the load on the origin server.

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

Currently, vCDN supports customizing cache features **:** allowing customers to customize cache metrics on the system and on the browser. Specifically:

<figure><img src="../../.gitbook/assets/image (348).png" alt=""><figcaption></figcaption></figure>

In there:

* **Caching Level** : Determines the CDN cache level. With VOD, vCDN is providing 3 cache levels including: URL without query string only, Skip Query String of URL, URL With Query String.
  * URL Without Query String Only: Do not cache if there is a URL Param in the request.
  * Skip Query String of URL: Skip URL Param when creating Cache.
  * URL With Query String: Cache the entire URL including URL Param.
* **Server Cache Expiration (TTL):** The amount of time that the vCDN system will cache your resources. During this time, the vCDN system will not access the origin server but respond to requests from the vCDN cache. You can choose this time from 30 minutes to 1 year depending on your system's needs.
* **Browser Cache Expiration:** The time vCDN asks the user's browser to cache files locally.
* **Development mode:** This feature allows you to temporarily disable caching on the Edge Server to support testing or testing content during development. All requests will be returned directly from Origin, allowing content to be updated immediately without clearing the cache.
