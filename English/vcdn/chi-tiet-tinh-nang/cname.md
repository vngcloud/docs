# CNAME

## Overview <a href="#cname-tongquan" id="cname-tongquan"></a>

CNAME in CDN is a type of DNS (Domain Name System) record used to **route traffic from your domain to the CDN server** .

***

## **How it works** <a href="#cach-hoat-dong" id="cach-hoat-dong"></a>

* **Step 1:** When a user visits your domain name, their browser sends a request to the DNS server.
* **Step 2:** The DNS server will look for a CNAME record for your domain name.
* **Step 3:** If the CNAME record exists, the DNS server will return the IP address of the CDN server.
* **Step 4:** The user's browser will send a request to the CDN server.
* **Step 5:** The CDN server will return the requested content to the browser.

***

## **Benefits of Using CNAME** <a href="#loi-ich-cua-viec-su-dung-cname" id="loi-ich-cua-viec-su-dung-cname"></a>

* **Improved performance:** CDNs store your content on multiple servers around the world. When users access your content, they are connected to the closest server, improving page load speeds.
* **Increased reliability:** CDNs are highly fault tolerant. If one CDN server fails, other servers will continue to deliver your content.
* **Reduce load on your origin server:** CDNs can handle large amounts of traffic, which reduces load on your origin server.

***

## **Create a CDN Name** <a href="#khoi-tao-cdn-name" id="khoi-tao-cdn-name"></a>

To use CNAME in CDN, you can set up CNAMEs in the CDN Name information field in the CDN Info folder when creating any CDN on the vCDN system.

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>
