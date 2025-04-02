# Cache Time

## **Overview** <a href="#tong-quan" id="tong-quan"></a>

* **Server Cache Expiration (TTL)** is an important mechanism used to determine how long vCDN will cache your resources. During this time, vCDN will not access your origin server and respond with results from the vCDN cache. The benefits of using Server Cache Expiration include:
  * Improve performance
  * Reduce bandwidth usage
  * Enhance user experience.
* **Browser Cache Expiration** is the time vCDN instructs a visitor's browser to cache files. During this time, the browser loads files from the local cache, speeding up page loads.

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

* **Server Cache Expiration (TTL):** On vCDN, you can set Server Cache Expiration (TTL) from a minimum value of 30 minutes to a maximum value of 1 year that we support.

<figure><img src="../../.gitbook/assets/image (39) (1).png" alt=""><figcaption></figcaption></figure>

* **Browser Cache Expiration:** On vCDN, you can set Browser Cache Expiration from a minimum value of 30 minutes to a maximum value of 1 year that we support.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
