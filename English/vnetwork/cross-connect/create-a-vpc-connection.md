# Create a VPC Connection

**Follow these steps to create a VPC connection between two regions:**

**Step 1**: Successfully log in to VNG Cloud, and on the Console screen, navigate to the vNetwork service;

**Step 2**: In the left-hand menu of the vNetwork interface, select the Cross Connect section;

**Step 3**: The screen will navigate to the Cross Connect List page;

**Step 4**: On the Cross Connect list screen, click on the previously created Cross Connect;

**Step 5**: On the Cross Connect detail screen, in the Connections tab, click '**Add VPC's Connections**' to create a VPC connection between the two regions;

<figure><img src="../../.gitbook/assets/image11.png" alt=""><figcaption></figcaption></figure>

**Step 6**: On the **Add VPC's Connections** screen:

* The user must first select the **Requester's VPC**;
* The system will check connection conditions based on the selected Requester's VPC and display the available **Accepter's VPCs** that can be connected;

<figure><img src="../../.gitbook/assets/image22.avif" alt=""><figcaption></figcaption></figure>

**Step 7**: After selecting the VPC pair to connect, click **Add** to create the new VPC connection pair.

<figure><img src="../../.gitbook/assets/image33.avif" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:**

* The **Requester Region** and **Accepter Region** are understood to be two independent regions that form a Cross Connect connection (the Requester Region is automatically selected based on the region chosen when accessing vServer).
* The VPCs in each region must be pre-created in vServer (refer to [**Create VPC**](../../vserver/compute-hcm03-1a/vpc/virtual-private-cloud-vpc.md)).
{% endhint %}
