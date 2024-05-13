# Concept

Current concepts that VKS provides for you:

## **1. Public Cluster and Public Node Group**

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

When you initialize a **Public Cluster with Public Node Group**, the VKS system will:

* Create VMs with Floating IPs (i.e., public IPs). At this point, these VMs (Nodes) can join the K8S cluster directly through this public IP. By using Public Cluster and Public Node Group, you can easily create Kubernetes clusters that are accessible from the internet. This can be useful for applications that need to be accessed from outside, such as web applications or APIs. In other words, using Public Cluster and Public Node Group helps you expand the connectivity of your Kubernetes cluster, allowing applications running on the cluster to be easily accessible from anywhere on the internet, while still ensuring flexibility and centralized management. This increases the accessibility and distribution of your applications to end users.

## **2. Public Cluster and Private Node Group**

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

When you initialize a **Public Cluster with Private Node Group**, the VKS system will:

* Create VMs without Floating IPs (i.e., no public IPs). At this point, these VMs (Nodes) cannot join the K8S cluster directly. For these VMs to join the K8S cluster, you need to use a NAT Gateway (NATGW). NATGW acts as a relay station, allowing VMs to connect to the K8S cluster without a public IP. With VNG Cloud, we recommend using Pfsense as a NATGW for your Cluster. Pfsense will help you manage inbound and outbound traffic effectively, ensuring network security and access management. In other words, using a Private Node Group in a Public Cluster requires a different approach to connect the VMs to the K8S cluster. You cannot access directly from the internet like when using Public Node Group, but you can still manage the connection through a specific NATGW through Pfsense to ensure the security and control of your Kubernetes cluster's network traffic.

## **3. Private Cluster and Private Node Group**

Coming soon.
