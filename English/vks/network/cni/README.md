# CNI

## **Overview** <a href="#tong-quan" id="tong-quan"></a>

**CNI (Container Network Interface)** is a standard set of tools that provides networking capabilities to containers in a Kubernetes cluster. Simply put, CNI is an abstraction layer that helps Kubernetes manage and configure networking for pods (a collection of containers sharing the same network) in a flexible and efficient way.

#### How does CNI work? <a href="#cni-hoat-dong-nhu-the-nao" id="cni-hoat-dong-nhu-the-nao"></a>

When you create a new pod, Kubernetes calls CNI to create a network interface for that pod. The CNI plugin performs the following tasks:

* **Assign IP address:** Assign a unique IP address to the pod.
* **Routing configuration:** Set up routing rules that allow communication between pods,...

Additionally, the connections work as follows:

* **Connecting within the same VPC** : Nodes within the same VPC will connect directly to each other.
* **Connecting between different VPCs** : Use VPC Peering to connect nodes between different VPCs.
* **Connect to external infrastructure:** Use networking solutions such as site-to-site VPN or Direct Connect to connect from nodes in VPC to external infrastructures (On Cloud, On-premise).

This helps maintain a continuous, flexible, and secure network infrastructure in a multi-cloud or hybrid-cloud environment.

***

## Comparison between CNI plugins <a href="#so-sanh-giua-cac-plugin-cni" id="so-sanh-giua-cac-plugin-cni"></a>

Currently, VKS is providing 3 popular CNI plugins: Calico Overlay, Cilium Overlay, Cilium VPC Native Routing. In which:

* **Calico Overlay** : Uses overlay model through tunneling ( **IP-in-IP** ). Compatible with many infrastructures but performance can be affected by tunnel **overhead .**
* **Cilium Overlay** : Also uses the overlay model but has strong integration with **eBPF** , which improves performance, security, and scalability.
* **Cilium VPC Native Routing** : Uses **eBPF** and **no overlay required** , leveraging the routing capabilities of the VPC infrastructure, providing the best performance and scalability.

**When to use Calico Overlay** : simple to use, does not require too high performance.

**When to use Cilium Overlay** : simple to use, does not require too high performance but requires intensive monitoring (Hubble).

**When to use Cilium VPC Native Routing** : high performance requirements, easy **connectivity to external systems** , and in-depth monitoring needs (Hubble).
