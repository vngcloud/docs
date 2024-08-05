# Migration

### Overview

Migration from one cluster to another is the process of transferring data, applications, and services from one group of servers to another. The purpose of this is usually to upgrade the system, enhance availability and fault tolerance, or to scale the system.

***

### How it works?

**Step 1: Prepare the Target Cluster**

On the VKS system, you need to create a new Cluster following the instructions here. Ensure that the configuration of the target cluster matches the source cluster.

#### Step 2 \[Optional]: Migrate Private Resources

If your cluster has private resources such as images, databases, or storage, you need to manually migrate these resources before starting the migration process.

#### Step 3: Install Velero on Both Clusters

After migrating any private resources outside the cluster, you can use the Velero migration tool to backup and restore applications between the source and target clusters.

#### Step 4: Backup

To back up resources, use Velero to create a backup object in the source cluster. Velero will query, package, and upload the data to an S3-compatible object storage.

#### Step 5: Restore

During the restore process on the target cluster, Velero will download the backup data to the new cluster and redeploy the resources based on the JSON file.

#### Step 6 \[Optional]: Update Resource Config

Once the resources on the target cluster are deployed successfully, you can switch the traffic for your services. After confirming that all services are running normally, you can delete the source cluster.
