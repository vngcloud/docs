# Create NAT

* Log in to [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/) with region set to HCM.
* Select the **"Public NAT Instance"** menu from the left-hand menu bar.
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

**Note:**

* You can go to the Server list on the "Server" page to perform support functions for the server on the NAT.
* If you detach the NAT's External Interface, internet connections will not work.
* If you detach the current External Interface of the NAT and attach a new External Interface, you must reconfigure the VPC/VM according to the IP of the newly attached external interface.
* If you intentionally change the vNetwork Image, the NAT will no longer work.

