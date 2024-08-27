# Release notes

## Aug 26, 2024 <a href="#april_19_2024-3" id="april_19_2024-3"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update for VKS, bringing numerous new improvements for users. Here are the details of the update:

**Improve:**

* **Kubernetes Version**: VKS has added new images to optimize the size, features, and network compared to the old images. The creation of these images also aims to serve both Public and Private clusters that VKS is about to launch. Specifically, in this release, we have added the following images:
  * Ubuntu-22.kube\_v1.27.12-vks.1724605200
  * Ubuntu-22.kube\_v1.28.8-vks.1724605200
  * Ubuntu-22.kube\_v1.29.1-vks.1724605200

***

## Aug 13, 2024 <a href="#april_19_2024-3" id="april_19_2024-3"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update to the existing VKS, bringing many new improvements to users. Here are the details about the update:

**Improve:**

* **Event History**: VKS has added events for **Auto Scaling** and **Auto Healing.** Now, with Event History, you can track every change occurring within your Cluster, from automatic scaling to automatic healing. These events enhance your ability to monitor and manage your Kubernetes cluster.

***

## Aug 01, 2024 <a href="#april_19_2024-3" id="april_19_2024-3"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update to the already available VKS, bringing many new features and improvements to users. Here are the details about the update:

**New feature:**

* **VKS resource monitoring:** Users can directly monitor the operating status of Cluster, Node, CPU usage, RAM, Memory,... status of Node through intuitive dashboards. To display data on the dashboard, users need to install it `vmonitor-metric-agent`on the cluster where they want to perform monitoring. For more details, refer [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/giam-sat/metrics) .

***

## July 25, 2024 <a href="#april_19_2024-3-1" id="april_19_2024-3-1"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update to the existing VKS, bringing many new improvements to users. Here are the details about the update:

**Improve:**

