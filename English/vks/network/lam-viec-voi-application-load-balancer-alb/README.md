# Working with Application Load Balancer (ALB)

## Overview <a href="#workingwithapplicationloadbalancer-alb-tongquan" id="workingwithapplicationloadbalancer-alb-tongquan"></a>

### What is ALB? <a href="#workingwithapplicationloadbalancer-alb-alblagi" id="workingwithapplicationloadbalancer-alb-alblagi"></a>

* **Application Load Balancer (ALB)** is a tool in network and server infrastructure used to distribute network traffic to multiple servers or virtual machines to improve the performance and availability of applications. ALB operates at the application layer, allowing traffic distribution based on many factors such as request type, server state, and load distribution algorithm. ALB provides advanced routing capabilities, allowing traffic to be directed based on Host or Path Header. It also supports session persistence, which helps maintain user sessions to the same server. This is useful for applications that require consistency in user interactions. For more information about ALB, please refer to \[How it works (ALB)]

Model:

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**In addition to the basic components of a K8S cluster and an ALB that you already know, in this model we use:**&#x20;

* **Ingress**: is a resource in Kubernetes that is configured to make Services accessible from outside the k8s cluster via URL, and can also load balance traffic, support SSL/TLS connections and provide virtual hosting based on names. An Ingress does not arbitrarily expose protocols other than HTTP and HTTPS. Ingress acts as a single entry point for HTTP and HTTPS requests from outside the cluster to internal services. Traffic routing is controlled by rules defined in the Ingress resource (Ingress Yaml File). An Ingress is managed by VNGCloud Ingress Controller: is an application that runs in the cluster and manages Ingress resources based on the Ingress Yaml File defined by the customer
