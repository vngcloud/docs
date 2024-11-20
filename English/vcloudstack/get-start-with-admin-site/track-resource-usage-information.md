# Track resource usage information

### Overview <a href="#tong-quan" id="tong-quan"></a>

The User Resource interface allows administrators to monitor all Resources (including VMs and Volumes) created and used by the virtualized infrastructure by the operator of that resource.

To access the User Resource screen, go to vCloudStack Admin Site and select User Resource in the control bar to be navigated to the User Resource screen.

The interface includes a list of resources (such as VM Server, Volume, LB). The detailed parameters displayed in the interface screen include:

**At the Server Interface Tab (VM)** :

* **Name:** Displays the name of the VM and the Identifier of the created or running VM;
* **Status:** Allows to identify the operating state of the VM resource;
* **Internal IP:** Indicates which Internal IP address this VM is using;
* **Location:** Location information
* **External IP:** Indicates which External IP address this VM is using;
* **Instance Type:** VM configuration information and operating system
* **Owner:** Email of the user account that created this VM.

{% hint style="info" %}
**Note** : Only VMs created by the Admin can be quickly selected to navigate to view details of that VM and vice versa.
{% endhint %}

**At the Volume interface tab:**

* **Name:** Displays the name of the Volume and the Identifier of the created or active Volume;
* **Status:** Allows to identify the operating status of the Volume resource;
* **Type:** Displays the configuration type ID of this Volume;
* **IOPS:** Displays the number of IOPS;
* **Size:** Capacity of created volume;
* **Attachment:** Indicates which Volume the Volume is attached to;
* **Multi-attach:** Indicates whether the Volume has multiple resources attached;
* **Owner:** Email of the user account that created this Volume.
