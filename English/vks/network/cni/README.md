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

* **Calico Overlay:** Suitable for environments that require **high performance** and compatibility with multiple infrastructures.
* **Cilium Overlay** : Optimized for applications that require **strong security,** helping to improve performance, security, and scalability.
* **Cilium VPC Native Routing: Ideal for VPC** environments , optimize performance and manage IPs directly from the VPC.

Below is a detailed comparison table of three popular CNI plugins offered on VKS: **Calico Overlay** , **Cilium Overlay** , and **Cilium VPC Native Routing** .

| **Network model**                           | Overlay (VXLAN/IPip tunneling)                                      | Overlay (VXLAN tunneling)                                           | Native routing directly on VPC (no overlay)             |
| ------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------- |
| **Platform Technology**                     | Use IP-in-IP or VXLAN to create overlay networks                    | Using eBPF to create overlay network                                | Use eBPF and use VPC native routing                     |
| **Performance**                             | Good, suitable for many workloads                                   | Very good, optimized for workloads that require high performance    | Best practice, make the most of your VPC infrastructure |
| **Security**                                | Powerful, granular policy-based networking support.                 | Good, deep integration with kernel, eBPF support                    | Relatively good, based on VPC configuration             |
| **Integrate with Kubernetes NetworkPolicy** | Have                                                                | Have                                                                | Have                                                    |
| **IP Management**                           | Dynamic IP management, IP allocation from Calico CIDR address range | Dynamic IP management, IP allocation from Cilium CIDR address range | Manage IPs directly from VPC address ranges             |
| **Scalability**                             | Good scalability support, suitable for large clusters               | Good scalability support, but limited by eBPF map size              | Good scalability support, optimized for VPC networks    |
