# Automatically Redirect from HTTP to HTTPS

## Overview <a href="#tong-quan" id="tong-quan"></a>

**The Automatic Redirect from HTTP to HTTPS** feature is a security and user experience optimization solution that automatically converts HTTP requests to HTTPS when users connect to a website via the insecure HTTP protocol. This feature ensures that all traffic is encrypted and complies with modern security standards.

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

When you initialize a Web Accelerator, you can configure automatic Redirect from HTTP to HTTPS via:

<figure><img src="../../.gitbook/assets/image (349).png" alt=""><figcaption></figcaption></figure>

In there:

* **Always Use HTTPS:** When this option is enabled, end-users accessing websites with HTTP protocol will be automatically redirected to HTTPS.
* **Automatic HTTPS Rewrites** : Support converting HTTP links to HTTPS in source code **:** The system will automatically identify http sources in source code to convert to HTTPS before transferring data to users. Customers can choose this feature when initializing CDN or when editing created CDN.
* **Minimum TLS Version** : If your website is using HTTP protocol and is in the process of switching to HTTPS, the browser will warn you when the website still contains HTTP links. This option will automatically replace all HTTP links with HTTPS.
