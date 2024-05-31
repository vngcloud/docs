# Release notes

## May 30, 2024 <a href="#april_19_2024" id="april_19_2024"></a>

We are pleased to announce the **General Availability** (GA) release of the VNGCloud Kubernetes Service (VKS). In addition to the features we have provided in previous releases, this GA release brings several new features and enhancements to users. Here are the details of the update:

**New Features:**

* **Re-activate:** VKS allows you to make a system request to automatically recreate the default IAM Service Account if you accidentally delete or change the information of the previously created default IAM Service Account. The default IAM Service Account is the IAM Service Account that the VKS system automatically creates when you start working with VKS. We will use this IAM Service Account to create resources for your Cluster.
* **Event History:** VKS will display the history of events that occur when users work with a Cluster or Node Group. This will be a way for you to monitor the activities happening to your Cluster, thus limiting abnormal activities from occurring.
* **Volume:** VKS has integrated a display of the list of Volumes in the Resource Tab, helping you easily manage the Volumes that are attached to your Cluster.
* **Load Balancer:** VKS has integrated a display of the list of Load Balancers in the Resource Tab, helping you easily manage the Load Balancers that are being used for your Cluster.

**Improvements:**

* **Performance:** VKS has optimized the performance of Cluster creation. Specifically, in the Alpha version, the time from when you start creating a Cluster (with Default Node Group) to when the Cluster transitions to **ACTIVE** state is around 4:00s to 4:30s. Currently, this time has been optimized to <mark style="color:red;">**2:30s to 3:00s**</mark> depending on the Cluster and the time you create it.
* **Garbage collection of unused containers and images:** VKS will automatically delete unused images when the disk usage reaches the usage limit (usage/quota ratio >= 85%).
* **In addition**, we have improved a few other issues in this GA release:
  * Changed the way **Node Names** are named to make it easier for you to use and manage your Cluster. Specifically, the Node Name will have additional information Cluster Name, Node Group Name.
  * Removed **User Builder** on User's Worker Node.
  * Changed the **SSH** mechanism from Port 22 to Port 234.

If you encounter any problems with this GA release, please contact VKS support for assistance.

***

## May 03, 2024 <a href="#april_19_2024" id="april_19_2024"></a>

The latest update for VKS is now available, bringing a variety of new features and improvements for users. Here's a detailed breakdown of the update:

**New Features:**

* **Whitelist:** VKS now enables the creation of Private Node Groups with only Private IPs, while also allowing specific IPs to connect to the cluster through the Whitelist IP feature. For more details, refer to [Whitelist](../clusters/whitelist.md).

**Enhancements:**

* **System Optimization:** Ensures smoother and more efficient system operation.
* **Bug Fixes:** Addresses minor bugs to provide a better user experience.

If you encounter any issues after updating, please contact VKS support for assistance.

***

## **April 17, 2024** <a href="#april_19_2024" id="april_19_2024"></a>

**We are thrilled to introduce the latest update to our VKS service, delivering a more powerful and efficient Kubernetes management experience!**

**Highlights:**

* **Fully Managed Control Plane:** VKS frees you from the burden of managing the Kubernetes Control Plane, allowing you to focus on application development.
* **Support for the Latest Kubernetes Versions:** VKS always stays up-to-date with the latest Kubernetes versions (minor versions from 1.27, 1.28, 1.29) to ensure you always benefit from the most advanced features.
* **Kubernetes Networking:** VKS integrates Calico CNI for high performance and security.
* **Seamless Upgrades:** VKS supports easy and fast upgrades between Kubernetes versions, keeping you up-to-date with the latest enhancements.
* **Automatic Scaling & Healing:** VKS automatically scales Node groups when needed and recovers from node failures, saving you time and management effort.
* **Reduced Costs and Increased Reliability:** VKS deploys the Kubernetes Control Plane in high availability mode and completely free of charge, helping you save costs and enhance system reliability.
* **Native Blockstore Integration (Container Storage Interface - CSI):** VKS allows you to manage Blockstore through Kubernetes YAML, providing persistent storage for containers and supporting critical features like resizing, changing IOPS, and volume snapshots.
* **Load Balancer Integration (Network Load Balancer, Application Load Balancer) via Pre-integrated Drivers like VNGCloud Controller Manager, VNGCloud Ingress Controller:** VKS provides NLB/ALB management through Kubernetes YAML, making it easy to expose your Kubernetes Service externally.
* **Enhanced Security:** VKS allows you to create Private Node Groups with only Private IPs and control access to the cluster through the Whitelist IP feature, ensuring the security of your system.

**With these groundbreaking features, VKS promises to deliver an entirely new Kubernetes management experience, helping you optimize efficiency and save costs!**

**Contact us for consultation and further support!**
