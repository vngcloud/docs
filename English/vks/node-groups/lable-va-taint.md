# Lable and Taint

## Lable <a href="#label" id="label"></a>

Labels are an important feature in Kubernetes, used to organize and manage objects effectively. You can assign key-value pairs to Kubernetes objects such as Pod, Node, Service, Deployment, etc. Specifically:

* **Each Lable is a key-value pair:** Key is a string of characters used to identify the name of the label. Value is an optional character string that provides detailed information about the label.
* **Keys and values ​​must follow the naming rules:** Keys and values ​​must not contain spaces or special characters other than (-, \_,.).
* Lable can be used for a variety of purposes, including:
  * Classify objects based on criteria such as environment, version, status, etc
  * Monitor and manage objects in a Kubernetes cluster.

**For example:**

* `app: nginx`- This label indicates the object is related to the Nginx application.
* `environment: production`- This label indicates that the object belongs to the production environment.
* `version: 1.7.2`- This label indicates the object is related to version 1.7.2.

### **Create Label** <a href="#tao-lable" id="tao-lable"></a>

To create a Lable for a Node Group, follow these instructions:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** At the previously created Cluster, select **Create a Node group.**

**Step 3:** At the Node Group initialization screen, we have set up information for your Node Group. You can keep these default values ​​or adjust the desired parameters for your Node Group. In the **Node Group Metadata Setting section,** you need:

* Enter the key for your label. The key must begin and end with letters or numbers and include the characters az, AZ, 0-9, -, \_, . Maximum 253 characters. Alternatively, you can enter the key as a DNS subdomain, for example: [example.com/my-app](http://example.com/my-app)
* Enter the value for this corresponding key.

**Step 5:** Select **Create Node Group.** Please wait a few minutes for us to initialize your Node Group. The status of the Node Group is currently **Creating** .

**Step 6: When the Node Group** status is **Active** , you can view Node Group information by selecting **Node Group Name** on the main screen.

Or you can create Lable through kubectl with the command:

```
kubectl label nodes my-node1 disktype=ssd
```

You can check the newly created label again with the command:

```
kubectl get nodes --show-labels
```

For example the result for this command would be as follows:

```
NAME      STATUS    ROLES    AGE     VERSION        LABELS
worker0   Ready     <none>   1d      v1.13.0        ...,disktype=ssd,kubernetes.io/hostname=worker0
worker1   Ready     <none>   1d      v1.13.0        ...,kubernetes.io/hostname=worker1
worker2   Ready     <none>   1d      v1.13.0        ...,kubernetes.io/hostname=worker2
```

### **Use Lable with nodeSelector** <a href="#su-dung-lable-voi-nodeselector" id="su-dung-lable-voi-nodeselector"></a>

nodeSelector is a parameter used in PodSpec to specify that Pods should only be scheduled on Nodes with a specific label. This is useful when you want to run Pods on Nodes with specific resources or properties.

* **Create a my-pod.yaml** file containing the following content:

```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  nodeSelector:
    disktype: ssd
    region: hcm03
```

In this example, the Pod `my-pod`is scheduled only on Nodes with label `disktype: ssd`and `region: hcm03`.

* Deploy Pod on your Cluster:

```
kubectl -f apply my-pod.yaml
```

***

## Taint <a href="#taint" id="taint"></a>

Taint is an important feature in Kubernetes, serving as a mechanism to tag Nodes and control Pod scheduling on those Nodes. Different from regular Label, Taint is used to specify special properties of Node and execute specific actions when Pod does not meet the conditions defined by Taint. Specifically:

Specifically:

* **Each Taint includes:**
  * Key is a string of characters used to identify the name of the taint.
  * Value is an optional character string that provides detailed information about the taint.
  * Effect:
    * **NoSchedule:** Prevent Pods from having a corresponding Toleration scheduled on the Node.
    * **NoExecute:** Allows the Pod to be scheduled on the Node but the Pod will not be executed.
    * **PreferNoSchedule:** Kubernetes will try to prioritize not scheduling the Pod to the Node with this Taint.
* **Keys and values ​​must follow the naming rules:** Keys and values ​​must not contain spaces or special characters other than (-, \_,.).
* **Toleration:** In order for a Pod to be scheduled and run on a Node with Taint, the Pod needs to have a corresponding Toleration. Toleration is declared in PodSpec using `tolerations`field. For example:

```
tolerations: - key: node.role.kubernetes.io/master effect: NoSchedule
```

* **Relationship between Taint and Toleration:** When Kubernetes schedules a Pod, Kubernetes matches the Node's Taints with the Pod's Tolerations. Pods are only scheduled on a Node if there is Toleration for all Taints of that Node.

**For example:**

* node.role.kubernetes.io/master:NoSchedule - prevents regular Pods from being run on this Node.

### **Create Taints** <a href="#tao-taint" id="tao-taint"></a>

To create a Taint for a Node Group, follow these instructions:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** At the previously created Cluster, select **Create a Node group.**

**Step 3:** At the Node Group initialization screen, we have set up information for your Node Group. You can keep these default values ​​or adjust the desired parameters for your Node Group. In the **Node Group Metadata Setting section,** you need:

* Enter the key for your taint. The key must begin and end with letters or numbers and include the characters az, AZ, 0-9, -, \_, . Maximum 253 characters. Alternatively, you can enter the key as a DNS subdomain, for example: [example.com/my-app](http://example.com/my-app)
* Enter the value for this corresponding key.
* Choose 1 of 3 effect types: **NoSchedule, NoExecute, PreferNoSchedule.**

**Step 5:** Select **Create Node Group.** Please wait a few minutes for us to initialize your Node Group. The status of the Node Group is currently **Creating** .

**Step 6: When the Node Group** status is **Active** , you can view Node Group information by selecting **Node Group Name** on the main screen.

Or you can create Taint through kubectl with the command:

```
kubectl taint node my-node node.role.kubernetes.io/master:NoSchedule.
```

**Taint usage example:**

Suppose you have a Node `master`used for management purposes and you want to prevent regular Pods from being run on this Node. You can use Taint as follows:

```
kubectl taint node my-master node.role.kubernetes.io/master:NoSchedule
```

In order for Pod to run on Node `master`, the Pod needs to have the corresponding Toleration:

```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  tolerations:
  - key: node.role.kubernetes.io/master
    effect: NoSchedule
```
