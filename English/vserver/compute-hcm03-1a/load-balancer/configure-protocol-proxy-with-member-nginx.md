# Configure Protocol Proxy with member Nginx

Protocol Proxy is a specific protocol that allows Load Balanacer to forward end-user connection information (client connection information) to Member servers. From there, Member Servers will have information to configure advanced features such as Rate-limit by IP, GeoIP, client log access statistics, etc. To use Protocol Proxy, you need to create vLB Layer 4 with Pool Settings is Proxy Protocol, and your Member Server must support this Proxy Protocol. Some popular Web Servers that support Proxy Protocol are Nginx, Apache, etc. This tutorial will use Nginx.

**Step 1:** You create a Pool with Setting as Proxy Protocol:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802739/image2021-10-27_11-59-17.png?version=1&#x26;modificationDate=1685082015000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


**Step 2:** On Nginx server, check if the proxy protocol module http\_relip\_module  has been installed before using command. If not, you need to install or rebuild nginx from source with the above module.

| `nginx -V 2>&1` `\| grep -- 'http_realip_module'` |
| ------------------------------------------------- |

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802739/image2021-10-27_11-46-47.png?version=1&#x26;modificationDate=1685082015000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\* **Note:** This module will be pre-installed from version **Ubuntu Bionic Beaver (18.04).**

**Step 3**: Configure to enable Proxy Protocol at Virtual Host:

\+ Configure additional parameters **proxy\_protocol** at **server {}** block:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802739/image2021-10-27_11-48-12.png?version=1&#x26;modificationDate=1685082016000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



\+ Determine the Load Balancer IP where you receive Proxy Protocol traffic at the **server {}** block with the configuration **set\_real\_ip\_from**

| `set_real_ip_from <Load balancer IP>;` |
| -------------------------------------- |



For example, here the vLB's IP is 103.245.248.204.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802739/image2021-10-27_11-49-14.png?version=1&#x26;modificationDate=1685082016000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


\+ Configure to change the IP of the Load balancer with the IP of the client, taken from the Proxy Protocol Header at the  **server {}** block with the configuration **real\_ip\_header** and the parameter **proxy\_protocol**

| `real_ip_header proxy_protocol;` |
| -------------------------------- |



<figure><img src="https://docs.vngcloud.vn/download/attachments/59802739/image2021-10-27_11-50-39.png?version=1&#x26;modificationDate=1685082016000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



**Step 4**: Configure Header to get log output value at **http {}** block with configuration **proxy\_set\_header**

| <p><code>proxy_set_header X-Real-IP       $proxy_protocol_addr;</code><br><code>proxy_set_header X-Forwarded-For $proxy_protocol_addr;</code></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------- |



<figure><img src="https://docs.vngcloud.vn/download/attachments/59802739/image2021-10-27_11-51-10.png?version=1&#x26;modificationDate=1685082016000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



**Step 5**: Configure Custom log with Client IP value (Optional if you need to export nginx log with log client ip).

Define custom log\_format with Client IP

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802739/image2021-10-27_11-52-12.png?version=1&#x26;modificationDate=1685082016000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Add in block server{} access\_log with log\_format as custom on.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802739/image2021-10-27_11-52-47.png?version=1&#x26;modificationDate=1685082016000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



**Step 6**: Test configuration and restart nginx to finish by command

| `nginx -t` |
| ---------- |

If there is no error, please restart nginx.

| `systemctl restart nginx` |
| ------------------------- |



**Step 7**: Make a request and check the log out to see the IP Client appear in the log file:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802739/image2021-10-27_11-55-33.png?version=1&#x26;modificationDate=1685082016000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
