# Security Link

## **Secure Token** <a href="#securitylink-securetoken" id="securitylink-securetoken"></a>

Secure tokens are structured codes that protect content from being stolen and distributed elsewhere. On vCDN, we support you to enable the Secure token feature when creating or editing a previously created CDN.

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

***

## Operational diagram <a href="#securitylink-sodohoatdong" id="securitylink-sodohoatdong"></a>

When the end user needs to access the content that has been set to activate the "Secure token", the system will check the request to see if it satisfies the formula or not. If it satisfies, the end user can get the content. If not, the request will be rejected.

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

In there:

* **Passphase** : is the key that comes with the formula you have set up so that the system can recognize that access has been granted.
* **Include client IP** : is the IP of the end user requesting content.
* For "Secure token" to work, the service administrator needs to integrate KEY into the system. Depending on the Token Type, there will be different KEY generation formulas, specifically:
  * **VNG** :
    * **URL Format** : http(s)://\<domain>/\<token>/\<expiredTime>/\<uri>
    * **\<token>** : md5(\<Passphare>\<filePath>\<expiredTime>\<clientIP>)
    * **\<expiredTime>:** The URL's expiration epochtime, in milliseconds
    * **\<filePath>** : /path/to/media/xxx.\[m3u8|ts|mpd|dash] (ie \<uri> leaves out the xxx.\[m3u8|ts|mpd|dash] part, in this example it would be: /path/to/media)
    * **\<ClientIP>** : The IP of the client that is authorized to access the content, provided only in case you have selected to enable "Include IP" in the CDN service configuration
    * Example: [http://abcxyz.vcdn.cloud/cb0a229fa7a81c219c0c0f964f9b6e68/1603691495000/test/index.m3u8](http://abcxyz.vcdn.cloud/cb0a229fa7a81c219c0c0f964f9b6e68/1603691495000/test/index.m3u8)
  * **SBD** :
    * **URL Format** : http(s)://\<domain>/\<token>/\<expiredTime>/\<uri>
    * **\<token>** : md5(\<clientIP> **:<** Passphare> **:** \<exiredTime> **:** \<filePath>)
    * **\<expiredTime>** : The URL's expiration epochtime, in seconds
    * **\<filePath>:/path/to/media** /xxx.\[m3u8|ts|mpd|dash] (ie \<uri> leaves out the xxx.\[m3u8|ts|mpd|dash], in this example it would be: /path/to/media)
    * **\<ClientIP>** : The IP of the client that is authorized to access the content, provided only in case you have selected to enable "Include IP" in the CDN service configuration
  * **Akamai** :
    * Refer to the instructions from Akamai's document at: [https://learn.akamai.com/en-us/webhelp/adaptive-media-delivery/adaptive-media-delivery-implementation-guide/GUID-041AEFDE-7E25-4AD8-B6C4-73F1B7200F02.html](https://learn.akamai.com/en-us/webhelp/adaptive-media-delivery/adaptive-media-delivery-implementation-guide/GUID-041AEFDE-7E25-4AD8-B6C4-73F1B7200F02.html)

***

## **Using CORS feature** <a href="#securitylink-sudungtinhnangcors" id="securitylink-sudungtinhnangcors"></a>

CORS is a vCDN output security feature that allows access with configurations such as: domain name, IP address, Header, Method, Expose Header to access the vCDN output Link.

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

***

## **Create a Whitelist / Blacklist IP** <a href="#securitylink-khoitaowhitelist-blacklistip" id="securitylink-khoitaowhitelist-blacklistip"></a>

* **WhiteList IP:** You can add IP lists of Origins that are allowed to access the output link by selecting **Allow** and entering **the IP Address** or **CIDR** you want:

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

* **BlackList IP:** In addition, you can also block IPs that do not allow Origin to access the output link of vCDN:

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

***

## **Geo Block** <a href="#securitylink-geoblock" id="securitylink-geoblock"></a>

* Additionally, you can create a list of origins in which countries the output link can be accessed by selecting **Allow** and entering the desired **country code :**

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

* You can also set to not allow Origins in a certain country to access the output link by selecting **Block** and entering the desired **country code :**

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

***

## **HTTP Referer Block** <a href="#securitylink-httprefererblock" id="securitylink-httprefererblock"></a>

* You can allow Origins with domains in the list to access the output link by selecting **Allow** and entering the desired **domain :**

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

* Finally, you can disallow Origin to have domains in the list that can access the output link by selecting **Block** and entering the desired **domain :**

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>
