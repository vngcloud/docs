# Auto Healing

#### Overview <a href="#tong-quan" id="tong-quan"></a>

On the VKS system, the Auto Healing feature is applied to each Node Group and is always on. Enabling self-healing in Kubernetes provides many important benefits, helping to ensure high availability and reliability for your applications.

The Auto Healing feature has the following highlights:

* **Automatic error detection:** Kubernetes can automatically detect failed or problematic nodes through monitoring the status of the nodes. Some signs that a node is failing include: node reporting "NotReady" status, node unable to be pinged, node experiencing hardware failure, etc.
* **Automatically restart the node:** When a node detects an error, Kubernetes will automatically restart the node. Restarting the node can help fix temporary errors and return the node to normal operation.
* **Minimize manual intervention:** Auto Healing helps minimize manual intervention by system administrators, saving time and effort.
* **Improved performance:** Auto Healing helps improve system performance by ensuring that nodes always operate normally.

***

#### Mechanism of action <a href="#co-che-hoat-dong" id="co-che-hoat-dong"></a>

**Auto Healing mechanism: VKS system activates auto healing when**

* The Node reports the **NotReady** status on consecutive checks at **10 minute** intervals .

If the above conditions are met, the system will immediately perform auto healing. This process is performed in 2 steps:

* **Step 1:** The VKS system drains the node, which means moving all pods running on this NotReady node to other nodes in the node group before removing that node from the node group.
* **Step 2:** The system will recreate a new node with the configuration set up on the node group and join this node to the cluster. If after rebooting, the node still reports a "NotReady" status, the system will continue to reboot the node until the node returns to its normal operating state.

**Attention:**

* When the system performs Auto Healing, creating a new node may encounter an error if you do not have enough credits or you have run out of quota to create a VM on the vServer system. At this time, every 30 minutes the system will restart the node until the node returns to normal operating status. To avoid the error above, you need to:
  * **Make sure you have enough credits:** If you're a prepaid user, add more credits to your account.
  * **Request a quota increase:** You can request a quota increase for your account [here](https://hcm-3.console.vngcloud.vn/vserver/limit) .

***

#### Turn on Auto Healing <a href="#bat-auto-healing" id="bat-auto-healing"></a>

Currently, the Auto Healing feature is applied to each Node Group and is always **on** . You do not need to manually enable it when initializing the Cluster or Node Group.
