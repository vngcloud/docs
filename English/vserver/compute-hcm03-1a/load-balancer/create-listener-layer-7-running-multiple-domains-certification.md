# Create Listener (Layer 7) running multiple domains, certification

vLB Layer 7 supports the feature **SNI (SERVER NAME INDICATION)** which allows you to configure multiple domains (multiple certifications) on the same vLB.

At the Listener initialization step, in the SSL Certificate check box, select the Certificates you want to use:

For example, here the writer chooses 3 certificates: [cert\_domain1.com](http://cert\_domain1.com/), [cert\_domain2.com](http://cert\_domain2.com/), benchmark\_lb

You can refer to how to create vLB, Listener and upload certificate here [Initialize Load Balancer Layer 7](initialize-load-balancer-layer-7.md), [Upload Certificates](upload-certificates.md)

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59802770/image2021-10-27_12-36-5.png?version=1&#x26;modificationDate=1685086455000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


\* Note: The Default Certificate that Load Balancer returns (For example, in case the client accesses the served domain, but does not yet exist an SSL Certificate at the Load Balancer's Listener) will be the first SSL Certificate in the selected list, specifically. in this example is:  [cert\_domain1.com](http://cert\_domain1.com/).

The rest of the steps, you still follow the instructions [Initialize Load Balancer Layer 7](initialize-load-balancer-layer-7.md)

After successful initialization, you will have a Listener with the following information:

Select Load Balancer and switch to Listener section, check the Certificates have been uploaded

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802770/image2021-10-27_12-42-28.png?version=1&#x26;modificationDate=1685086455000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
To receive all of the above domains, on your member Server you also need to configure the above domains to serve requests.

In this example, the writer uses Apache. On the apache server, you  create 2 virtual hosts with the server names  [www.server1.com](http://www.server1.com/) and  [www.server2.com](http://www.server2.com/)  as follows.

Server1

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802770/image2021-10-27_12-45-21.png?version=1&#x26;modificationDate=1685086456000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Server2:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802770/image2021-10-27_12-45-43.png?version=1&#x26;modificationDate=1685086456000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


After adding and reloading the apache configuration. We proceed to check the Load Balancer results and return the correct certificate corresponding to the domain that the user accesses or not.

_**Note:** The certificate used in the article is a self-signed certificate, so when accessing it in a web browser, it will report that the certificate is not secure._

Visit  [www.server1.com](http://www.server1.com/), member's certificate and Private IP information returned correctly

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802770/image2021-10-27_12-47-14.png?version=1&#x26;modificationDate=1685086456000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Go to [www.server2.com](http://www.server2.com/), member's certificate and Private IP information returned correctly

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802770/image2021-10-27_12-47-50.png?version=1&#x26;modificationDate=1685086456000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
