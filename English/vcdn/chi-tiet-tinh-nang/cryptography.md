# Cryptography

## Overview <a href="#tong-quan" id="tong-quan"></a>

**Crypto** in CDN is a group of settings and tools that help manage encryption and security features related to websites.

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

When initializing a Web Accelerator on the vCDN system, in the Crypto section, you need to select/enter:

<figure><img src="../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

In there:

* **HTTPS (HTTP/2)** : Enable or disable HTTPS security for the CDN stream. You can create a new **Certificate** by selecting **Add new** .
* **HTTP Strict Transport Security (HSTS)** : tells the user's browser that they can only connect to the Web server via the HTTPS protocol. This can be used to prevent some attacks that downgrade connections from HTTPS to HTTP. Enable this feature to protect visitors to your customer's website.
* **Max Age Header (max-age):** Specifies how long HSTS headers are cached in the browser.
* **Apply HSTS policy to subdomains (includeSubDomains):** Every domain will inherit the same HSTS headers. If any of your domains don't support HTTPS, they won't be accessible.
* **Preload:** Allows the browser to preload the HSTS configuration automatically. Preloading can make a non-HTTPS-enabled site completely inaccessible.
* **Relative Canonical URL:** A canonical URL allows you to tell search engines that similar URLs are actually the same content. This is useful when you have a product or content that can be found on multiple URLs or even multiple websites.
* **No-Sniff Header:** Send the "X-Content-Type-Options: nosniff" header to prevent Internet Explorer and Google Chrome from checking MIME types other than the declared Content-Type.
