# Deployment mode

In the VNG Cloud environment, we offer two distinct types of Load Balancers: Application Load Balancers (ALBs) and Network Load Balancers (NLBs). These Load Balancers play a crucial role in optimizing the performance, availability, and scalability of your applications by efficiently distributing network traffic to backend servers. Each type of Load Balancer is tailored for specific use cases, offering unique features to meet the diverse requirements of modern IT architectures.

## Overview of Load Balancer Deployment Models in VNG Cloud

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

The Load Balancer management model consists of the following key components:

**Layer**

* **Application Load Balancer (ALB):** An application-layer Load Balancer that routes traffic based on HTTP/HTTPS requests, allowing for analysis of application-level data like HTTP headers and cookies. Ideal for web applications with complex routing requirements or content-based routing needs.
* **Network Load Balancer (NLB):** A transport-layer Load Balancer that uses TCP and UDP to distribute traffic across multiple servers based on IP addresses and port numbers. Ideal for applications that require high reliability and availability.

**Scheme**

* **Internet-facing:** An internet-facing Load Balancer routes traffic from clients over the internet to server clusters, enabling access to applications or services from the internet.
* **Internal:** An internal Load Balancer routes traffic within a private network from clients to server clusters, facilitating efficient request distribution within the internal network.

**Load Balancer Components**

Each Load Balancer, whether ALB or NLB, includes the following key components:

* **Listener:** The listener monitors and listens for incoming connection requests. It is responsible for receiving traffic on a specific port and protocol, then forwarding or routing that traffic to eligible servers based on predefined rules and configurations.
* **Policy (ALB only):** For Application Load Balancers, a policy acts as a set of rules/conditions for distributing requests to backend servers.
* **Pool:** A pool represents a group of servers that handle incoming traffic. The pool is responsible for load balancing requests across its members, ensuring efficient distribution and utilization of resources.
* **Pool Member:** A pool member acts as a server within the pool.
* **Health Check:** Health check settings are a set of rules that allow the Load Balancer to monitor the health of pools and their members.

## Learn More

To delve deeper into Application Load Balancers and Network Load Balancers, explore the following resources:

* **Application Load Balancer**
* **Network Load Balancer**
* **Feature Comparison**
