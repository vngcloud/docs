# Node Groups

Node Group is an important concept in Kubernetes, used to manage groups of nodes (VMs) with the same configuration within a cluster. For a Node Group, you can:

### Create a Node Group <a href="#nodegroups-createanodegroup" id="nodegroups-createanodegroup"></a>

To create a Node Group, follow the steps below:

**Step 1:** Go to [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** In the previously created Cluster, select **Create a Node group.**

**Step 3:** On the Node Group creation screen, we have set up the information for your Node Group. You can keep these default values or adjust the desired parameters for your Node Group:

* Node Group Information:
  * **Node Group Name**: A memorable name for your Node Group.
  * **Number of nodes:** Enter the number of Worker nodes for your Cluster, note the number of nodes should be between 1 and 100.
* Node Group Automation Setting:
  * **Auto Healing:** By default, we will enable HA in your Cluster. When a node or pod fails, Kubernetes will automatically restart or create a new pod to replace it, ensuring your application runs uninterrupted.
  * **Auto Scaling:** Enable automatic scaling in your Cluster. Auto scaling automatically adjusts the number of pods based on actual usage needs, preventing resource waste when demand is low or overload when demand is high.
    * **Minimum node**: the minimum number of nodes the Cluster needs.
    * **Maximum node**: the maximum number of nodes the Cluster can scale to.
  * Node Group upgrade strategy: upgrade strategy for the Node Group. When you set **Node Group Upgrade Strategy** through the **Surge upgrade** method for a Node Group in VKS, the VKS system will sequentially update nodes for upgrade, in an undefined order.
    * **Max surge:** limits the number of nodes being upgraded simultaneously (number of new nodes (surge) that can be created at once). Default **Max surge = 1** - only one node is upgraded at a time.
    * **Max unavailable**: limits the number of nodes unavailable during the upgrade (number of current nodes that can be disrupted at once). Default **Max unavailable = 0** - ensures all nodes are accessible during the upgrade.
* Node Group Setting:
  * **Image**: by default, we provide one type of Image - Ubuntu with containerd.
  * **Instance type**: select the suitable configuration type for the Worker node as per your needs.
* Node Group Volume Setting: **Boot Volume Configuration** – Parameters are default set by the system optimized for your Cluster.
* Node Group Network Setting: You can choose **Public Node Group** or **Private Node Group** based on your Cluster requirement.
* Node Group Security Setting: You can select **Security Group and SSH Key** for your Node Group.
* Node Group Metadata Setting: You can enter corresponding **Metadata** for the Node Group.

**Step 5:** Select **Create Node Group.** Wait a few minutes for us to create your Node Group, at which point the Node Group status will be **Creating**.

**Step 6:** When the status of **Node Group** is **Active**, you can view the Node Group information by selecting **Node Group Name** on the main screen.

***

### Delete Node Group <a href="#nodegroups-xoamotnodegroup" id="nodegroups-xoamotnodegroup"></a>

{% hint style="info" %}
Note:

When you no longer need to use Node Group, delete them to save costs. When deleting Node Group, the following resources will be deleted:&#x20;

* All nodes in Node Group (VM)
{% endhint %}

Step 1: Go to https://vks.console.vngcloud.vn/overview&#x20;

Step 2: On the Overview screen, select the Kubernetes Cluster menu.&#x20;

Step 3: In the successfully created Cluster, select the Node Group you want to delete and select Delete.&#x20;

Step 4: Select Delete to completely delete your Node Group.
