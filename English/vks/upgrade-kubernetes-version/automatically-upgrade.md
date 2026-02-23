# Automatically Upgrade

## **Overview**

**Automatically Upgrade Cluster on VKS** is the process where the VKS system automatically upgrades the cluster according to the upgrade window you specify, or automatically upgrades to improve system performance, security, and compatibility. Currently, VKS provides 2 types of automatic upgrades:

### **1. Required Upgrades**

* **Purpose**: Required upgrades to protect the cluster from risks related to security, stability, and the use of unsupported Kubernetes versions.
* **Specifically**: the VKS system will upgrade the cluster in the following cases:
  * **End-of-Life (EOL) Upgrades**: Update the Cluster to newer versions when the current version is about to expire.
  * **Security Upgrades**: Patch security vulnerabilities to ensure data safety.
  * **Stability Upgrades**: Fix critical bugs affecting system stability.
* **Execution time**:
  * These upgrades will be automatically performed by the VKS system <mark style="color:red;">**after 8 PM on any day**</mark> if needed, to minimize impact on you. We will notify you about these upgrades as soon as possible.

### **2. Regular Upgrades**

* **Purpose**: Periodic upgrades according to the **upgrade window** you specify to keep your cluster up to date with the latest versions, including both **minor version** and **patch version**.
* **Specifically**:&#x20;
  * **Minor Version Upgrades**: Update new features and APIs. For example, if the current cluster is using version 1.28.2, the system will automatically upgrade to version 1.29.6.
  * **Patch Version Upgrades**: Fix minor bugs and improve performance. For example, if the current cluster is using version 1.29.1, the system will automatically upgrade to version 1.29.2.
*   **Execution time**:

    * You can configure the upgrade schedule through **VKS Portal** following the guide below. After you select the auto-upgrade schedule via VKS Portal, the system will **start the upgrade after at least&#x20;**<mark style="color:red;">**6 days**</mark> from the current date. This time allows you to prepare and test before the upgrade takes place.
    * The system will **repeat for subsequent weeks** from the previous upgrade and follow the days you selected.
    * **Before each upgrade**, the system will send a **notification email** 6 days before the actual auto-upgrade time. In the email, we will specify the exact time the auto-upgrade will take place.
    * If you **select multiple days in the week** (such as Monday, Thursday), the system will calculate the upgrade cycle for the selected days, without affecting other days.

    _Please refer to the 2 examples below to understand how the VKS system performs Regular Upgrades._

<details>

<summary>Case 1: You select the schedule to run on Tuesday every week at 08:00 PM</summary>

Suppose _**Today is Monday (02/12/2024)**_

* _You select auto-upgrade on **Tuesday, 08:00 PM**._
* _The system schedule will be as follows:_
  * _**04/12/2024 (Wednesday)**: Send email notification for upgrade **#1**._
  * _**10/12/2024 (Tuesday, 08:00 PM)**: Perform **auto-upgrade #1 successfully.**_
  * _**11/12/2024 (Wednesday)**: Send email notification for upgrade **#2**._
  * _**17/12/2024 (Tuesday, 08:00 PM)**: Perform **auto-upgrade #2 successfully.**_
  * _**18/12/2024 (Wednesday)**: Send email notification for upgrade **#3**._
  * _**24/12/2024 (Tuesday, 08:00 PM)**: Perform **auto-upgrade #3 successfully**, and continue repeating._

</details>

<details>

<summary>Case 2: You select the Auto-upgrade schedule for Monday and Thursday every week at 12:00 PM</summary>

_Suppose **Today is Tuesday (03/12/2024)**_

* _You select auto-upgrade on **Monday and Thursday, 12:00 PM**._
* _The system schedule will be as follows:_

_**Thursday schedule (12:00 PM)**:_

* _**06/12/2024 (Friday)**: Send email notification for upgrade **#1**._
* _**12/12/2024 (Thursday, 12:00 PM)**: Perform **auto-upgrade #1 successfully.**._
* _**13/12/2024 (Friday)**: Send email notification for upgrade **#2**._
* _**19/12/2024 (Thursday, 12:00 PM)**: Perform **auto-upgrade #2 successfully.**._
* _**20/12/2024 (Friday)**: Send email notification for upgrade **#3**._
* _**26/12/2024 (Thursday, 12:00 PM)**: Perform **auto-upgrade #3 successfully,** and continue repeating._

