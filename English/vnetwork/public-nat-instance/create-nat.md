# Create NAT

* Log in to [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/) with region set to HCM.
* Select the **"Public NAT Instance"** menu from the top-left-hand menu bar.
* Choose the **"Create a Public NAT"** function.
* Enter the required NAT information, including:
  * NAT Name
  * Instance Type (Flavor)
  * Volume attachment (if any)
  * VPC, Subnet
  * External Interface
* Check the service pricing information in the "**Summary**" section.
* Click **"CREATE A PUBLIC NAT"**.

When the NAT is successfully created, you will see it appear on the NAT list. You will need to configure which VMs will route through the NAT to the internet as instructed on the NAT detail.

_<mark style="color:blue;">**Note:**</mark>_

* _<mark style="color:blue;">You can go to the Server list on the "Server" page to perform support functions for the server on the NAT.</mark>_
* _<mark style="color:blue;">If you detach the NAT's External Interface, internet connections will not work.</mark>_
* _<mark style="color:blue;">If you detach the current External Interface of the NAT and attach a new External Interface, you must reconfigure the VPC/VM according to the IP of the newly attached external interface.</mark>_
* _<mark style="color:blue;">If you intentionally change the</mark> <mark style="color:blue;"></mark><mark style="color:blue;">**vNetwork Image**</mark><mark style="color:blue;">, the NAT will no longer work.</mark>_

