# Node Groups

Node Group is an important concept in Kubernetes, used to manage groups of **nodes** (VMs) with the same configuration in a cluster. For a Node Group, you can:

## Create a Node Group <a href="#nodegroups-taomotnodegroup" id="nodegroups-taomotnodegroup"></a>

To initialize a Node Group, follow the steps below:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** At the previously created Cluster, select **Create a Node group.**

**Step 3:** At the Node Group initialization screen, we have set up information for your Node Group. You can keep these default values ​​or adjust the desired parameters for your Node Group at:

* Node Group Information:
  * **Node Group Name** : A memorable name for your Node Group.
  * **Number of nodes:** Enter the number of Worker nodes for your Cluster, note that the number of nodes needs to be greater than or equal to 1 and less than or equal to 100.
* Node Group Automation Setting:
  * **Auto Healing:** By default we will enable the HA feature in your Cluster. When a node or pod fails, Kubernetes will automatically restart or create a new pod to replace it, ensuring your application always operates without interruption.
  * **Auto Scaling:** Enable auto-scaling in your Cluster. Auto scaling helps automatically adjust the number of pods (application deployment units) based on actual usage needs, avoiding wasting resources when demand is low or overloading when demand is high.
    * **Minimum node** : minimum number of nodes that the Cluster needs to have.
    * **Maximum node** : maximum number of nodes that the Cluster can scale to.
  * Node Group upgrade strategy: Node Group upgrade strategy. When you set up **a Node Group Upgrade Strategy** via the **Surge upgrade** method for a Node Group in VKS, the VKS system will update sequentially to upgrade the nodes, in an unspecified order [.](https://cloud.google.com/kubernetes-engine/docs/concepts/node-pool-upgrade-strategies.)
    * **Max surge:** limits the number of nodes that can be upgraded simultaneously (the number of new nodes (surge) that can be created at the same time). Default **Max surge = 1** - upgrade only one node at a time. with maxUnavailable
    * **Max unavailable** : limits the number of nodes that cannot be reached during the upgrade (the number of existing nodes that can be offline at the same time). Default **Max unavailable = 0** - ensures all nodes are accessible during the upgrade.
* Node Group Setting:
  * **Image** : By default we provide one type of Image, Ubuntu with containerd.
  * **Instance type** : select the appropriate configuration instance type for the Worker node according to your usage needs.
* Node Group Volume Setting: **Boot Volume Configuration** – Parameters are set by default by the system to help optimize your Cluster
* Node Group Network Setting: You can choose **Public Node Group** or **Private Node Group** depending on your Cluster usage needs.
* Node Group Security Setting: You can choose **Security Group and SSH Key** for your Node Group.
* Node Group Metadata Setting: You can enter the corresponding **Metadata for the Node Group.**

**Step 5:** Select **Create Node Group.** Please wait a few minutes for us to initialize your Node Group. The status of the Node Group is currently **Creating** .

**Step 6: When the Node Group** status is **Active** , you can view Node Group information by selecting **Node Group Name** on the main screen.

***

## Edit a Node Group <a href="#nodegroups-chinhsuamotnodegroup" id="nodegroups-chinhsuamotnodegroup"></a>

**For Node Group, you can edit the parameters: Number of Nodes, Auto Scaling, Upgrade Strategy, Security Group in each separate edit** . Specifically, you can follow these steps:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** In the previously created Cluster, select **the Cluster you want to edit the Node group.**

**Step 3:** On the screen containing the list of existing Node Groups, in the Node Group you want to edit, select one of the options:

* Resize feature **:** you can change
  * Number of nodes: Enter the number of Worker nodes for your Cluster, note that the number of nodes needs to be greater than or equal to 1 and less than or equal to 100.
* **Edit Auto Scaling** feature : you can change
  * Auto Scaling: Enable auto-scaling in your Cluster. Auto scaling helps automatically adjust the number of pods (application deployment units) based on actual usage needs, avoiding wasting resources when demand is low or overloading when demand is high.
    * Minimum node: minimum number of nodes that the Cluster needs to have.
    * Maximum node: maximum number of nodes that the Cluster can scale to.
* **Edit Upgrade Strategy** feature : you can change
  * Node Group upgrade strategy: Node Group upgrade strategy. When you set up a Node Group Upgrade Strategy via the Surge upgrade method for a Node Group in VKS, the VKS system will update sequentially to upgrade the nodes, in an unspecified order [.](https://cloud.google.com/kubernetes-engine/docs/concepts/node-pool-upgrade-strategies.)
    * Max surge: limits the number of nodes that can be upgraded simultaneously (the number of new nodes (surge) that can be created at the same time). Default Max surge = 1 - upgrade only one node at a time. with maxUnavailable
    * Max unavailable: limits the number of nodes that cannot be reached during the upgrade (the number of existing nodes that can be offline at the same time). Default Max unavailable = 0 - ensures all nodes are accessible during the upgrade.
* **Edit Security Group** feature : you can change
  * Node Group Security Setting: You can choose Security Group and SSH Key for your Node Group.

***

## Delete a Node Group <a href="#nodegroups-xoamotnodegroup" id="nodegroups-xoamotnodegroup"></a>

{% hint style="info" %}
**Attention:**

When you no longer need to use the Node Group, delete them to save costs. When deleting a Node Group, the following resources will be deleted:

* All nodes included in the Node Group (VM)
{% endhint %}

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select the **Kubernetes Cluster menu.**

**Step 3:** In the successfully created **Cluster , select the Node Group you want to delete and select Delete.**

**Step 4:** Select **Delete** to completely delete your **Node Group .**
