# vCDN

### \[vCDN] How do I create a CDN?

Please refer to the documentation at the following link for instructions: <mark style="color:blue;">Setup Guide</mark>

### \[vCDN] How is CDN/Live-Stream billed? Will the CDN be disabled immediately when the Volume is depleted?

You purchase CDN volume for usage. If the domain's volume is depleted, it will be disabled, and the remaining volume information is displayed in CDN Remain.

### \[vCDN] How can I use livestreaming?

Please refer to the documentation at the following link for <mark style="color:blue;">here</mark> instructions:

### \[vCDN] Can I view the traffic using my CDN?

Currently, VNGCloud provides charts for each domain to view the traffic in use. Click on each domain for details.

### \[vCDN] How do I clear cache on the CDN?

On the portal, there is a cache purge button for each domain. You can use it to clear the cache on the CDN.

### \[vCDN] How do I delete a CDN domain?

Currently, GreenNode does not support deleting CDN domains. You can only edit them.

### \[vCDN] I want to know the IP range corresponding to 2 domains (bskjv7x1zq.vcdn.com.vn and ggkiz9mkp.vcdn.com.vn)

VNGCloud's CDN system includes multiple IP ranges to ensure readiness and redundancy across different regions to serve the CDN. Therefore, there is no specific IP range for individual CDN domains.

### \[vCDN] How is \[CDN/Live-Stream] billed? Will the CDN be \[disabled] immediately when the \[Volume] is depleted?

Users purchase CDN volume for usage. If the domain's volume is depleted, it will be disabled, and the remaining volume information is displayed in CDN Remain.

### \[vCDN] Can I view the traffic using my \[CDN]?

Currently, GreenNode provides charts for each domain to view the traffic in use. Click on each domain for details <mark style="color:blue;">here</mark>.

### \[vCDN] How do I \[clear cache] on \[CDN]?

On the portal, there is a cache purge button for each domain. You can use it to clear the cache on the CDN.

### \[vCDN] How do I delete a CDN domain?

Currently, GreenNode does not support deleting CDN domains. If you do not want to use a domain, you can disable it.

### \[vCDN] Guide me on using SSL

Currently, GreenNode supports selecting SSL certificates:\
\- Default CDN certificate (\*.[vcdn.com.vn](http://vcdn.com.vn/)): You can use GreenNode's certificate.\
\- Custom SSL certificate: You can upload your own certificate and key to use. SSL certificates can be obtained from websites or places where customers purchase domains.\
You can also check if your cert and key are correct at the following link:\
[https://www.sslchecker.com/matcher](https://www.sslchecker.com/matcher)&#x20;

### \[vCDN] "I need support to provide GreenNode's CDN IP range

Here is a list of GreenNode's CDN IP ranges: 113.164.15.32/28 113.164.15.80/29; 113.164.241.176/28 113.164.14.192/27 171.244.128.0/27 171.244.16.224/27 42.115.221.64/27 43.239.149.128/28 118.69.83.64/27 118.69.83.160/28 118.69.84.64/28 210.245.38.64/27 210.245.26.0/24 42.115.221.128/27 14.225.2.32/28 14.225.10.64/28 171.244.28.64/27 61.28.226.48/28 14.225.10.64/28 171.244.28.64/27 61.28.231.126/32

### \[vCDN] How to change the parameters of the CDN manifest file

Currently, GreenNode supports changing the parameters of the CDN manifest file.

### \[vCDN] I use vCDN to upload VOD to the web, but I get a 404 error

Please check the source of the Video, this is a not found error. It's possible that you have uploaded the wrong key or source.

### \[vCDN] Does vCDN support an API for uploading files to CDN similar to AWS S3?

You can refer to the vStorage service to use in conjunction with vCDN, similar to AWS S3.

### \[vCDN] "I have just finished installing an SSL certificate on my server. How do I check the expiration date of the SSL and other information? "

You can check on one of the following websites:

Digicert: [http://www.digicert.com/help/](http://www.digicert.com/help/)\
Thawte: [https://search.thawte.com/support/ssl-digital-certificates/index?page=content\&id=SO9555](https://search.thawte.com/support/ssl-digital-certificates/index?page=content\&id=SO9555)\
Verisign: [https://knowledge.verisign.com/support/ssl-certificates-support/index?page=content\&id=AR1130](https://knowledge.verisign.com/support/ssl-certificates-support/index?page=content\&id=AR1130)\
RapidSSL: [https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content\&id=SO9556](https://knowledge.rapidssl.com/support/ssl-certificate-support/index?page=content\&id=SO9556)\
GeoTrust: [https://knowledge.geotrust.com/support/knowledge-base/index?page=content\&id=SO9557](https://knowledge.geotrust.com/support/knowledge-base/index?page=content\&id=SO9557)

### \[vCDN] Do I need to pay any fees for using the CDN trial?

When registering for a GreenNode account and using the trial, you get 100GB free to use with the CDN, and there will be no additional fees. Please note that trial accounts can only create one CDN domain.

### \[vCDN] I am using a trial CDN account, and my remaind is 5000GB. When I turn off the trial, will my CDN remaind be lost?

When turning off the trial, your CDN remain will remain unchanged. Only the 100GB of CDN given at the initial usage will be lost.

### \[vCDN] Why can I only create 1 CDN domain?

Please check if your portal is in trial mode. If it is in trial, GreenNode only supports creating one CDN domain.

### \[vCDN] Why did I configure the CDN but get a 502 error when running on the web?

Please check the original link and the CDN link. If both links are the same, the CDN returns correctly; otherwise, please check if you have cleared the cache. If you encounter a 502 error, please allow the IP range: : 113.164.15.32/28 113.164.15.80/29; 113.164.241.176/28 113.164.14.192/27 171.244.128.0/27 171.244.16.224/27 42.115.221.64/27 43.239.149.128/28 118.69.83.64/27 118.69.83.160/28 118.69.84.64/28 210.245.38.64/27 210.245.26.0/24 42.115.221.128/27 14.225.2.32/28 14.225.10.64/28 171.244.28.64/27 61.28.226.48/28 14.225.10.64/28 171.244.28.64/27 61.28.231.126/32 After allowing, check the CDN link again to see if it has been enabled.
