# Multi-AZ Control Plane

## Overview

**Multi-AZ Control Plane** is a feature that allows deploying a Kubernetes Cluster with the Control Plane distributed across multiple Availability Zones (AZ), ensuring **High Availability** (HA) for your cluster.

### What is Multi-AZ Control Plane?

In the Multi-AZ model, the Control Plane components (API Server, Controller Manager, Scheduler, etcd) are deployed across multiple AZs. This ensures that:

* If one AZ experiences an outage, the Control Plane continues to operate normally from the remaining AZs
* Automatic failover without manual intervention
* Meets compliance requirements for disaster recovery

To create a Multi-AZ Cluster, please refer to the guide [here](../bat-dau-voi-vks/create-a-multi-az-cluster.md).

### Comparison between Single-AZ and Multi-AZ Cluster

| Feature | Single-AZ | Multi-AZ |
| --- | --- | --- |
| **Control Plane Availability** | 99.9% | 99.99% |
| **Fault Tolerance** | Single point of failure at AZ level | Tolerates AZ-level failures |
| **Cost** | Lower | Free during initial release phase (Private Service Endpoints cost applies) |
| **Latency** | Low (same AZ) | Slightly higher (cross-AZ for Control Plane) |
| **Private DNS (VPC)** | Optional | Required (prerequisite) |
| **Use Case** | Development, Testing | Production, Mission-critical |
| **Subnet Requirement** | 1 subnet | Minimum 2 subnets from 2 different AZs |
| **Node Group** | 1 AZ (1 subnet) | 1 AZ per Node Group (select 1 subnet from the cluster's subnet list) |

### When should you use Multi-AZ Cluster?

* **Production workloads**: Applications that require high uptime and cannot tolerate downtime
* **Mission-critical applications**: Payment systems, transactions, critical data
* **Enterprise requirements**: Compliance with disaster recovery requirements
* **High Availability**: When you need to ensure the cluster remains operational even if an AZ experiences an outage

{% hint style="info" %}
**Note:**

* **Single-AZ Cluster** is suitable for **development** and **testing** environments due to lower cost
* **Multi-AZ Cluster** is recommended for **production** environments
{% endhint %}

***

## Multi-AZ Control Plane Architecture

The diagram below illustrates the architecture of a Multi-AZ Cluster:

<figure><img src="../../.gitbook/assets/vks-multi-az-architecture.png.png" alt=""><figcaption><p>Multi-AZ Control Plane Architecture</p></figcaption></figure>

**Key components:**

* **Control Plane**: Distributed across multiple AZs, including API Server, Controller Manager, Scheduler, etcd
* **etcd cluster**: Replicated across AZs to ensure data consistency
* **vLB Multi-AZ**: Load Balancer that distributes traffic to Control Plane nodes across AZs
* **Node Groups**: Each Node Group is deployed in only 1 subnet (1 AZ), users can create multiple Node Groups in different AZs

***

## Managing Multi-AZ Cluster

### Viewing Cluster information on the list page

On the Kubernetes Cluster list page, you can identify Multi-AZ Clusters through the **Control Plane Availability** column:

<figure><img src="../../.gitbook/assets/vks-multi-az-cluster-list-page.png" alt=""><figcaption><p>Cluster List Page with Control Plane Availability column</p></figcaption></figure>

| Badge | Meaning |
| --- | --- |
| **Single-AZ** (gray badge) | Control Plane is in 1 AZ |
| **Multi-AZ** (dark blue badge) | Control Plane is distributed across multiple AZs |

### Viewing Cluster details

When accessing the detail page of a Multi-AZ Cluster:

**1. General Information**

Displays an additional **Control Plane Availability** field with the value **Multi-AZ** (dark blue badge)

<figure><img src="../../.gitbook/assets/vks-multi-az-cluster-detail-general-info.png" alt=""><figcaption><p>General Information with Control Plane Availability</p></figcaption></figure>

**2. Network Section**

Displays the list of **Subnets** in use with detailed information:

```
Subnets (2)
├── sub-85ba01f6-02ec-4dfc-8884-ee0036c68a5b
│   Name: sub-1A (10.60.0.0/24) | AZ: HCM-1A
└── sub-12345678-abcd-efgh-ijkl-mnopqrstuvwx
    Name: sub-1B (10.60.1.0/24) | AZ: HCM-1B
```

* Click the **copy** icon next to the Subnet ID to copy it to clipboard

<figure><img src="../../.gitbook/assets/vks-multi-az-cluster-detail-network.png" alt=""><figcaption><p>Network section with Subnets list</p></figcaption></figure>

**3. Node Group Tab**

The Node Group details display **Subnet** along with the corresponding **AZ**, helping you identify which AZ the Node Group is deployed in.

### Upgrade Control Plane

The Control Plane upgrade process for Multi-AZ Cluster is **the same** as for Single-AZ Cluster:

1. Navigate to the cluster detail page
2. Upgrade the Control Plane to a new version following the guide [here](upgrading-control-plane-version.md)

{% hint style="info" %}
**Multi-AZ Cluster upgrade characteristics:**

* The system performs a **rolling upgrade** across all AZs
* The cluster remains **available** during the upgrade
* Existing workloads are **not interrupted**
* If the upgrade fails, the system automatically **rolls back** to the previous version
{% endhint %}

### Delete Cluster

The process for deleting a Multi-AZ Cluster is **similar** to a Single-AZ Cluster:

1. Navigate to [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console.vngcloud.vn/k8s-cluster)
2. Select the cluster you want to delete and choose **Delete**
3. Confirm the deletion

{% hint style="warning" %}
**Notes when deleting a Multi-AZ Cluster:**

When deleting a cluster, the system will:
* Delete all **Control Plane components** across **all AZs**
* Delete all **Node Groups** and **Worker Nodes**
* Release **network resources** (subnets will remain in the VPC)
* Delete the cluster's default **Security Group**
* Delete the cluster's default **Load Balancer**

The following resources **may not be automatically deleted**:
* Load Balancers integrated into the cluster by you
* Persistent Volumes integrated into the cluster by you
{% endhint %}

***

## Limitations and Notes

### Current Limitations

| Limitation | Description |
| --- | --- |
| **Cannot convert** | Cannot convert a cluster from Single-AZ to Multi-AZ (or vice versa) after creation |
| **Cannot change subnets** | Cannot add/remove subnets after creating a Multi-AZ cluster |
| **Node Group remains Single-AZ** | Each Node Group only supports deployment in 1 subnet (1 AZ) |
| **VPC DNS required** | VPC must have DNS enabled to create a Multi-AZ Cluster |

### Important Notes

{% hint style="success" %}
**Regarding cost:**

During the initial release phase, the Multi-AZ Control Plane feature is provided **free of charge**. Official pricing will be updated in the future. Please follow the [Announcements and Updates](../thong-bao-va-cap-nhat/) page for the latest information.

Note: Multi-AZ Cluster operates on a private flow, so there will be additional costs for **4 Private Service Endpoints** (IAM, vCR, vServer, vStorage).
{% endhint %}

{% hint style="warning" %}
**Regarding Private Service Endpoints:**

* Multi-AZ Cluster operates on a **private flow**, the system automatically creates 4 Private Service Endpoints when the cluster is created
* **Do not delete** these endpoints to avoid service disruption
* Nodes in the cluster **cannot connect to the internet** to pull images — you must use **vContainer Registry (vCR)**
* To access the **kube-api**, you must be **within the VPC** that the cluster uses
* For details, refer to [Create a Multi-AZ Cluster](../bat-dau-voi-vks/create-a-multi-az-cluster.md)
{% endhint %}

{% hint style="info" %}
**Regarding Node Groups:**

* When creating a cluster, the first Node Group can only select 1 subnet from the list of subnets configured for the cluster
* To ensure HA for workloads, you should create additional Node Groups in other AZs after the cluster is created
{% endhint %}

{% hint style="info" %}
**Regarding cross-AZ latency:**

Traffic between AZs may have slightly higher latency compared to traffic within the same AZ. This is normal and is an acceptable trade-off for High Availability.
{% endhint %}

***

## FAQ

### 1. Can I convert a cluster from Single-AZ to Multi-AZ?

**No.** Currently, VKS does not support changing the Control Plane Availability after a cluster has been created. You need to create a new cluster with Multi-AZ configuration.

### 2. Will my Node Group automatically be distributed across multiple AZs?

**No.** Each Node Group is deployed in only 1 AZ (1 subnet). To distribute workloads across multiple AZs, you need to create multiple Node Groups in different AZs.

### 3. What happens when an AZ experiences an outage?

When 1 AZ experiences an outage:
* **Control Plane** continues to operate normally from the remaining AZs
* **Node Groups** in that AZ will not be available
* Kubernetes will automatically reschedule pods to nodes in other AZs (if Node Groups exist in other AZs)

### 4. Why is my VPC not displayed when creating a Multi-AZ Cluster?

Your VPC does not have **DNS** enabled. Please enable DNS for your VPC in the vServer portal before creating a Multi-AZ Cluster.

### 5. Can I select multiple subnets from the same AZ for a Multi-AZ Cluster?

You can select multiple subnets, but you must ensure the subnets belong to **at least 2 different AZs**. If all subnets belong to the same AZ, the system will display a validation error.

### 6. How much does a Multi-AZ Cluster cost?

During the initial release phase, the Multi-AZ Control Plane feature is provided **free of charge**. Official pricing will be updated in the future. Note that Multi-AZ Cluster operates on a private flow, so there will be additional costs for 4 Private Service Endpoints. Please refer to the [Pricing](../cach-tinh-gia.md) and [Announcements and Updates](../thong-bao-va-cap-nhat/) pages for details.
