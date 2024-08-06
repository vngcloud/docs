# How VKS works?

Below are the current concepts being provided to you by VKS:

## **1. Public Cluster and Public Node Group**

<figure><img src="../.gitbook/assets/image (243).png" alt=""><figcaption></figcaption></figure>

When you create a **Public Cluster with Public Node Group**, the VKS system will:

* Creating a VM with a Floating IP (i.e., Public IP). These VMs (Nodes) can directly join the K8S cluster through this Public IP. By using a Public Cluster and Public Node Group, you can easily create Kubernetes clusters and expose services without needing a Load Balancer. This will help you save costs for your cluster.&#x20;

## **2. Public Cluster and Private Node Group**

<figure><img src="../.gitbook/assets/image (15) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

When you initialize a **Public Cluster with a Private Node Group**, the VKS system will:

* Create VMs without a Floating IP (that is, no Public IP). At this point, these VMs (Nodes) cannot directly join the K8S cluster. To enable these VMs to join the K8S cluster, you need to use a NAT Gateway (NATGW). The NATGW acts as a relay station, allowing VMs to connect to the K8S cluster without needing a Public IP. With VNG Cloud, we recommend that you use Pfsense or Palo Alto as a NATGW for your Cluster. Pfsense will help you effectively manage inbound and outbound traffic, ensuring network security and access management. In addition, using a Private Node Group will help you better control the applications in the cluster, specifically allowing you to limit access to the control plane through the Whitelist IP feature.

## **3. Private Cluster and Private Node Group**

Coming soon.
