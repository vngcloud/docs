# Network Configuration

### Overview <a href="#tong-quan" id="tong-quan"></a>

When deploying a hybrid cloud solution like vCloudStack, the network setup plays a central role in ensuring that applications and data can be efficiently processed both in the cloud and on-premises. Therefore, users and system administrators need to carefully design to ensure that services run smoothly, securely and efficiently, helping businesses achieve the optimal balance between the flexibility of the cloud and the performance and compliance requirements of on-premises.

vCloudstack provides administrators with an interface to configure Network information settings at the Admin Site interface. This is a prerequisite step for users to perform Virtual Server Initialization at the User Site interface.

### Steps to follow: <a href="#cac-buoc-thuc-hien" id="cac-buoc-thuc-hien"></a>

**Step 1** : User accesses and logs in to Admin Site, go to Infrastructure/Network;

{% hint style="info" %}
**Note:** The user performing the operation must be authorized to use the Create Network function at Admin Site.
{% endhint %}

**Step 2:** User fills in parameters to configure Network;

* **Network Name** (required): Enter an arbitrary name for users to identify the created Network;
* **CIDR** (required): Fill in IP address allocation
* **IP Gateway** (required): enter the gateway IP address for the subnet;
* **Network Type** (required): vCloudStack currently supports vlan network type;
* **Segment ID** (required): enter the code compatible with the network type;
* **Physical Network** : default display vlan by network type;
* **Share Type/Owner** (required): Fill in the email of the user who will manage and use this network;
* **Shared all** : Option allows all users to use this Network to create virtual machines;

{% hint style="info" %}


**Note:**

* If creating a private Network, just fill in the Email Owner as the Email User used to create the virtual machine and do not need to select Share all;
* If you create a public Network, you can use the Share all function for all users to create virtual machines.
{% endhint %}

_Example of Network configuration content:_

* Network Name: _network-01_
* CIDR: _192.168.1.0/24_
* IP Gateway: _192.168.1.1_
* Network Type: _vlan_
* IP Segment: _100_
* Share Type/Owner: _admin01@abc.com_

**Step 3** : Successfully create Network

* Users who are allowed to use the Network will see the Networks on the User Site/Network screen;
* The user can then use the created Network to Initialize the virtual server.
