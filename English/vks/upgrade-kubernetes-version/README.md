# Upgrade Kubernetes Version

## Manually Upgrade

**Manually Upgrade** is the process of immediately upgrading manually as specified by you on the VKS system. Specifically, the VKS system supports upgrading Control Plane Version or Node Group Version in the following cases:

* Upgrade to a newer **Minor Version** (e.g. 1.24 to 1.25)
* Upgrade to a newer **Patch Version** (e.g. 1.24.2-VKS.100 to 1.24.5-VKS.200)

## **Automatically Upgrade**

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
* **Specifically**:
  * **Minor Version Upgrades**: Update new features and APIs. For example, if the current cluster is using version 1.28.2, the system will automatically upgrade to version 1.29.6.
  * **Patch Version Upgrades**: Fix minor bugs and improve performance. For example, if the current cluster is using version 1.29.1, the system will automatically upgrade to version 1.29.2.
* **Execution time**:
  * You can configure the upgrade schedule through **VKS Portal** following the guide below. After you select the auto-upgrade schedule via VKS Portal, the system will **start the upgrade after at least** <mark style="color:red;">**6 days**</mark> from the current date. This time allows you to prepare and test before the upgrade takes place.
  * The system will **repeat for subsequent weeks** from the previous upgrade and follow the days you selected.
  * **Before each upgrade**, the system will send a **notification email** 6 days before the actual auto-upgrade time. In the email, we will specify the exact time the auto-upgrade will take place.
  * If you **select multiple days in the week** (such as Monday, Thursday), the system will calculate the upgrade cycle for the selected days, without affecting other days.

For details, please refer to [Automatically Upgrade](automatically-upgrade.md).
