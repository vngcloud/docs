# Pricing

## Overview <a href="#tong-quan" id="tong-quan"></a>

**The vCDN** system supports both types of users:

1. **Prepaid users** : Customers purchase **Traffic** capacity in advance and use it according to the purchased amount.
2. **Postpaid users** : Customers use the service in advance and pay based on consumption at the end of the period.

***

## Traffic Package <a href="#huongdanmuahang-goitangtocwebsite" id="huongdanmuahang-goitangtocwebsite"></a>

### **Prepaid users** <a href="#nguoi-dung-tra-truoc" id="nguoi-dung-tra-truoc"></a>

When purchasing **Traffic** , you can choose:

* **Group Type** : Select package usage period ( **3 months, 6 months or 12 months** ).
* **Traffic Type** : Traffic Type:
  * **Domestic** : Domestic traffic.
  * **International** : International traffic.
* **Package Traffic** : Desired **Traffic** capacity .

{% hint style="info" %}
**Note:**

* If you select **Traffic type = Domestic** , up to **20% of traffic** can be used for **international** .
  * For example: Domestic package 50000GB → 10000GB is allowed for International.
* **When you use up all the Traffic** :
  * **Domestic : Extra Domestic** can be purchased , duration depends on the duration of the main package.
  * **International : Extra International** can be purchased with the same duration.
* If you select **Traffic type = International** , this traffic can be used for both **Domestic and International.**
* Each account can only apply **1 main package at a time but can buy many extra packages.**
* The system supports **traffic aggregation** if you change packages.
{% endhint %}

### **Postpaid users** <a href="#nguoi-dung-tra-sau" id="nguoi-dung-tra-sau"></a>

* The system will count **monthly traffic consumption** and calculate payment costs at the end of the month.

## **Accelerator Package** <a href="#huongdanmuahang-goitangtocwebsite-1" id="huongdanmuahang-goitangtocwebsite-1"></a>

Customers can purchase packages according to features such as:

* **Basic** , **Standard** , **Pro** , and **Enterprise** .
* These packages apply to **Web Accelerator** service only .

**LIST OF WEB ACCELERATOR FEATURES**

<table data-header-hidden data-full-width="true"><thead><tr><th></th><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Features</strong></td><td><strong>Describe</strong></td><td><strong>Basic</strong></td><td><strong>Standard</strong></td><td><strong>Pro</strong></td><td><strong>Enterprise</strong></td></tr><tr><td>Enable HTTP2</td><td>Enable/disable HTTP/2 support</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr><tr><td>CDN</td><td>Number of CDNs that can be created</td><td>1</td><td>3</td><td>5</td><td>20</td></tr><tr><td>Multi CNAME</td><td>Support customers to fill in multiple domains to use services on each CDN</td><td></td><td>3</td><td>5</td><td>10</td></tr><tr><td>SSL Certificate</td><td>Support customers to upload SSL to use the service</td><td>50</td><td>50</td><td>50</td><td>50</td></tr><tr><td>Image Optimization</td><td><p>Automatically optimize images on customer websites:</p><p>- If the image quality is high, it will automatically reduce to 1080p or equal to the vertical size of the device screen (&#x3C;1080);</p><p>- Image quality: Automatically compresses images to 60% for PC, 50% for Tablet and 30% for mobile;</p><p>**With browsers that support WebP image format => Automatically convert images to WebP to reduce capacity and increase page loading speed.</p></td><td></td><td></td><td>Supported</td><td>Supported</td></tr><tr><td>Auto zoom out</td><td>Automatically optimize Javascript, CSS, HTMl segments on customer's website.</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr><tr><td>Load Balancing</td><td>Support LB Origin Servers in the pool to distribute requests reasonably, supported LB Algorithms: Weight RoundRobin, Least Connected, IP Hashing.</td><td></td><td>3 (ips)</td><td>5 (ips)</td><td>50 (ips)</td></tr><tr><td>HSTS Support</td><td>HSTS Support</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr><tr><td>HTTPS Support</td><td>Automatically rewrite homepage from http -> https</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr><tr><td>Automatic HTTPS Rewrites</td><td>Support rewriting http urls to https automatically in page content</td><td></td><td>Supported</td><td>Supported</td><td>Supported</td></tr><tr><td>TLS 1.3: Support TLS Version 1.3</td><td>Support for selecting the lowest TLS version that can be supported</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr><tr><td>Brotli Compression</td><td>Page compression option reduces size for supported devices</td><td></td><td>Supported</td><td>Supported</td><td>Supported</td></tr><tr><td>Cache</td><td>Option to cache response results from origin</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr><tr><td>Development Mode</td><td>Enable no-cache mode across services</td><td></td><td>Supported</td><td>Supported</td><td>Supported</td></tr><tr><td>Cache Browser</td><td>Browser Cache Time</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr><tr><td>Cache Edge TTL</td><td>Cache Time on Edge</td><td>>3 days</td><td>>1 day</td><td>>12 rolls</td><td>>30 minutes</td></tr><tr><td>Purge Cache</td><td>Tool to help delete cached content on CDN system</td><td>5 times/day</td><td>20 times/day</td><td>50 times/day</td><td>1000 times/day</td></tr><tr><td>Page Rules</td><td>Page rule options to adjust cache, quality, size, image format</td><td>1 rule</td><td>3 rules</td><td>5 rules</td><td>100 rules</td></tr><tr><td>Statistical</td><td>Statistical report</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr></tbody></table>

## **Steps to follow** <a href="#cac-buoc-thuc-hien" id="cac-buoc-thuc-hien"></a>

Instructions for purchasing and using Traffic on vCDN Portal

**Step 1** : Access vCDN Portal at [https://vcdn.vngcloud.vn](https://vcdn.vngcloud.vn/) .

**Step 2** : Select **Package** or **Buy More Traffic . The vCDN Billing** screen will appear.

<figure><img src="../.gitbook/assets/image (379).png" alt=""><figcaption></figcaption></figure>

**Step 3** : Select **the Accelerator Package** and **Period** you want. Click **Confirm** to continue.

<figure><img src="../.gitbook/assets/image (380).png" alt=""><figcaption></figcaption></figure>

**Step 4** : Continue to perform according to the conditions:

* **For prepaid customers** : select usage time and desired **Traffic Package**
* **For postpaid customers** : no need to choose Traffic package, can use immediately and pay at the end of the month.
* After selecting a package (if any), click **Confirm** .

<figure><img src="../.gitbook/assets/image (381).png" alt=""><figcaption></figcaption></figure>

**Step 5** : In **Payment Details** , check the selected service packages again. If the information is correct, select **Payment Confirm** to complete.

<figure><img src="../.gitbook/assets/image (382).png" alt=""><figcaption></figcaption></figure>

**Step 6 : At the Payment Confirm** screen , select **Continue** . Follow the payment instructions.

<figure><img src="../.gitbook/assets/image (383).png" alt=""><figcaption></figcaption></figure>

**Step 7:** Once completed, you can check your payment and consumption information in **Pay/Consume History** .
