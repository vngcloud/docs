# PostgreSQL Cluster

## Overview

**PostgreSQL Cluster** is a feature that enables deploying PostgreSQL with a **1 Writer (Primary) + N Readers (Replica)** architecture, ensuring **High Availability** and the ability to **scale read** operations for production workloads on vDB.

### What is PostgreSQL Cluster?

In the PostgreSQL Cluster model, nodes are assigned clear roles:

* **Writer (Primary)**: The node that handles all write operations (INSERT, UPDATE, DELETE). Each cluster always has exactly **1 Writer**.
* **Reader (Replica)**: Read-only nodes that synchronize data from the Writer via **Streaming Replication**. A cluster can have from **1 to 9 Readers**.
* **Automatic Failover**: When the Writer encounters an issue, a Reader is **automatically promoted** to Writer without manual intervention.

To create and manage a PostgreSQL Cluster, please refer to the guide [here](create-and-manage-postgresql-cluster.md).

### Single Node vs. Cluster Comparison

| Feature               | Single Node                              | Cluster                                                          |
| --------------------- | ---------------------------------------- | ---------------------------------------------------------------- |
| **Architecture**      | 1 single node                            | 1 Writer + N Readers                                             |
| **High Availability** | No                                       | Yes (Automatic Failover)                                         |
| **Scale Read**        | No                                       | Yes (Read traffic distributed to Readers)                        |
| **Backup**            | Automatic daily backup (legacy)          | Integrated with Backup Center (Auto Backup + Manual Backup)      |
| **Number of nodes**   | 1                                        | 2 - 10                                                           |
| **Use Case**          | Development, Testing, small applications | Production, Mission-critical, applications requiring high uptime |

### When should you use PostgreSQL Cluster?

* **Production workloads**: Applications requiring high uptime that cannot tolerate downtime.
* **Read-heavy applications**: Applications with heavy read traffic that need to scale out read operations.
* **Mission-critical systems**: Payment systems, transactions, and critical data that need protection by automatic failover.
* **Data protection**: Applications requiring a comprehensive backup strategy with Auto Backup and Manual Backup through Backup Center.

{% hint style="info" %}
**Note:**

* **Single Node** is suitable for **development** and **testing** environments due to simpler configuration and lower cost.
* **Cluster** is recommended for **production** environments when High Availability and fault tolerance are required.
{% endhint %}

***

## PostgreSQL Cluster Architecture

<figure><img src="../../../.gitbook/assets/vDB Postgres Cluster Architecture Diagram.png" alt=""><figcaption></figcaption></figure>

**Key components:**

* **Writer Node (Primary)**: Handles all write operations. Each cluster has exactly 1 Writer.
* **Reader Node(s) (Replica)**: Handle read operations, synchronizing data from the Writer via Streaming Replication. Provide failover capability when the Writer encounters an issue.
* **Automatic Failover**: When the Writer node becomes unavailable, the system automatically promotes a Reader to become the new Writer, ensuring service continuity.

**Role distribution by number of nodes:**

| Number of Nodes | Role Distribution    |
| --------------- | -------------------- |
| 2               | 1 Writer + 1 Reader  |
| 3               | 1 Writer + 2 Readers |
| 5               | 1 Writer + 4 Readers |
| 10              | 1 Writer + 9 Readers |

***

## Backup Center Integration

PostgreSQL Cluster is integrated with **Backup Center (vBackup)**, providing a comprehensive backup & restore solution:

* **Auto Backup**: Mandatory configuration when creating a cluster. Backup runs automatically according to the schedule of the selected Backup Policy.
* **Manual Backup**: Allows creating a **Full Snapshot** manually at any time from the cluster detail page.
* **Restore**: Create a new cluster from an available restore point in Backup Center. The Storage Size of the new cluster must be greater than or equal to the Backup Size.

{% hint style="warning" %}
**Note about Backup when deleting a Cluster:**

* **Auto Backup**: Will be **automatically deleted** when the cluster is deleted.
* **Manual Backup**: Will be **retained** after the cluster is deleted. You need to manually manage and delete it in Backup Center if no longer needed.
{% endhint %}

***

## Limitations and Notes

### Current Limitations

| Limitation             | Description                                              |
| ---------------------- | -------------------------------------------------------- |
| **Number of nodes**    | Minimum 2, maximum 10 nodes per cluster                  |
| **Writer node**        | Always exactly 1 Writer per cluster                      |
| **Database Proxy**     | Not supported in current version (Coming Soon - Phase 2) |
| **Concurrent backups** | Only 1 backup/restore job allowed at a time per cluster  |

### Important Notes

{% hint style="info" %}
**About Reserved Usernames:**

When creating a cluster, you **must not** use the following usernames as the Master Username as they are reserved by the system: `postgres`, `admin`, `cron_admin`, `robot_zmon`, `vngpooler`, `vngpam`, `vngrep`, `vngsuperrole`.
{% endhint %}

{% hint style="info" %}
**About Deployment Type:**

The PostgreSQL Cluster feature is only available when selecting **PostgreSQL** as the Engine. Other engines (MySQL, MariaDB) currently only support the **Single Node** deployment type.
{% endhint %}

***

## FAQ

### 1. Can I switch from Single Node to Cluster?

**No.** vDB currently does not support changing the Deployment Type after a database has been created. You need to create a new cluster and migrate the data.

### 2. What happens when the Writer node encounters an issue?

When the Writer node encounters an issue, the system will **automatically failover**: a Reader node will be promoted to become the new Writer. This process happens automatically without manual intervention. The UI will update the role of the nodes after the failover is complete.

### 3. Can I create a cluster from an existing backup?

**Yes.** When creating a new cluster, you can select a restore point from Backup Center to restore data. Note that the Storage Size of the new cluster must be greater than or equal to the Backup Size of the backup.

### 4. What is Database Proxy and when will it be available?

Database Proxy provides connection pooling and load balancing for the cluster. This feature is under development and will be released in **Phase 2**. Please follow the [Announcements and Updates](../../announcements/release-notes.md) page for the latest information.
