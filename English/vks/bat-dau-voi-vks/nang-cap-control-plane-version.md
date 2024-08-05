# Upgrading Control Plane Version

Currently, our VKS system has supported you to upgrade Control Plane Version, you can:

* Upgrade to a newer **Minor Version** (e.g. 1.24 to 1.25)
* Upgrade to a newer **Patch Version (for example: 1.24.2-VKS.100 to 1.24.5-VKS.200)**

**To upgrade the Control Plane version, you can follow these instructions:**

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select the **Kubernetes Cluster menu.**

**Step 3:** Select the icon ![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762076%2Fimage2024-4-16\_15-51-55.png%3Fversion%3D1%26modificationDate%3D1713257518000%26api%3Dv2\&width=40\&dpr=4\&quality=100\&sign=25aa6095\&sv=1)and select **Upgrade control plane version** to upgrade the control plane version.

**Step 4:** You can select a new version for the control plane. The new version needs to be valid and compatible with the current version of the cluster. Specifically: you can choose:

* Upgrade to a newer Minor Version (e.g. 1.24 to 1.25)
* Upgrade to a newer Patch Version (for example: 1.24.2-VKS.100 to 1.24.5-VKS.200)

**Step 4:** The VKS system will upgrade the Control Plane components of the Cluster to the new version. After the upgrade is complete, the Cluster status returns to **ACTIVE** .

Attention:

* Upgrading Control Plane Version is optional and independent of upgrading Node Group Version. However, Control Plane Version and Node Group Version in the same Cluster cannot differ by more than 1 minor version. Besides, the VKS system automatically upgrades Control Plane Version when the current K8S Version used for your Cluster exceeds the supplier's support period.
* During the Control Plane Version upgrade, you cannot perform other actions on your Cluster.
* Below are a few notes before, during and after the upgrade process, please refer to:

**Before getting into work:**

* Back up data: You should back up cluster data before upgrading to ensure safety in case the upgrade fails.
* Check the current version: Visit Releases for a list of supported versions. Select a new version that is valid and compatible with the current version of the cluster.
* Ensure cluster availability: Cluster must be in ACTIVE status and all nodes must be HEALTHY.
* Stop running tasks: Stop running tasks on the cluster to avoid affecting the upgrade process.

**While doing:**

* Monitor cluster status: Monitor cluster status during the upgrade process. The cluster status will change to UPDATING and after completion will return to ACTIVE.
* Check system logs: Check system logs to detect any errors or warnings during the upgrade process.

**After implementation:**

* Check cluster availability: Confirm that the cluster has been upgraded successfully and all nodes are operating normally.
* Test applications: Test applications running on the cluster to ensure they work properly after the upgrade.

**Note:**

* Upgrading Control Plane Version may take some time depending on the size and complexity of the cluster.
* In some rare cases, the Control Plane Version upgrade may fail. If this happens, the VKS system will automatically rollback the cluster to the current version.
