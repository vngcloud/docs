# Working with Network load balancing (NLB)

#### What is NLB? <a href="#workingwithnetworkloadbalancing-nlb-nlblagi" id="workingwithnetworkloadbalancing-nlb-nlblagi"></a>

* **Network Load Balancer (NLB)** is a load balancer provided by GreenNode that helps distribute network traffic to multiple back-end servers in a computer group (instance group). NLB operates at layer 4 of the OSI model, providing load balancing based on IP addresses and TCP/UDP ports. For more detailed information about NLB, please refer to \[How it works (NLB)]

**Model deployment**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FVYBtJjEoUNgDi1f5J9vL%252Fimage.png%3Falt%3Dmedia%26token%3D554a2d62-320e-48d1-a884-3c7cce589071&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d7f786ac&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* **vngcloud-controller-manager** : GreenNode LoadBalancer Controller is a controller that runs on Kubernetes clusters deployed on GreenNode. It is responsible for managing GreenNode resources for Kubernetes clusters, including:
  * **Create and manage Network Load Balancer (NLB)** for Kubernetes Services with service type = Load Balancer.
