# Auto Scaling

## Overview <a href="#tong-quan" id="tong-quan"></a>

Auto Scaling for Cluster is a feature in Kubernetes that allows automatically adjusting the size of the cluster, specifically the number of nodes in the cluster to meet usage needs.

The Auto Scaling feature has the following highlights:

1. **Optimize performance:** Auto Scaling allows the cluster to automatically scale resources as needed. When workloads are higher, the cluster automatically creates additional nodes to ensure applications operate at their best performance.
2. **Cost savings:** Auto Scaling allows the cluster to automatically reduce resources when not needed. If workload decreases, the cluster automatically reclaims unused resources to save costs.
3. **Ensure availability:** Auto Scaling helps ensure that the cluster is available to meet demand and avoid resource overload or shortages.
4. **Auto Scaling:** Auto Scaling helps automatically recover from crashes or errors by creating new nodes to replace failed nodes.

When deploying applications in a cloud environment, using Auto Scaling helps optimize resource usage, improve application availability and performance, and makes cluster management easy and convenient. more effective.

***

## Mechanism of action <a href="#co-che-hoat-dong" id="co-che-hoat-dong"></a>

### **Scale up mechanism: the Procuracy system performs scale up when**

* Pods cannot be scheduled on any existing node due to lack of resources.
* Adding 1 more node similar to the current node group configuration is useful and can handle this resource shortage problem.

Illustration:

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

If the above two conditions are met, the system will increase the number of nodes (one or more nodes) to accommodate all unscheduling pods. This process will be done immediately in 2 steps:

* **Step 1:** The VKS system creates a new node according to the current node group configuration.
* **Step 2:** The VKS system will deploy these unscheduling pods to new nodes.

{% hint style="info" %}
**Attention:**

* When the system performs Auto Scaling, creating a new node may encounter an error if you do not have enough credits or you have run out of quota to create a VM on the vServer system. To avoid the error above, you need to:
  * **Make sure you have enough credits:** If you're a prepaid user, add more credits to your account.
  * **Request a quota increase:** You can request a quota increase for your account [here](https://hcm-3.console.vngcloud.vn/vserver/limit) .
{% endhint %}

### **Scale down mechanism: the Procuracy system performs scale down when**

* One or more nodes have continuously low load over a period of time. Specifically, the node has low utilization (availability) including CPU and memory requests of the pod at **< 50%.**
* All existing pods of that node, can be moved to another node without any problem.

If the above two conditions are met, by default within about 10 minutes, that node will be deleted from the Cluster. This deletion process will include 3 steps:

* **Step 1:** The VKS system will mark that node as unschedulable.
* **Step 2:** The system moves the entire pod to another node.
* **Step 3:** After successfully moving all pods to another node, the VKS system will delete the marked node.

***

## **Turn on Auto Scaling** <a href="#autoscaling-batautoscaling" id="autoscaling-batautoscaling"></a>

On the VKS system, you can turn on Auto Scaling when:

* **Initialize a Cluster**
* **Create a Node Group**
* **Edit a Node Group**

To enable Auto Scaling for your Kubernetes Cluster please enable the **Enable Auto Scaling option.** When enabling this option you need to enter:.

* **Minimum node** : minimum number of nodes that the Cluster must have.
* **Maximum node** : maximum number of nodes that the Cluster can scale to.
* **Node Group upgrade strategy** : Node Group upgrade strategy. When you set up **a Node Group Upgrade Strategy** via the **Surge upgrade** method for a Node Group in VKS, the VKS system will update sequentially to upgrade the nodes, in an unspecified order [.](https://cloud.google.com/kubernetes-engine/docs/concepts/node-pool-upgrade-strategies.)
  * **Max surge:** limits the number of nodes that can be upgraded simultaneously (the number of new nodes (surge) that can be created at the same time). Default **Max surge = 1** - upgrade only one node at a time.
  * **Max unavailable** : limits the number of nodes that cannot be reached during the upgrade (the number of existing nodes that can be offline at the same time). Default **Max unavailable = 0** - ensures all nodes are accessible during the upgrade.

For example, as shown below: I have initialized a Node Group with:

* **Number of nodes: 3 nodes**
* **Minimum nodes: 1 nodes**
* **Maximum nodes: 5 nodes**

At this time:

* If one or more pods cannot be scheduled on any node on the cluster due to lack of resources and adding a node similar to this node group configuration can solve the problem, the system will perform scale up. With this setup, the system can scale up to a maximum of **5 nodes** .
* If there is a node with low utilization (availability) at **< 50%** and all pods of that node can be scheduled on another node, the system will perform scale up. With this setup, the system can scale down to a minimum of **1 node.**
