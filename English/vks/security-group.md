# Security Group

Security Groups play a crucial role in safeguarding Kubernetes clusters by controlling inbound and outbound traffic to and from the cluster's nodes. VKS, the Kubernetes service on VNG Cloud, implements default Security Groups to ensure the secure and efficient operation of clusters. These default Security Groups are automatically created during cluster initialization, simplifying the deployment process and providing initial protection for the cluster.

### **Default Security Groups in VKS Clusters**

When you create a cluster on VKS, two default Security Groups are automatically created:

* Inbound:

<table><thead><tr><th width="114">Protocol</th><th width="83">Ether type</th><th width="140">Port range</th><th width="215">Source</th><th>Description</th></tr></thead><tbody><tr><td>TCP</td><td>IPv4</td><td>30000-32767</td><td>The CIDR of the VPC used for your Cluster</td><td>Security group rule used for TCP Node Port Services</td></tr><tr><td>UDP</td><td>IPv4</td><td>30000-32767</td><td>The CIDR of the VPC used for your Cluster</td><td>Security group rule used for UDP Node Port Services</td></tr><tr><td>TCP</td><td>IPv4</td><td>10250</td><td>The External IP of a Load Balancer used for your Cluster.</td><td>Security group rule used for Kubelet API control-plane</td></tr><tr><td>TCP</td><td>IPv4</td><td>10250</td><td>The CIDR of the VPC used for your Cluster</td><td>Security group rule used for Kubelet API control-plane</td></tr><tr><td>TCP</td><td>IPv4</td><td>179</td><td>The CIDR of the VPC used for your Cluster</td><td>Security group rule used for Kubelet API control-plane</td></tr><tr><td>4</td><td>IPv4</td><td>1-65535</td><td>The CIDR of the VPC used for your Cluster</td><td>Security group rule used for Calico IP-in-IP</td></tr><tr><td>TCP</td><td>IPv4</td><td>5473</td><td>The CIDR of the VPC used for your Cluster</td><td>Security group rule used for Calico Typha</td></tr></tbody></table>

* Outbound

<table><thead><tr><th width="114">Protocol</th><th width="131">Ether type</th><th width="126">Port range</th><th width="125">Destination</th><th>Description</th></tr></thead><tbody><tr><td>ANY</td><td>IPv4</td><td>0-65535</td><td>0.0.0.0/0</td><td>Default rule of all Security group</td></tr><tr><td>ANY</td><td>IPv6</td><td>0-65535</td><td>::/0</td><td>Default rule of all Security group</td></tr></tbody></table>

### Automatically created using VNGCLOUD Controller Manager

When you integrate Network Load Balancer (NLB) with your Kubernetes cluster on VKS using VNGCloud Controller Manager, a Security Group is automatically created to facilitate secure communication between the NLB and the cluster components. Key Features of the Automatically Created Security Group:

* Inbound:

<table><thead><tr><th width="207">Protocol</th><th width="108">Ether type</th><th>Port range</th><th>Source</th></tr></thead><tbody><tr><td>TCP, UDP hoặc ICMP</td><td>IPv4</td><td>Port của Service</td><td>The Subnet Mask of the Subnet used for your Cluster.</td></tr></tbody></table>

* Outbound:

<table><thead><tr><th width="113">Protocol</th><th width="115">Ether type</th><th width="126">Port range</th><th width="127">Destination</th><th>Description</th></tr></thead><tbody><tr><td>ANY</td><td>IPv4</td><td>0-65535</td><td>0.0.0.0/0</td><td>Default rule of all Security group</td></tr><tr><td>ANY</td><td>IPv6</td><td>0-65535</td><td>::/0</td><td>Default rule of all Security group</td></tr></tbody></table>

### Automatically created using VNGCLOUD Ingress Controller

When you integrate Application Load Balancer (ALB) with your Kubernetes cluster on VKS using VNGCloud Ingress Controller, a Security Group is automatically created to facilitate secure communication between the ALB and the cluster components. Key Features of the Automatically Created Security Group:

* Inbound:

<table><thead><tr><th width="141">Protocol</th><th width="117">Ether type</th><th>Port range</th><th>Source</th></tr></thead><tbody><tr><td>TCP</td><td>IPv4</td><td>Port of Service</td><td>The Subnet Mask of the Subnet used for your Cluster.</td></tr></tbody></table>

* Outbound:

<table><thead><tr><th width="105">Protocol</th><th width="109">Ether type</th><th width="122">Port range</th><th width="162">Destination</th><th>Description</th></tr></thead><tbody><tr><td>ANY</td><td>IPv4</td><td>0-65535</td><td>0.0.0.0/0</td><td>Default rule of all Security group</td></tr><tr><td>ANY</td><td>IPv6</td><td>0-65535</td><td>::/0</td><td>Default rule of all Security group</td></tr></tbody></table>

{% hint style="info" %}
**Note:**

* Default Security Groups are set up to meet the basic security needs of the cluster. If you edit or delete the Security Groups created for the cluster, it may result in connectivity and access issues between nodes in the cluster or the cluster may not function correctly or may not even start. To ensure the stability and security of the cluster, the system will automatically reset Security Groups to default settings after every fixed period of time.
{% endhint %}
