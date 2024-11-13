---
description: >-
  VPN Site to Site is a private connection to communicate between  two or more
  private network through a secure connection and safety.
---

# VPN Connect Condition

Between 2 sites, to create a valid VPN Connection, need to satisfy the below conditions. If not system will throw an error.

### **Condition:**

<table><thead><tr><th width="88">STT</th><th width="316">Condition</th><th>Error</th></tr></thead><tbody><tr><td>1</td><td>Able to create a VPN if private CIDR 2 sites are different - not covert CIDR each other</td><td><p>(code 2017) </p><p>Overlapping CIDR in two sites</p></td></tr><tr><td>2</td><td>Able to create a Connection if Remote Private CIDR does not overlap with other Site private CIDR Networks that created before (case multi tunnel)</td><td>(code 2023)<br>The newly created RemoteSite Subnet overlaps with a previously created RemoteSite Subnet.:</td></tr><tr><td>3</td><td>The Pre-Shared Key must not be empty if the user selects the <em>checkbox</em> <em><strong>"Used Your Pre-shared Key"</strong></em></td><td>(code 2022)<br>PSK cannot be empty</td></tr><tr><td>4</td><td>Private CIDR of the remote site must be in a valid format and must be a private network</td><td>(mã 2018, 2019)<br>Remote VPN CIDR must be CIDR Private</td></tr><tr><td>5</td><td>IP Gateway of the site Remote  must be public and correct format</td><td>(mã 2020, 2021)<br>Remote VPN Gateway IP must be IP Public.</td></tr></tbody></table>

## **Example**

### <mark style="color:blue;">**\[**</mark><mark style="color:blue;">Code 2017</mark><mark style="color:blue;">**]**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">Overlapping CIDR in two sites</mark>

<figure><img src="../../.gitbook/assets/image (304).png" alt=""><figcaption></figcaption></figure>

Not be able to create VPN connect above picture

* On Site HCM03 has CIDR of VPC1 is 10.1.0.0/16.
* On Site HAN01 has CIDR of VPC1 là 10.1.0.0/16.
* 2 CIDR of HCM03 and HAN01 are conflict each other.

_-> Cannot create VPN connection_

### <mark style="color:blue;">**\[Code**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">2023</mark><mark style="color:blue;">**]**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">The newly created RemoteSite Subnet overlaps with a previously created RemoteSite Subnet.:</mark>

<figure><img src="../../.gitbook/assets/image (305).png" alt=""><figcaption></figcaption></figure>

Example

* At Site HCM03 has CIDR of VPC1 is 10.1.0.0/16.
* At Site HAN01 has CIDR of VPC1 is 172.16.0.0/16.
* At site On Premise has CIDR is 172.16.0.0/16.
* A  Site-to-Site VPN was created from Site HCM03 to HAN01.

_-> Cannot create Site-to-Site VPN between HCM03 and site On-Premise cause CIDR On-Premise is overlapping with HAN01 172.16.0.0/16._
