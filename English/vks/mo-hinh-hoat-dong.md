# How VKS works?

Below are the current concepts being provided to you by VKS:

## **1. Public Cluster** <a href="#id-1.-public-cluster" id="id-1.-public-cluster"></a>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fvbnmi3cReXehXboTd85R%252Fimage.png%3Falt%3Dmedia%26token%3D618fbb97-4bd7-4612-be3a-0e6d3ea40021&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=9119e8dd&#x26;sv=1" alt=""><figcaption></figcaption></figure>

When you create a **Public Cluster with Public Node Group** , the VKS system will:

* Create a VM with Floating IP (ie Public IP). Now these VMs (Nodes) can directly join the K8S cluster through this Public IP. By using Public Cluster and Public Node Group, you can easily create Kubernetes clusters and expose services without using Load Balancer. This will contribute to cost savings for your cluster.

When you create a **Public Cluster with a Private Node Group** , the VKS system will:

* Create VM without Floating IP (ie without Public IP). At this time, these VMs (Nodes) cannot join the K8S cluster directly. In order for these VMs to join the K8S cluster, you need to use a NAT Gateway ( **NATGW** ). **NATGW** acts as a relay station, allowing VMs to connect to the K8S cluster without needing a Public IP. With GreenNode, we recommend you use Pfsense or Palo Alto as a NATGW for your Cluster. Pfsense will help you manage incoming and outgoing network traffic (inbound and outbound traffic) effectively, ensuring network security and access management. Besides, using Private Node Group will help you control applications in the cluster more securely, specifically you can limit control plane access rights through the Whitelist IP feature.

## **2. Private Cluster** <a href="#id-2.-private-cluster" id="id-2.-private-cluster"></a>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fj8WSjgnwd7WXKXblh1ex%252Fimage.png%3Falt%3Dmedia%26token%3Dae664224-8486-495b-aab6-5d1d1017edec&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=8c00454b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

When you create a **Public Cluster with Public/Private Node Group** , the VKS system will:

* To enhance the security of your cluster, we have introduced the private cluster model. The Private Cluster feature helps make your K8S cluster as secure as possible, all connections are completely private from the connection between nodes to the control plane, the connection from the client to the control plane, or the connection from nodes to products. Other services in GreenNode such as: vStorage, vCR, vMonitor, VNGCloud APIs,...Private Cluster is the ideal choice for **services that require strict access control, ensuring compliance with security regulations and data privacy**.

## 3. Comparison between using Public Cluster and Private Cluster <a href="#id-3.-so-sanh-giua-viec-su-dung-public-cluster-va-private-cluster" id="id-3.-so-sanh-giua-viec-su-dung-public-cluster-va-private-cluster"></a>

Below is a comparison table between creating and using Public Cluster and Private Cluster on the VKS system:

<table data-header-hidden><thead><tr><th width="201"></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Criteria</strong></td><td><strong>Public Cluster</strong></td><td><strong>Private Cluster</strong></td></tr><tr><td><strong>Connect</strong></td><td>Use Public IP addresses to communicate between nodes and control plane, between clients and control plane, between nodes and other services in GreenNode.</td><td>Use Private IP addresses to communicate between nodes and control plane, between clients and control plane, between nodes and other services in GreenNode.</td></tr><tr><td><strong>Security</strong></td><td>Medium security since connections use Public IP.</td><td>Higher security with all connections private and limited access.</td></tr><tr><td><strong>Access management</strong></td><td>More difficult to control, access can be managed through the Whitelist feature</td><td>Strict access control, all connections are within GreenNode's private network, thereby minimizing the risk of external network attacks.</td></tr><tr><td><strong>Scalability (AutoScaling)</strong></td><td>Easily scalable through <strong>Auto Scaling</strong> feature .</td><td>Easily scalable through <strong>Auto Scaling</strong> feature .</td></tr><tr><td><strong>AutoHealing</strong> </td><td>Automatically detect errors and restart the node ( <strong>Auto Healing</strong> )</td><td>Automatically detect errors and restart the node ( <strong>Auto Healing</strong> )</td></tr><tr><td><strong>Accessibility from outside</strong></td><td>Easy access from anywhere with internet.</td><td>Access from outside must be through other security solutions.</td></tr><tr><td><strong>Configuration and deployment</strong></td><td>Simpler because it does not require setting up an internal network.</td><td>More complex, requires private and secure network configuration.</td></tr><tr><td><strong>Cost</strong></td><td>Usually lower because there is no need to set up a complex security infrastructure.</td><td>Higher cost due to additional security and management components required. <strong>Specifically, when using a private cluster, you need to pay for 4 automatically created private service endpoints to connect to services on GreenNode.</strong></td></tr><tr><td><strong>Flexibility</strong></td><td>High, easy to change and access services.</td><td>More flexible in applications that require security, but less flexible for applications that require external access.</td></tr></tbody></table>

Therefore:

* **Public Cluster** : Suitable for applications that do not require high security and need flexibility and access from multiple locations. Easy to deploy and manage but has higher security risks.
* **Private Cluster** : Suitable for applications that require high security, strictly complying with security and privacy regulations. Provides stable and secure connectivity, but requires more complex configuration and management, as well as higher costs.
