# Create NAT



{% hint style="danger" %}
**Important**

* _<mark style="color:blue;">NAT and VM going through NAT to the internet must be on the same subnet</mark>_
* _<mark style="color:blue;">The NAT's public interface is created automatically when the NAT is successfully established. Users can configure the public IP addresses into</mark>_ [_<mark style="color:blue;">purchased bandwidth</mark>_](https://docs.vngcloud.vn/vng-cloud-document/vserver/compute-hcm03-1a/vpc/bandwidth/datatransfers-bandwidth-service) _<mark style="color:blue;">packages (if available) to increase the bandwidth for the NAT.</mark>_
* _<mark style="color:blue;">NAT only connects to the internet through ports 53, 80, 443, and ICMP packets. If you need support for other requests, please contact the VNG Cloud hotline.</mark>_
* _<mark style="color:blue;">If DNS resolution is needed, users must ensure that the route above is correctly configured to go through the NAT gateway for the IP resolver.</mark>_
{% endhint %}

* Log in to [https://hcm-3-vnetwork.console.vngcloud.vn/nat/list](https://hcm-3-vnetwork.console.vngcloud.vn/nat/list) with region set to HCM.
* Select the **"Public NAT Instance"** menu from the top-left-hand menu bar.
* Choose the **"Create a Public NAT"** function.
* Enter the required NAT information, including:
  * NAT Name
  * Service Package
  * VPC, Subnet
* Check the service pricing information in the "**Summary**" section.
* Click **"CREATE A PUBLIC NAT"**.

When the NAT is successfully created, it will appear on the NAT list. The user needs to configure which VMs will use NAT by specifying the NAT IP gateway, using the sample syntax for Linux.&#x20;

_`ip route add <internet_ip> via <nat_gateway_ip> dev <interface>`._

In this context:

* `<internet_ip>` is the IP address of the destination on the internet.
* `<nat_gateway_ip>` is the IP address of the NAT gateway.
* `<interface>` is the network interface that will be used for this route.

Below is an example of adding a route on a VM with Linux OS using the syntax above:

&#x20;_`ip route add 0.0.0.0/0 via 10.0.0.100 dev eth0`._

**In case there is already an existing route to the internet through a different gateway IP, the user must remove the current route and add a new route to the NAT gateway IP.**

_<mark style="color:purple;">Here is an example of an internet route that already exists through a different gateway IP on Linux OS</mark>_

<figure><img src="../../.gitbook/assets/image (275).png" alt=""><figcaption></figcaption></figure>

_<mark style="color:purple;">After deleting the existing route on the VM, add the route to the internet through NAT.</mark>_

<figure><img src="../../.gitbook/assets/image (271).png" alt=""><figcaption></figcaption></figure>

_<mark style="color:purple;">The result is successful as shown in the screenshot.</mark>_

<figure><img src="../../.gitbook/assets/image (272).png" alt=""><figcaption></figcaption></figure>



