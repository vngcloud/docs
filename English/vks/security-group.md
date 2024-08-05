# Security Group

Security Group acts as a firewall to help you control traffic in and out of the server (VM). On the VKS system, to ensure the cluster operates safely and efficiently, default Security Groups are set up to allow access necessary for the internal operation of the cluster. Automatically creating Security Groups simplifies the cluster deployment process and ensures that the cluster is protected from the start. Specifically, when you initialize a Cluser, we will automatically initialize a few Security Groups with the following parameters:

### Default Security group is automatically created for all Clusters&#x20;

For each Cluster created in the VKS system, we will automatically create a Security Group. This Security group will include:

* Inbound:

<table><thead><tr><th width="114">Protocol</th><th width="83">Ether type</th><th width="140">Port range</th><th width="215">Source</th><th>Ý nghĩa</th></tr></thead><tbody><tr><td>TCP</td><td>IPv4</td><td>30000-32767</td><td>CIDR của VPC mà bạn sử dụng cho Cluster.</td><td>Security group rule sử dụng cho TCP Node Port Services</td></tr><tr><td>UDP</td><td>IPv4</td><td>30000-32767</td><td>CIDR của VPC mà bạn sử dụng cho Cluster.</td><td>Security group rule sử dụng cho UDP Node Port Services</td></tr><tr><td>TCP</td><td>IPv4</td><td>10250</td><td>External IP của Load Balancer sử dụng cho Cluster.</td><td>Security group rule sử dụng cho Kubelet API control-plane</td></tr><tr><td>TCP</td><td>IPv4</td><td>10250</td><td>CIDR của VPC mà bạn sử dụng cho Cluster.</td><td>Security group rule sử dụng cho Kubelet API control-plane</td></tr><tr><td>TCP</td><td>IPv4</td><td>179</td><td>CIDR của VPC mà bạn sử dụng cho Cluster.</td><td>Security group rule sử dụng cho Kubelet API control-plane</td></tr><tr><td>4</td><td>IPv4</td><td>1-65535</td><td>CIDR của VPC mà bạn sử dụng cho Cluster.</td><td>Security group rule sử dụng cho Calico IP-in-IP</td></tr><tr><td>TCP</td><td>IPv4</td><td>5473</td><td>CIDR của VPC mà bạn sử dụng cho Cluster.</td><td>Security group rule sử dụng cho Calico Typha</td></tr></tbody></table>

* Outbound

<table><thead><tr><th width="114">Protocol</th><th width="131">Ether type</th><th width="126">Port range</th><th width="125">Destination</th><th>Ý nghĩa</th></tr></thead><tbody><tr><td>ANY</td><td>IPv4</td><td>0-65535</td><td>0.0.0.0/0</td><td>Rule mặc định của tất cả Security group</td></tr><tr><td>ANY</td><td>IPv6</td><td>0-65535</td><td>::/0</td><td>Rule mặc định của tất cả Security group</td></tr></tbody></table>

### Security group is automatically created by VNGCLOUD Controller Manager&#x20;

When you use VNGCloud Controller Manager to integrate Network Load Balancer with Cluster on VKS system, we will automatically create a Security Group. This Security group will include:

* Inbound:

<table><thead><tr><th width="207">Protocol</th><th width="108">Ether type</th><th>Port range</th><th>Source</th></tr></thead><tbody><tr><td>TCP, UDP hoặc ICMP</td><td>IPv4</td><td>Port của Service</td><td>Subnet Mask của Subnet mà bạn sử dụng cho Cluster.</td></tr></tbody></table>

* Outbound:

<table><thead><tr><th width="113">Protocol</th><th width="115">Ether type</th><th width="126">Port range</th><th width="127">Destination</th><th>Ý nghĩa</th></tr></thead><tbody><tr><td>ANY</td><td>IPv4</td><td>0-65535</td><td>0.0.0.0/0</td><td>Rule mặc định của tất cả Security group</td></tr><tr><td>ANY</td><td>IPv6</td><td>0-65535</td><td>::/0</td><td>Rule mặc định của tất cả Security group</td></tr></tbody></table>

### **Security group is automatically created by VNGCLOUD Ingress Controller**&#x20;

When you use VNGCloud Ingress Controller to integrate Application Load Balancer with Cluster on VKS system, we will automatically create a Security Group. This Security group will include:

* Inbound:

<table><thead><tr><th width="141">Protocol</th><th width="117">Ether type</th><th>Port range</th><th>Source</th></tr></thead><tbody><tr><td>TCP</td><td>IPv4</td><td>Port của Service</td><td>Subnet Mask của Subnet mà bạn sử dụng cho Cluster.</td></tr></tbody></table>

* Outbound:

<table><thead><tr><th width="105">Protocol</th><th width="109">Ether type</th><th width="122">Port range</th><th width="162">Destination</th><th>Ý nghĩa</th></tr></thead><tbody><tr><td>ANY</td><td>IPv4</td><td>0-65535</td><td>0.0.0.0/0</td><td>Rule mặc định của tất cả Security group</td></tr><tr><td>ANY</td><td>IPv6</td><td>0-65535</td><td>::/0</td><td>Rule mặc định của tất cả Security group</td></tr></tbody></table>

{% hint style="info" %}
**Note:**

* The default Security Groups are set up to meet the basic security needs of the cluster. If you modify or delete the Security Groups that are created for the cluster, it may lead to connectivity and access problems between nodes in the cluster or the cluster may not function properly or even fail to start. To ensure the stability and security of the cluster, the system will automatically reset the Security Groups to the default settings after a fixed period of time.
{% endhint %}