* **Upgrade VKS management through Terraform:** Users can **simultaneously** adjust the number of nodes and change the number of nodes for autoscale (Minimum/ Maximum node Autoscale) right during the configuration editing process. With the ability to adjust multiple parameters at the same time, managing a Kubernetes cluster becomes more flexible and convenient. For more details, see examples [here](https://registry.terraform.io/providers/vngcloud/vngcloud/latest/docs/resources/vks\_cluster) .

***

## July 23, 2024 <a href="#april_19_2024-3-2" id="april_19_2024-3-2"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update to the existing VKS, bringing many new improvements to users. Here are the details about the update:

**Improve:**

* **Upgrade VNGCloud Controller Manager Plugin, VNGCloud Ingress Controller Plugin:** Errors discovered in previous versions have been fixed, helping the system operate smoother and more reliably.

***

## July 18, 2024 <a href="#april_19_2024" id="april_19_2024"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update to the existing VKS, bringing many new improvements to users. Here are the details about the update:

**Improve:**

* **Upgrade VNGCloud BlockStorage CSI Driver Plugin:** Errors discovered in previous versions have been fixed, helping the system operate smoother and more reliably.

***

## July 17, 2024 <a href="#april_19_2024-1" id="april_19_2024-1"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update to the already available VKS, bringing many improvements to users. Here are the details about the update:

**Improve:**

* **Private Node Group** : The MTU for Nodes belonging to the Private Node Group has been updated to 1450. This improves network performance for applications running in the Private Node Group.
* **Number of nodes and AutoScale** : You can now edit both of these properties in the same API. This simplifies your Cluster management.

***

## July 02, 2024 <a href="#april_19_2024-2" id="april_19_2024-2"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update to the already available VKS, bringing many new features and improvements to users. Here are the details about the update:

**New feature:**

* **Stop POC support for Cluster** : Users can now easily perform Stop POC for all resources being POC on a Cluster, instead of having to perform Stop POC individually for each resource. This helps save time and effort when moving Cluster from test resources to real resources. For more details, refer [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/clusters/stop-poc) .

**Improve:**

* **Node Group status : Added " Degraded** " status so users can monitor the operating status of the Node Group more accurately. This status will display when the number of active nodes is less than the actual number of replicas.
* **Timeout for Cluster and Node Group** : Added timeout for Cluster and Node Group creation, this improvement ensures VKS operates smoothly and efficiently, while providing clear and timely information to users. use. Timeout for Cluster creation is **1 hour** and for Node Group is **3 hours** . If after this time your Cluster or Node Group has not been successfully created, we will update their status to ERROR. At this point, you can delete and create another Cluster or Node Group instead.
* **KubeConfig Access:** Access to the KubeConfig file is now only allowed when the Cluster is Active. This improvement helps users avoid configuration errors when using Terraform to automate Kubernetes deployments.

***

## June 27, 2024 <a href="#april_19_2024-4" id="april_19_2024-4"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update to the existing VKS, bringing many new improvements to users. Here are the details about the update:

**Improve:**

* **Upgrade VNGCloud Controller Manager Plugin, VNGCloud Ingress Controller Plugin:** Errors discovered in previous versions have been fixed, helping the system operate smoother and more reliably.

***

## June 19, 2024 <a href="#april_19_2024-5" id="april_19_2024-5"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update to the existing VKS, bringing many new improvements to users. Here are the details about the update:

**Improve:**

* **Upgrade PVC size setting feature (Persistent Volume Claim Size):** Users can now specify the minimum size for CSI drives to be **1GB** instead of the minimum size of 20GB as before. For more details, you can refer to Volume and Integrate with Container Storage Interface .
* **Change the default Storage Class used for Cluster:** change the default from SSD type drives - IOPS 200 to the default SSD type drives - IOPS 3000.
* **Upgrade VNGCloud Controller Manager Plugin, VNGCloud Ingress Controller Plugin:** plugin improvements help avoid duplicate Load Balancer naming.

**Attention:**

Because the old default Storage Class has been removed from the system, if you want to continue using and resize this storage class, you can:

* Create a Storage Class named sc-iops-200-retain with the Volume Type you desire.
* Resize Storage Class via command:

Copy

```
kubectl patch pvc sc-iops-200-retain -p '{"spec":{"resources":{"requests":{"storage":"50Gi"\}}\}}'
```

For more details, refer to Integrate with Container Storage Interface .

***

## June 12, 2024 <a href="#april_19_2024-6" id="april_19_2024-6"></a>

VKS (VNGCloud Kubernetes Service) introduces the latest update to the already available VKS, bringing many new features and improvements to users. Here are the details about the update:

**New feature:**

* **Support users working with VKS through Terraform:** Users can easily create Clusters and Node Groups in VKS using Terraform. For more details, refer here .

**Improve:**

* **Upgrade VNGCloud Controller Manager Plugin:** Add Annotation to configure Load Balancer to support Proxy Protocol. For more details, refer [here](../bat-dau-voi-vks/preserve-source-ip-khi-su-dung-vlb-layer4-va-nginx-ingress-controller.md) .

***

## May 30, 2024 <a href="#april_19_2024-7" id="april_19_2024-7"></a>

We are extremely pleased to announce that the official release ( **General Availability** ) of VNGCloud Kubernetes Service is available. With this official release, in addition to the features we have provided on previous releases, this version will bring many new features and improvements to users. Here are the details about the update:

**New feature:**

* **Re-activate:** VKS allows you to request the system to automatically re-initialize the default IAM Service Account when you mistakenly delete or change previously created default IAM Service Account information. The default IAM Service Account is the IAM Service Account that is automatically created by the VKS system when you start working with VKS. We will use this IAM Service Account to initialize resources for your Cluster.
* **Event History** : VKS will display the history of events that occur when users work with the Cluster or each Node Group. This will be a way to help you monitor activities occurring with your Cluster, thereby limiting unusual activities from occurring.
* **Volume** : VKS has integrated the display of the Volume list at the Resource Tab, helping you easily manage the Volumes that are attached to your Cluster.
* **Load Balancer** : VKS has integrated the display of the Load Balancer list in the Resource Tab, helping you easily manage the Load Balancers being used for your Cluster.

**Improve:**

* **Performance** : VKS has optimized performance when initializing the Cluster. Specifically, in the Alpha version, the time from the start of Cluster initialization (with Default Node Group) to the time the Cluster switches to **ACTIVE** state is about 04:00s to 04:30s. Currently, this time has been optimized by us to **02:30s to 03:00s** depending on each Cluster and each time you initialize.
* **Garbage collection of unused containers and images** : VKS will automatically delete unused images when the disk reaches the usage limit (usage/quota ratio >= 85%).
* **In addition** , this GA version has improved a few other issues such as:
  * Changing **the Node Name** helps you easily use and manage your Cluster. Specifically, the Node Name will have additional information: **Cluster Name** , **Node Group Name** .
  * Delete **User Builder** on User's Worker Node.
  * **Change SSH** mechanism from Port 22 to Port 234.

If you encounter any problems with this official release, please contact VKS support for assistance.

***

## May 03, 2024 <a href="#april_19_2024-8" id="april_19_2024-8"></a>

The latest update for VKS is available, bringing many new features and improvements to users. Here are the details about the update:

**New feature:**

* **Supports Whitelist feature:** VKS allows creating a Private Node Group with only Private IP and also allows any IP to connect to the Cluster through the Whitelist IP feature. For more details, please refer to Whitelist .

**Improve:**

* **System optimization:** Helps the system operate more smoothly and efficiently.
* **Bug Fixes:** Fixed some minor bugs to provide a better user experience.

If you encounter any problems after updating, please contact VKS support for assistance.

***

## April 17, 2024 <a href="#april_19_2024-9" id="april_19_2024-9"></a>

**We're excited to introduce a new update to the VKS service, giving you a more powerful and efficient Kubernetes management experience than ever before!**

**Highlights:**

* **Fully Managed control plane:** VKS will free you from the burden of managing Kubernetes' Control Plane, helping you focus on application development.
* **Supports the latest versions of Kubernetes:** VKS always updates the latest versions of Kubernetes (minor versions from 1.27, 1.28, 1.29) to ensure you always take advantage of the most advanced features.
* **Kubernetes Networking:** VKS integrates Calico CNI, providing high efficiency and security.
* **Upgrade seamlessly:** VKS supports upgrading between Kubernetes versions easily and quickly, helping you stay up to date with the latest improvements.
* **Scaling & Healing Automatically:** VKS automatically expands the Node group when necessary and automatically fixes errors when the node has problems, helping you save time and effort on management.
* **Reduce costs and improve reliability:** VKS deploys Control Plane of Kubernetes in high availability mode and is completely free, helping you save costs and improve system reliability.
* **Blockstore Native (Container Storage Interface - CSI) integration:** VKS allows you to manage Blockstore through Kubernetes' YAML, providing persistent storage for containers and supporting important features such as resizing, IOPS scaling and snapshot volumes.
* **Integrate Load Balancer (Network Load Balancer, Application Load Balancer) through built-in drivers such as VNGCloud Controller Mananger, VNGCloud Ingress Controller:** VKS provides the ability to manage NLB/ALB through YAML of Kubernetes, making it easy for you expose Service in Kubernetes to the outside.
* **Enhance security:** VKS allows you to create a Private Node Group with only Private IP and control access to the cluster through the IP Whitelist feature, ensuring the safety of your system.

**With these breakthrough features, VKS promises to bring you a completely new Kubernetes management experience, helping you optimize efficiency and save costs!**

**Please contact us for further advice and support!**
