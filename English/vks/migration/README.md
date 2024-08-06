# Migration

## Overview <a href="#tong-quan" id="tong-quan"></a>

Migration from one cluster to another is the process of moving data, applications, and services from one set of servers to another. The purpose of this is often to upgrade the system, increase availability and fault tolerance, or to scale the system.

***

## Model <a href="#mo-hinh-tong-quan" id="mo-hinh-tong-quan"></a>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FrqUCZk2auMT2E23qE8TT%252Fimage.png%3Falt%3Dmedia%26token%3Dd7dfd2a6-af47-4f71-b99f-cd63669f1300&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6205a9ec&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

## Implementation steps <a href="#cac-buoc-thuc-hien" id="cac-buoc-thuc-hien"></a>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FLzNoxY4RIf5sLt2IOlnV%252Fimage.png%3Falt%3Dmedia%26token%3D9bce3f24-3669-4bec-b565-52d147d84a04&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=3aac57d1&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Specifically:

* **Step 1:** Prepare target cluster (Prepard target resource): on the VKS system, you need to initialize a Cluster according to the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/clusters) . Make sure that the destination cluster's configuration is the same as the source cluster's configuration.
* **Step 2 \[Optional]** : If your cluster has private resources such as images, databases, storage... Now, before starting to migrate, you need to **proactively** migrate these resources yourself.
* **Step 3** : Install Velero on both source and destination clusters (Install Velero tool): after you have migrated private resources outside the cluster, you can use the migration tool to backup and restore. Restore the application on the source cluster and target cluster.
* **Step 4** : Backup: To back up resources, use the Velero tool to create a backup object in the source cluster. Velero will perform queries, package the data, and upload them to an S3 Compatible Object Storage.
* **Step 5** : Restore: During the restore process at the destination cluster, Velero will download backup data to the new cluster and redeploy resources based on the JSON file.
* **Step 6 \[Optional]** : Update resource config: After the target cluster's resources are deployed properly, you can **switch traffic** for your service. After confirming that all services are running properly, you can delete the source cluster.

Below are detailed instructions for common cases when you migrate workloads from one Cluster to another. You can refer to and follow the instructions at:

* [Migrate Cluster from VKS to VKS](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/migration/migrate-cluster-from-vks-to-vks)
* [Migrate Cluster from vContainer to VKS](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/migration/migration-cluster-from-vcontainer-to-vks)
* [Migrate Cluster from another platform to VKS](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/migration/migrate-cluster-from-other-to-vks)
