# Create NAT

* Log in to [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/) with region set to HCM.
* Select the **"Public NAT Instance"** menu from the top-left-hand menu bar.
* Choose the **"Create a Public NAT"** function.
* Enter the required NAT information, including:
  * NAT Name
  * Service Package
  * VPC, Subnet
* Check the service pricing information in the "**Summary**" section.
* Click **"CREATE A PUBLIC NAT"**.

When the NAT is successfully created, you will see it appear on the NAT list. The user needs to configure which VMs will go through NAT by using the NAT IP gateway with the syntax _`ip route add <internet_ip> via <nat_gateway_ip> dev <interface>`._

In this context:

* `<internet_ip>` is the IP address of the destination on the internet.
* `<nat_gateway_ip>` is the IP address of the NAT gateway.
* `<interface>` is the network interface that will be used for this route.

Below is an example of adding a route on a VM with Linux OS using the syntax above: _`ip route add 0.0.0.0/0 via 10.0.0.100 dev eth0`._

If the route file already contains the route that is being added, the user must remove the existing route from the file in order to add the route to NAT.

_<mark style="color:blue;">**Note:**</mark>_

* _<mark style="color:blue;">The NAT's public interface is created automatically when the NAT is successfully established. Users can configure the public IP addresses into</mark>_ [_<mark style="color:blue;">purchased bandwidth</mark>_](https://docs.vngcloud.vn/vng-cloud-document/vserver/compute-hcm03-1a/vpc/bandwidth/datatransfers-bandwidth-service) _<mark style="color:blue;">packages (if available) to increase the bandwidth for the NAT.</mark>_
* _<mark style="color:blue;">The NAT only connects to the internet through ports 80 and 443.</mark>_

