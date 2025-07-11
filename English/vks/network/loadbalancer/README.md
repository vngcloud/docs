# Load Balancer

## What is NLB?

### Overview

* **Network Load Balancer (NLB)** is a load balancer provided by VNGCloud that helps distribute network traffic to multiple back-end servers in a computer group (instance group). NLB operates at layer 4 of the OSI model, providing load balancing based on IP addresses and TCP/UDP ports. For more detailed information about NLB, please refer to \[How it works (NLB)]

### Model deployment

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FVYBtJjEoUNgDi1f5J9vL%252Fimage.png%3Falt%3Dmedia%26token%3D554a2d62-320e-48d1-a884-3c7cce589071&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d7f786ac&#x26;sv=1" alt=""><figcaption></figcaption></figure>

## What is ALB?

### Overview

* **Application Load Balancer (ALB)** is a tool in network and server infrastructure used to distribute network traffic to multiple servers or virtual machines to improve the performance and availability of applications. ALB operates at the application layer, allowing traffic distribution based on many factors such as request type, server state, and load distribution algorithm. ALB provides advanced routing capabilities, allowing traffic to be directed based on Host or Path Header. It also supports session persistence, which helps maintain user sessions to the same server. This is useful for applications that require consistency in user interactions. For more information about ALB, please refer to \[How it works (ALB)]

### Model deployment

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## VNGCloud LoadBalancer Controller

The VNG Cloud Load Balancer Controller simplifies the deployment and management of load balancers in VNG Cloud environments for Kubernetes clusters. It automates the creation, configuration, and lifecycle management of load balancers for Kubernetes services and ingress resources. The controller ensures seamless integration with VNG Cloud services, enabling dynamic load balancing, SSL termination, and efficient traffic routing. It continuously monitors and reconciles resources to maintain their desired state, ensuring high availability, scalability, and optimized performance for applications running on VNG Cloud.

### Installation

#### Create Service Account and install VNGCloud LoadBalancer Controller

* Create or use a **service account** created on IAM and attach policy: **vLBFullAccess** , **vServerFullAccess** . To create a service account, go here [and](https://iam.console.vngcloud.vn/service-accounts) follow these steps:
  * Select " **Create a Service Account** ", enter a name for the Service Account and click **Next Step** to assign permissions to the Service Account
  * Find and select **Policy: vLBFullAccess and Policy: vServerFullAccess** , then click "**Create a Service Account**" to create Service Account, Policy: vLBFullAccess and Policy: vServerFullAccess created by VNG Cloud, you cannot delete these policies.
  * After successful creation, you need to save **the Client\_ID** and **Secret\_Key** of the Service Account to perform the next step.

#### Install VNGCloud LoadBalancer Controller

* Install Helm version 3.0 or higher. Refer to [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/) for instructions on how to install.
* Replace your ClientID an Client Secret information and run the following command:

```bash
helm install vngcloud-load-balancer-controller oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/vngcloud-load-balancer-controller \
  --namespace kube-system \
  --set mysecret.global.clientID= __________________ \
  --set mysecret.global.clientSecret= __________________
```

* After the installation is complete, check the status of pod:

```bash
kubectl -n kube-system get pod -l app.kubernetes.io/name=vngcloud-load-balancer-controller
```

For example, in the image below you have successfully installed vngcloud-controller-manager:

```bash
NAME                                                              READY   STATUS    RESTARTS   AGE
vngcloud-load-balancer-controller-1736217866-manager-77599vrxpz   1/1     Running   0          4h24m
```