_**Monday schedule (12:00 PM)**:_

* _**10/12/2024 (Tuesday)**: Send email notification for upgrade **#1**._
* _**16/12/2024 (Monday, 12:00 PM)**: Perform **auto-upgrade #1 successfully.**._
* _**17/12/2024 (Tuesday)**: Send email notification for upgrade **#2**._
* _**23/12/2024 (Monday, 12:00 PM)**: Perform **auto-upgrade #2 successfully..**_
* _**24/12/2024 (Tuesday)**: Send email notification for upgrade **#3**._
* _**30/12/2024 (Monday, 12:00 PM)**: Perform **auto-upgrade #3 successfully,** and continue repeating._

</details>

{% hint style="info" %}
**Note:**

* The VKS system **will try to perform upgrades** according to the schedule you configured via **VKS Portal**. However, depending on system load, **some upgrades may be delayed** or not performed on schedule. In that case, the system will automatically reschedule the upgrade to **the next appropriate time**, which is the repeat cycle in the following week.
{% endhint %}

***

## **Steps to configure**

Below are instructions for updating the Upgrade Policy on the VKS system:

**Step 1:** Go to [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Step 2:** Select **Create a Cluster.**

**Step 3:** On the Cluster creation screen, we have pre-configured information for the Cluster and a **Default Node Group.** In the Cluster Upgrade policy section, you can select **Enable/ Disable Automatic upgrade.** Where:

* **Enable Automatic upgrade**, in this case:
  * **Required Upgrades** will be automatically performed after 8 PM on any day by the VKS system when needed.
  * **Regular Upgrades** will be performed according to the schedule you set.
* **Disable Automatic upgrade, in this case**:
  * Only **Required Upgrades** will be automatically performed after 8 PM on any day by the VKS system when needed.

**Step 4:** If you select **Enable Automatic upgrade**, please select the time the system can perform the upgrade. Specifically, you need to:

* **Select one or more days** in the week that the VKS system can perform auto-upgrade (e.g. Monday, Tuesday, ...).
* **Select a specific time** that you want the VKS system to perform auto-upgrade (e.g. 20:00 (08:00 PM - UTC+07:00 timezone)

<figure><img src="../../.gitbook/assets/vks_autoupgrade1.png" alt=""><figcaption></figcaption></figure>

**Step 5:** Select **Create Kubernetes cluster/ Update Cluster.** Please wait a few minutes for us to create/update your Cluster. The Cluster status at this point will be **Creating/ Updating**.

**Step 6:** When the **Cluster** status is **Active**, the VKS system has completed creating/updating this cluster.

***

## **System operation rules**

### Required Upgrade

On the VKS system, required upgrades include **End-of-Life (EOL) Upgrades, Security Upgrades, Stability Upgrades**. Required Upgrades will be performed **after 8:00 PM** on any necessary day. These upgrades do not follow a fixed schedule but are triggered when the system detects the need to ensure:

* The Cluster is using a Kubernetes version that is still on the supported list.
* Avoid critical issues that could pose security or data risks.

Before performing a Required Upgrade, the system will send you a detailed notification email, including:

* Information about the Cluster/Node Group planned for upgrade.
* Current version and planned upgrade version.
* Planned date and time for the upgrade,...

After the upgrade is complete, the system will send a confirmation email about the cluster status and related changes.

Specifically for the Force Upgrade case, when it detects that your Kubernetes version is about to expire. We will send you notification emails **60 days, 30 days, 7 days, and 1 day** in advance. During this time, you can manually upgrade the Kubernetes version. After this period, if you do not manually upgrade, we will proceed with a force upgrade to the nearest supported Kubernetes version. Depending on your workload, the upgrade process may cause service disruption for varying durations. Please refer to the section below for details.

***

### **Regular Upgrades**

Regular Upgrades include **Minor** and **Patch** upgrades to improve performance, new features, and fix minor bugs in the Kubernetes system. You can configure the Regular Upgrades schedule through **VKS Portal**. The system will try to perform the upgrade in the cluster on the day and time you specified.&#x20;

Before performing a Regular Upgrade, the system will send you a detailed notification email, including:

* Information about the Cluster/Node Group planned for upgrade.
* Current version and planned upgrade version.
* Planned date and time for the upgrade,...

After the upgrade is complete, the system will send a confirmation email about the cluster status and related changes.

Before the system performs the automatic upgrade, if you change the Upgrade Window or perform a manual upgrade, the system will skip this automatic upgrade. In that case, you can ignore the notification email we sent. Depending on your workload, the upgrade process may cause service disruption for varying durations. Please refer to the section below for details.

***

## **Optimizing Upgrade Process and Minimizing Downtime When Upgrading Kubernetes Version**

Upgrading a Kubernetes cluster is an important step to maintain system stability, security, and performance. However, this process can lead to downtime if not done properly. Below are details of common causes of disruption, along with solutions to help you minimize risks during the upgrade process.

When upgrading a cluster, two main components are upgraded:

* **Control Plane (Kubernetes API Server)**: This component is replaced with a new version. During this process, the API server will be unavailable for a few minutes, but workloads will not be affected.
* **Worker Nodes**: These nodes are upgraded via a **rolling update** mechanism, one node at a time in each node group.

Node group upgrade process:

* **Step 1:** The VKS system identifies nodes that need upgrading.
* **Step 2:** The VKS system drains the node, moving all pods running on the old node to other nodes.&#x20;
* **Step 3:** The system creates a new node with the configuration set on the node group and joins it to the cluster. If after restart, the node still reports "NotReady" status, the system will continue restarting the node until it returns to normal operating status.

If **surge upgrades** are enabled, the system will create up to 10 new nodes before starting to upgrade the existing nodes. This ensures workloads have sufficient resources to run throughout the upgrade process.

### **Common Causes of Downtime or Upgrade Failure and Solutions**

* **Pods Without Enough Replicas or Not Deployed via Deployment/StatefulSet:** If a pod does not have enough replicas or is not deployed with Deployment/StatefulSet, when the node containing this pod is upgraded, the service will stop. **Solution:**
  * Ensure critical pods always have replicas >=2.
  * Use Deployment or StatefulSet to automatically manage pods.
* **Pod Disruption Budget (PDB) Configured Too Small:** PDB limits the number of pods that can be disrupted at a time. If configured too small, the upgrade process may hang. **Solution:**
  * Configure PDB appropriately for application requirements (e.g. allow at least 1 pod to always be running).&#x20;
* **Persistent Volume (PV) Not Configured With ReadWriteMany:** PV with `ReadWriteOnce` mode can only be attached to a single node. When this node is upgraded, the PV needs to be moved, causing downtime. **Solution:**
  * Use `ReadWriteMany` mode if the application requires data to be available on multiple nodes.
* **Pods Missing Liveness and Readiness Probes:** Without probes, Kubernetes cannot determine pod status, leading to incorrect routing or downtime. **Solution:**
  * Configure **Liveness Probes** to check if pods are functioning correctly.
  * Configure **Readiness Probes** to ensure traffic is only routed to ready pods.
* **Unbalanced Workload (Affinity/Anti-Affinity):** Overly strict Affinity/Anti-Affinity rules may prevent Kubernetes from finding enough nodes to restart pods. **Solution:**
  * Adjust Affinity/Anti-Affinity rules appropriately.
  * Combine with **surge upgrades** to add temporary resources. **Surge Upgrades** is a feature that creates new nodes before upgrading existing nodes. This ensures workloads have backup resources, speeding up the upgrade process and limiting downtime.

Additionally, for a successful upgrade, you should also consider the following 2 issues:

* **Billing Problem:** When performing an upgrade, the VKS system will drain old nodes and create new nodes before deleting old nodes. Therefore, at the time the system performs the upgrade, cluster costs will temporarily increase. If the credit balance is insufficient, the system cannot create new nodes, causing the upgrade process to be interrupted. **Solution:**
  * Monitor upgrade schedule notifications **via email and prepare sufficient credit balance** for the system to perform the upgrade.
* **Resource Quota Problem:** If the number of nodes you can create exceeds the current quota, the Kubernetes upgrade may be interrupted because new nodes cannot be created. This is especially important when using **Surge Upgrade**, where the system needs to create additional new nodes before deleting old nodes to ensure service continuity. **Solution:**
  * Monitor upgrade schedule notifications **via email and request quota increase if needed.**

If you want to proactively control Kubernetes Cluster upgrades (manually upgrade) and do not want the system to automatically upgrade, you can disable the **Regular Upgrade** feature by unchecking **Enable Automatic Upgrade**.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
