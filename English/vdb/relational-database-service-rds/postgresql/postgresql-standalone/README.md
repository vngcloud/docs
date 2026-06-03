# PostgreSQL Standalone

## Overview

**PostgreSQL Standalone** (Single Node) is a PostgreSQL deployment model on vDB with a **single node**, suitable for development, testing environments, or small applications that do not require High Availability.

### What is PostgreSQL Standalone?

In the Standalone model, all database operations — including reads and writes — are handled by a **single node**:

* **Single Node**: Handles all read and write operations (SELECT, INSERT, UPDATE, DELETE) on the same instance.
* **Simple deployment**: No replication or failover configuration required.
* **Lower cost**: Suitable for workloads that do not require high availability.

### Single Node vs. Cluster Comparison

| Feature               | Single Node                              | Cluster                                                          |
| --------------------- | ---------------------------------------- | ---------------------------------------------------------------- |
| **Architecture**      | 1 single node                            | 1 Writer + N Readers                                             |
| **High Availability** | No                                       | Yes (Automatic Failover)                                         |
| **Scale Read**        | No                                       | Yes (Read traffic distributed to Readers)                        |
| **Backup**            | Automatic daily backup (legacy)          | Integrated with Backup Center (Auto Backup + Manual Backup)      |
| **Number of nodes**   | 1                                        | 2 - 10                                                           |
| **Use Case**          | Development, Testing, small applications | Production, Mission-critical, applications requiring high uptime |

### When should you use PostgreSQL Standalone?

* **Development & Testing**: Environments that do not require high uptime.
* **Small applications**: Applications with low traffic that do not need read scaling.
* **Cost optimization**: When High Availability is not a top priority.

{% hint style="info" %}
**Note:**

* **Single Node** is suitable for **development** and **testing** environments due to simpler configuration and lower cost.
* **Cluster** is recommended for **production** environments when High Availability and fault tolerance are required.
{% endhint %}

***

## Limitations and Notes

{% hint style="info" %}
**About Reserved Usernames:**

When creating an instance, you **must not** use the following usernames as the Master Username as they are reserved by the system: `postgres`, `admin`, `cron_admin`, `robot_zmon`, `vngpooler`, `vngpam`, `vngrep`, `vngsuperrole`.
{% endhint %}

{% hint style="info" %}
**About Deployment Type:**

PostgreSQL Standalone uses the **Single Node** deployment type. If you need High Availability and read scaling, consider using [PostgreSQL Cluster](../postgresql-cluster/README.md).
{% endhint %}

{% hint style="warning" %}
**Deployment Type conversion is not supported:**

vDB currently does not support converting from Standalone to Cluster after an instance has been created. To migrate, you need to create a new PostgreSQL Cluster and [migrate the data](../postgresql-cluster/migrate-from-postgresql-single-to-cluster.md).
{% endhint %}
