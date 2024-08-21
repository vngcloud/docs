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

When the NAT is successfully created, you will see it appear on the NAT list. You will need to configure which VMs will route through the NAT to the internet. Here is an example of adding a route on a VM with a Linux OS:

_ip route add 0.0.0.0/0 via 10.0.0.100 dev eth0_

_ip route add \<internet\_ip> via \<nat\_gateway\_ip> dev \<interface>_

_<mark style="color:blue;">**Note:**</mark>_

_<mark style="color:blue;">The public interface of NAT is automatically created when NAT is successfully set up. Users can configure public IP addresses for purchased bandwidth packages (if available) to increase the bandwidth for NAT.</mark>_

