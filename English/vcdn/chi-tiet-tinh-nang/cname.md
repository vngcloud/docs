# CNAME

#### Overview <a href="#cname-tongquan" id="cname-tongquan"></a>

A CNAME in CDN is a type of DNS record used to **redirect traffic from your domain to the CDN server**

***

**Model**

1. When a user visits your domain name, their browser sends a request to the DNS server.&#x20;
2. The DNS server will look for the CNAME record for your domain name.&#x20;
3. If a CNAME record exists, the DNS server returns the IP address of the CDN server.&#x20;
4. The user's browser sends the request to the CDN server.&#x20;
5. The CDN server will return the requested content to the browser.

***

**Benefits of using CNAME in CDN**&#x20;

* **Improved performance**: CDN stores your content on multiple servers worldwide. When users access your content, they will be connected to the nearest server, improving page loading speed.&#x20;
* **Increased reliability**: CDNs are highly fault-tolerant. If one CDN server goes down, the others will continue to serve your content.&#x20;
* **Reduce the load on your origin servers**: CDNs can handle large amounts of traffic, helping to reduce the load on your origin servers.

***

**Create a CDN Name**

To use CNAMEs in CDN, you can set up CNAMEs in the CDN Name information field on the CDN Info folder when creating any CDN on the vCDN system.

<figure><img src="../../.gitbook/assets/image (178).png" alt=""><figcaption></figcaption></figure>
