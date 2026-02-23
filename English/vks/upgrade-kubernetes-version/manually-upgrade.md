# Manually Upgrade

## Upgrading Control Plane Version

Currently, the VKS system supports upgrading Control Plane Version. You can:

* Upgrade to a newer **Minor Version** (e.g. 1.24 to 1.25)
* Upgrade to a newer **Patch Version** (e.g. 1.24.2-VKS.100 to 1.24.5-VKS.200)

**To upgrade the Control Plane version, follow these instructions:**&#x20;

**Step 1:** Go to [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** On the **Overview** screen, select the **Kubernetes Cluster** menu.

**Step 3:** Select the icon <img src="https://docs-admin.vngcloud.vn/download/thumbnails/73762076/image2024-4-16_15-51-55.png?version=1&#x26;modificationDate=1713257518000&#x26;api=v2" alt="" data-size="line"> and select **Upgrade control plane version** to upgrade the control plane version.

**Step 4:** You can select a new version for the control plane. The new version must be valid and compatible with the current cluster version. Specifically, you can choose:

* Upgrade to a newer Minor Version (e.g. 1.24 to 1.25)
* Upgrade to a newer Patch Version (e.g. 1.24.2-VKS.100 to 1.24.5-VKS.200)

**Step 4:** The VKS system will upgrade the Control Plane components of the Cluster to the new version. After the upgrade is complete, the Cluster status returns to **ACTIVE**.&#x20;

{% hint style="info" %}
**Note:**

* Upgrading Control Plane Version is not mandatory and is independent of upgrading Node Group Version. However, the Control Plane Version and Node Group Version in the same Cluster must not differ by more than 1 minor version. Additionally, the VKS system automatically upgrades the Control Plane Version when the Kubernetes Version currently used by your Cluster has exceeded the supported period.
* During Control Plane Version upgrade, you cannot perform other actions on your Cluster.&#x20;
* Below are some notes before, during, and after the upgrade process:&#x20;

**Before upgrading:**

* Back up data: You should back up your cluster data before upgrading to ensure safety in case the upgrade fails.
* Check current version: Visit Releases to see the list of supported versions. Select a new version that is valid and compatible with the current cluster version.
* Ensure cluster availability: Cluster must be in ACTIVE status and all nodes must be HEALTHY.
* Stop running tasks: Stop running tasks on the cluster to avoid affecting the upgrade process.

**During upgrade:**

* Monitor cluster status: Monitor cluster status during the upgrade process. The cluster status will change to UPDATING and after completion will return to ACTIVE.
* Check system logs: Check system logs to detect any errors or warnings during the upgrade process.

**After upgrade:**

* Verify cluster availability: Confirm that the cluster has been successfully upgraded and all nodes are operating normally.
* Check applications: Check applications running on the cluster to ensure they are working normally after the upgrade.

**Notes:**

* Upgrading Control Plane Version may take some time depending on the size and complexity of the cluster.
* In some rare cases, the Control Plane Version upgrade may fail. If this happens, the VKS system will automatically rollback the cluster to the current version.
{% endhint %}

***

## Upgrading Node Group Version

Currently, the VKS system supports upgrading Node Group Version. You can upgrade Node Group Version to:

* **Control Plane Version** (For example, upgrade from 1.24 (current Node Group version) to 1.25 (current Control Plane Version), but cannot upgrade to other versions.

**To upgrade the Node Group Version, follow these instructions:**&#x20;

**Step 1:** Go to [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** On the **Overview** screen, select the **Kubernetes Cluster** menu. Select a **Cluster** for which you want to upgrade the **Node Group Version**.

**Step 3:** Select the icon <img src="https://docs-admin.vngcloud.vn/download/thumbnails/73762196/image2024-4-16_15-51-55.png?version=1&#x26;modificationDate=1713258271000&#x26;api=v2" alt="" data-size="line"> and select **Upgrade Node Group Version** to upgrade the node group version.

**Step 4:** You can select a new version for all Node Groups. The new version must be valid and compatible with the current cluster version. Specifically, you can choose:

* Upgrade Node Group to match the Control Plane Version (e.g. 1.24 to 1.25)

**Step 5:** The VKS system will upgrade all Node Groups to the Control Plane version. After the upgrade is complete, the Node Group status returns to **ACTIVE**.&#x20;

{% hint style="info" %}
**Note:**

* Upgrading Node Group Version is not mandatory and is independent of upgrading Control Plane Version. However, all Node Groups in a Cluster will be upgraded at the same time, and the Control Plane Version and Node Group Version in the same Cluster must not differ by more than 1 minor version. Additionally, the VKS system automatically upgrades the Node Group Version when the Kubernetes Version currently used by your Cluster has exceeded the supported period.
* During Node Group Version upgrade, you cannot perform other actions on your Node Group.&#x20;
* Below are some notes before, during, and after the upgrade process:&#x20;

**Before upgrading:**

* Check current version: Visit Releases to see the list of supported versions. Select a new version that is valid and compatible with the current cluster version.
* Ensure Node Group availability: Node Group must be in ACTIVE status and all nodes must be HEALTHY.
* Stop running tasks: Stop running tasks on the cluster to avoid affecting the upgrade process.

**During upgrade:**

* Monitor Node Group status: Monitor Node Group status during the upgrade process. The Node Group status will change to UPDATING and after completion will return to ACTIVE.
* Check system logs: Check system logs to detect any errors or warnings during the upgrade process.

**After upgrade:**

* Verify Node Group availability: Confirm that the Node Group has been successfully upgraded and all nodes are operating normally.
* Check applications: Check applications running on the cluster to ensure they are working normally after the upgrade.

**Notes:**

* Upgrading Node Group Version may take some time depending on the size and complexity of the Node Group.
* In some rare cases, the Node Group Version upgrade may fail. If this happens, the VKS system will automatically rollback the cluster to the current version.
{% endhint %}
