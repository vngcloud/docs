# Public Cluster and Private Cluster

## **1. Public Cluster** <a href="#id-1.-public-cluster" id="id-1.-public-cluster"></a>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fvbnmi3cReXehXboTd85R%252Fimage.png%3Falt%3Dmedia%26token%3D618fbb97-4bd7-4612-be3a-0e6d3ea40021&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=9119e8dd&#x26;sv=1" alt=""><figcaption></figcaption></figure>

When you create a **Public Cluster with Public Node Group** , the VKS system will:

* Create a VM with Floating IP (ie Public IP). Now these VMs (Nodes) can directly join the K8S cluster through this Public IP. By using Public Cluster and Public Node Group, you can easily create Kubernetes clusters and expose services without using Load Balancer. This will contribute to cost savings for your cluster.

When you create a **Public Cluster with a Private Node Group** , the VKS system will:

* Create VM without Floating IP (ie without Public IP). At this time, these VMs (Nodes) cannot join the K8S cluster directly. In order for these VMs to join the K8S cluster, you need to use a NAT Gateway ( **NATGW** ). **NATGW** acts as a relay station, allowing VMs to connect to the K8S cluster without needing a Public IP. With VNG Cloud, we recommend you use Pfsense or Palo Alto as a NATGW for your Cluster. Pfsense will help you manage incoming and outgoing network traffic (inbound and outbound traffic) effectively, ensuring network security and access management. Besides, using Private Node Group will help you control applications in the cluster more securely, specifically you can limit control plane access rights through the Whitelist IP feature.

## **2. Private Cluster** <a href="#id-2.-private-cluster" id="id-2.-private-cluster"></a>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fj8WSjgnwd7WXKXblh1ex%252Fimage.png%3Falt%3Dmedia%26token%3Dae664224-8486-495b-aab6-5d1d1017edec&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=8c00454b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

When you create a **Public Cluster with Public/Private Node Group** , the VKS system will:

* To enhance the security of your cluster, we have introduced the private cluster model. Private clusters do not use External IP addresses for nodes. This means that users from the internet cannot directly connect to nodes in the cluster. Private Cluster is the ideal choice for services that require strict access control, ensuring compliance with security and data privacy regulations.
