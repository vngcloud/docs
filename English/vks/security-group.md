# Security Group

Security Group acts as a firewall to help you control traffic going in and out of the server (VM). On the VKS system, to ensure the cluster operates safely and effectively, default Security Groups are set up to allow necessary access for the cluster's internal operations. Automatically creating a Security Group simplifies the cluster deployment process and ensures that the cluster is protected from the start. Specifically, when you initialize a Cluser, we will automatically create several Security Groups with the following parameters:

#### The default security group is automatically created for all Clusters <a href="#security-group-mac-dinh-duoc-tao-tu-dong-cho-tat-ca-cluster" id="security-group-mac-dinh-duoc-tao-tu-dong-cho-tat-ca-cluster"></a>

For each Cluster created in the VKS system, we will automatically create a Security Group. This security group will include:

* Inbound:

| Protocol | Ether type | Port range  | Source                                         | Meaning                                                |
| -------- | ---------- | ----------- | ---------------------------------------------- | ------------------------------------------------------ |
| TCP      | IPv4       | 30000-32767 | CIDR of the VPC you use for the Cluster.       | Security group rule used for TCP Node Port Services    |
| UDP      | IPv4       | 30000-32767 | CIDR of the VPC you use for the Cluster.       | Security group rule used for UDP Node Port Services    |
| TCP      | IPv4       | 10250       | External IP of Load Balancer used for Cluster. | Security group rule used for Kubelet API control-plane |
| TCP      | IPv4       | 10250       | CIDR of the VPC you use for the Cluster.       | Security group rule used for Kubelet API control-plane |
| TCP      | IPv4       | 179         | CIDR of the VPC you use for the Cluster.       | Security group rule used for Kubelet API control-plane |
| 4        | IPv4       | 1-65535     | CIDR of the VPC you use for the Cluster.       | Security group rule used for Calico IP-in-IP           |
| TCP      | IPv4       | 5473        | CIDR of the VPC you use for the Cluster.       | Security group rule used for Calico Typha              |

* Outbound

| Protocol | Ether type | Port range | Destination | Meaning                             |
| -------- | ---------- | ---------- | ----------- | ----------------------------------- |
| ANY      | IPv4       | 0-65535    | 0.0.0.0/0   | Default rule of all Security groups |
| ANY      | IPv6       | 0-65535    | ::/0        | Default rule of all Security groups |

#### Security group is automatically created by VNGCLOUD Controller Manager <a href="#security-group-duoc-tao-tu-dong-boi-vngcloud-controller-manager" id="security-group-duoc-tao-tu-dong-boi-vngcloud-controller-manager"></a>

When you use VNGCloud Controller Manager to integrate Network Load Balancer with Cluster on VKS system, we will automatically create a Security Group. This security group will include:

* Inbound:

| Protocol         | Ether type | Port range      | Source                                             |
| ---------------- | ---------- | --------------- | -------------------------------------------------- |
| TCP, UDP or ICMP | IPv4       | Port of Service | Subnet Mask of the Subnet you use for the Cluster. |

* Outbound:

| Protocol | Ether type | Port range | Destination | Meaning                             |
| -------- | ---------- | ---------- | ----------- | ----------------------------------- |
| ANY      | IPv4       | 0-65535    | 0.0.0.0/0   | Default rule of all Security groups |
| ANY      | IPv6       | 0-65535    | ::/0        | Default rule of all Security groups |

#### Security group is automatically created by VNGCLOUD Ingress Controller <a href="#security-group-duoc-tao-tu-dong-boi-vngcloud-ingress-controller" id="security-group-duoc-tao-tu-dong-boi-vngcloud-ingress-controller"></a>

When you use VNGCloud Ingress Controller to integrate Application Load Balancer with Cluster on VKS system, we will automatically create a Security Group. This security group will include:

* Inbound:

| Protocol | Ether type | Port range      | Source                                             |
| -------- | ---------- | --------------- | -------------------------------------------------- |
| TCP      | IPv4       | Port of Service | Subnet Mask of the Subnet you use for the Cluster. |

* Outbound:

| Protocol | Ether type | Port range | Destination | Meaning                             |
| -------- | ---------- | ---------- | ----------- | ----------------------------------- |
| ANY      | IPv4       | 0-65535    | 0.0.0.0/0   | Default rule of all Security groups |
| ANY      | IPv6       | 0-65535    | ::/0        | Default rule of all Security groups |

{% hint style="info" %}
**Attention:**

* Default Security Groups are set up to meet the basic security needs of the cluster. If you edit or delete the Security Groups created for the cluster, it may result in connectivity and access issues between nodes in the cluster or the cluster may not function correctly or may not even start. To ensure the stability and security of the cluster, the system will automatically reset Security Groups to default settings after every fixed period of time.
{% endhint %}
