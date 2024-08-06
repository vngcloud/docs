# Upgrading Node Group Version

Currently, our VKS system has supported you to upgrade Node Group Version, you can upgrade Node Group Version to:

* **Control Plane Version** (For example upgrade from 1.24 (current Node Group version) to 1.25 (current Control Plane Version), but cannot upgrade to other versions.

**To perform a Node Group Version upgrade, you can follow these instructions:**

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select the **Kubernetes Cluster menu.** Select a **Cluster** where you want to upgrade **Node Group Version** .

**Step 3:** Select the icon ![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762196%2Fimage2024-4-16\_15-51-55.png%3Fversion%3D1%26modificationDate%3D1713258271000%26api%3Dv2\&width=40\&dpr=4\&quality=100\&sign=a9fb64df\&sv=1)and select **Upgrade Node Group Version** to upgrade the node group version.

**Step 4:** You can select the new version for all Node Groups. The new version needs to be valid and compatible with the current version of the cluster. Specifically: you can choose:

* Upgrade Node Group to the same version as Control Plane Version (for example: 1.24 to 1.25)

**Step 5:** The VKS system will upgrade all Node Groups to the Control Plane version. After the upgrade is complete, the Node Group status returns to **ACTIVE** .

{% hint style="info" %}
**Attention:**

* Upgrading Node Group Version is optional and independent of upgrading Control Plane Version. However, all Node Groups in a Cluster will be upgraded at the same time, as well as Control Plane Version and Node Group Version in the same Cluster cannot differ by more than 1 minor version. Besides, the VKS system automatically upgrades the Node Group Version when the current K8S Version being used for your Cluster exceeds the supplier's support period.
* During the Node Group Version upgrade, you cannot perform other actions on your Node Group.
* Below are a few notes before, during and after the upgrade process, please refer to:

**Before getting into work:**

* Check the current version: Visit Releases for a list of supported versions. Select a new version that is valid and compatible with the current version of the cluster.
* Ensure Node Group availability: Node Group must be in ACTIVE status and all nodes must be HEALTHY.
* Stop running tasks: Stop running tasks on the cluster to avoid affecting the upgrade process.

**While doing:**

* Monitor Node Group status: Monitor Node Group status during the upgrade process. Node Group status will change to UPDATING and after completion will return to ACTIVE.
* Check system logs: Check system logs to detect any errors or warnings during the upgrade process.

**After implementation:**

* Check Node Group Availability: Confirm that the Node Group has been upgraded successfully and all nodes are operating normally.
* Test applications: Test applications running on the cluster to ensure they work properly after the upgrade.

**Note:**

* Upgrading Node Group Version may take some time depending on the size and complexity of the Node Group.
* In some rare cases, upgrading Node Group Version may fail. If this happens, the VKS system will automatically rollback the cluster to the current version.
{% endhint %}
