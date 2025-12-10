# HTTP Origin

## Overview <a href="#tong-quan" id="tong-quan"></a>

Currently, vCDN supports HTTP Origin with connection algorithms: **Round Robin, Least Connection, IP Hash and automatic fail-over.**

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

When you create a Web Accelerator, Object Download, or Video On Demand, the CDN initialization screen will include the following information:

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

In there:

* **Fail-Over Error Code:** List of HTTP error codes (eg: 500, 502, 503, 504), based on these error codes the system will recognize and coordinate customers through other Origin Servers in the pool.
* **Origin Load Balancing:** Load balancing mechanism between designated Origin Servers. Specifically:
  * **Round Robin** : The system will automatically coordinate traffic to the customer's Origin Server using a round-robin method - evenly between servers.
  * **Least Connected:** The system will choose the Origin Server with the lowest number of connections to route traffic down.
  * **IP Hashing:** The system will rely on the Client IP to coordinate and maintain the connection to the Origin Server.
* **Origin Host Header:** Header used when sending requests from vCDN to Origin Server.
* **IP Address:** The IP address of the Origin Server (e.g. IPv4 like 1.1.1.1 or IPv6).
* **Weight:** The priority (weight) of the Origin Server, enter “0” to set this Origin Server in Backup/Standy mode, the higher the number, the higher the priority.

After entering the Server Origin information and selecting **Add Server** , the screen will display a list of Server Origin IP addresses and information as shown below:

_\* When the customer enters the main domain information, the system will automatically add the Origin Servers based on the available DNS records of the domain name into the number box as shown below._

<figure><img src="../../../.gitbook/assets/image (183) (1).png" alt=""><figcaption></figcaption></figure>

In there:

* **Priority** – represents the priority level (weight) of the Origin Server, the higher the number, the higher the priority.
* **Value** : IPv4 address of Origin Servers.
* **Algorithms** : Algorithms for distributing traffic to Origin Servers.
* **Status** : Shows the status ![](<../../../.gitbook/assets/image (6) (1) (1) (1) (1).png>) (**Active** ) and ![](<../../../.gitbook/assets/image (185) (1).png>)(**Disabled** )
  * **Active** : Origin Server will be added to Pool Origin Servers.
  * **Disabled** : The Origin Server will be removed from the Origin Servers Pool.
* Support configuring error codes for the system to automatically perform Fail-Over.
* **Origin:** allows customers to specify error code types when running in Fail-Over mode.
