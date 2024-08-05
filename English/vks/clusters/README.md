# Clusters

**A cluster in Kubernetes** is a collection of one or more virtual machines (VMs) connected together to run containerized applications. Cluster provides a unified environment to deploy, manage, and operate containers at scale.

#### Prerequisites: <a href="#clusters-dieukiencan" id="clusters-dieukiencan"></a>

To be able to initialize a **Cluster** and **Deploy** a **Workload** , you need:

* There is at least 1 **VPC** and 1 **Subnet in ACTIVE** state . If you do not have a VPC or Subnet yet, please create a VPC and Subnet according to the instructions here [.](../../vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc.md)
* There is at least 1 **SSH key in ACTIVE** state . If you do not have any SSH key, please create an SSH key according to the instructions here [.](../../vserver/compute-hcm03-1a/security/ssh-key-bo-khoa.md)
* Installed and configured **kubectl** on your device. Please refer here [if](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) you are not sure how to install and use kuberctl. In addition, you should not use a kubectl version that is too old, we recommend that you use a kubectl version that is no more than one version different from the cluster version.

***

## Initialize Cluster <a href="#clusters-khoitaocluster" id="clusters-khoitaocluster"></a>

To initialize a Cluster, follow the steps below:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select **Activate.**

**Step 3:** Wait until we successfully create your VKS account. After Activate successfully, select **Create a Cluster.**

**Step 4:** At the Cluster initialization screen, we have set up information for the Cluster and a **Default Node Group** for you. You can keep these default values ​​or adjust the desired parameters for the Cluster and Node Group at Cluster Configuration, Default Node Group Configuration, Plugin.

* Cluster Configuration:
  * Cluster Information:
    * **Cluster Name:** Name for your Cluster. The name can only contain alphanumeric characters (az, AZ, 0-9, '\_', '-'). Your input data length must be from 5 to 50. The name must be unique within the Region and VNG Cloud account you are creating the Cluster for.
    * **Kubernetes Version:** The version of Kubernetes that will be used for your Cluster. We recommend that you choose the latest version, unless you need an older version.
    * **Description:** Enter the information you want to note for the Cluster to create a separate mark for easier management in the future.
  * Network Setting:
    * **Network type, Encapsulation Mode** are selected by default by the system and you cannot change them, however you can re-enter **Calico CIDR** parameters (note that IP must be private and can be selected according to the following options ( 10.0.0.0 - 10.255.0.0 / 172.16.0.0 - 172.24.0.0 / 192.168.0.0)
    * **VPC:** Select an existing VPC that meets K8S requirements to create your Cluster. Before choosing a VPC, we recommend that you familiarize yourself with all VPC requirements and considerations as well as Subnet requirements and considerations. You cannot change which VPC you want to use after creating the Cluster. If no VPC is listed, you need to create one first. For more information, see [**Create a VPC**](../../vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc.md) **.**
    * **Subnet:** By default, all available subnets in the VPC specified in the previous field will be randomly selected in the first order, you can choose another Subnet again, but only 1 can be selected.
* Default Node group Configuration:
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
* Plugins
  * **Enable BlockStore Persistent Disk CSI Driver** : enable us to automatically install CSI Controller on your Cluster.
  * **Enable vLB Native Integration Driver** : enable us to automatically install LB Controller on your Cluster.

**Step 5:** Select **Create Kubernetes cluster.** Please wait a few minutes for us to initialize your Cluster, the Cluster's status is now **Creating** .

**Step 6: When the Cluster** status is **Active** , you can view Cluster information and Node Group information by selecting Cluster Name in the **Name** column .

***

#### Download the Kube Config file <a href="#clusters-taixuongteptinkubeconfig" id="clusters-taixuongteptinkubeconfig"></a>

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select the **Kubernetes Cluster menu.**

**Step 3:** In the successfully created **Cluster , select the icon and** select **Download Config File.**![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F71729305%2Fimage2024-4-16\_16-41-12.png%3Fversion%3D1%26modificationDate%3D1713260474000%26api%3Dv2\&width=40\&dpr=4\&quality=100\&sign=95404067\&sv=1)

**Step 4:** The config file will be saved to your computer, now you can use Kubectl to manage your Cluster on your personal device.

***

#### Delete a Cluster <a href="#clusters-xoamotcluster" id="clusters-xoamotcluster"></a>

Attention:

**When you no longer need to use a Kubernetes Cluster, you should delete the resources associated with that cluster so you don't incur any unnecessary costs. When deleting a Kubernetes Cluster the following resources will be deleted:**

* Control Plane Resource of the Cluster.
* All nodes in the Cluster (VM)
* Which Pods are all running on the nodes.
* The default Security Group is created for that Cluster.
* The default Load Balancer is created for that Cluster.
* ETCD.

**The system may not delete the following resources:**

* The Load Balancer is integrated into the Cluster by you.
* Persistent Volume is integrated into the Cluster by you.

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select the **Kubernetes Cluster menu.**

**Step 3:** In the successfully created **Cluster , select the cluster you want to delete and select Delete**

**Step 4:** Select **Delete** to completely delete your Cluster.
