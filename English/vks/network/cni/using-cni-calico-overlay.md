# Using CNI Calico Overlay

Overview

**The CNI Calico Overlay** in VKS is a type of **overlay network** that uses **IP-in-IP encapsulation** to create an overlay network. This allows pods to communicate with each other without changing the underlying physical network configuration. Pods will receive IP addresses from the IP address range configured for Calico, which is usually different from the IP address of your VPC or subnet.

***

## Model <a href="#model" id="model"></a>

On VKS, **Calico Overlay** works according to the following model:

<figure><img src="../../../.gitbook/assets/image (12) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**In there:**

* **Pods** on each node communicate with each other via **the cali interface** and **bridge cni0** .
* When pods need to communicate with pods on other nodes, packets are encapsulated into overlay packets and sent over **the physical network (VPC Network)** .
* **Calico** on each node is responsible for performing encapsulation and decapsulation so that pods can communicate across different nodes.

***

## Necessary conditions <a href="#dieu-kien-can" id="dieu-kien-can"></a>

To be able to initialize a **Cluster** and **Deploy** a **Workload** , you need:

* There is at least 1 **VPC** and 1 **Subnet in ACTIVE** state . If you do not have any VPC, Subnet, please initialize VPC, Subnet according to the instructions here [.](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc)
* There is at least 1 **SSH key in ACTIVE** state . If you do not have any SSH key, please initialize SSH key following the instructions here [.](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/security/ssh-key-bo-khoa)
* **kubectl** installed and configured on your device. please refer here [if](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) you are not sure how to install and use kuberctl. In addition, you should not use an outdated version of kubectl, we recommend that you use a kubectl version that is no more than one version different from the cluster version.

***

## **Create a Cluster using Calico Overlay** <a href="#khoi-tao-mot-cluster-su-dung-calico-overlay" id="khoi-tao-mot-cluster-su-dung-calico-overlay"></a>

To initialize a Cluster, follow the steps below:

**Step 1:** Access [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Step 2: On the Overview** screen , select **Activate.**

**Step 3:** Wait until we successfully initialize your VKS account. After successfully Activating, select **Create a Cluster.**

**Step 4:** At the Cluster initialization screen, we have set up the information for the Cluster and a **Default Node Group** for you. To use **Calico Overlay** for your **Cluster , please select:**

* **Network type** : **Calico Overlay**

<table data-header-hidden><thead><tr><th width="205"></th><th></th><th></th></tr></thead><tbody><tr><td>Field</td><td>Meaning</td><td>Illustrative example</td></tr><tr><td><strong>VPC</strong></td><td>The IP address range that the Cluster nodes will use to communicate.</td><td>In the picture, we choose VPC with IP range <strong>10.111.0.0/16</strong> , corresponding to <strong>65536 IPs</strong></td></tr><tr><td><strong>Subnet</strong></td><td>A smaller IP address range belonging to the VPC. Each node in the Cluster will be assigned an IP from this Subnet. The Subnet must be within the IP range of the selected VPC.</td><td>In the picture, we choose Subnet with <strong>Primary IP range</strong> of <strong>10.111.0.0/24</strong> , corresponding to <strong>256 IPs</strong></td></tr><tr><td><strong>IP-IP encapsulation mode</strong></td><td>IP-IP encapsulation mode in VKS is Always</td><td><strong>In the figure, we select Always</strong> mode to always encapsulate packets.</td></tr><tr><td><strong>CIDR</strong></td><td>The virtual network range that the pods will use</td><td>In the picture, we choose the virtual network range as <code>172.16.0.0/16</code>. The pods will get IP from this IP range.</td></tr></tbody></table>

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* **Only one networktype:** In a cluster, you can use only one of three networktypes: Calico Overlay, Cilium Overlay, or Cilium VPC Native Routing
* **Multiple subnets for a cluster:** VKS supports the use of multiple subnets for a cluster. This allows you to configure each node group in the cluster to be located on different subnets within the same VPC, helping to optimize resource allocation and network management.
{% endhint %}

**Step 5:** Select **Create Kubernetes cluster.** Please wait a few minutes for us to initialize your Cluster, the status of the Cluster is now **Creating** .

**Step 6: When the Cluster** status is **Active** , you can view Cluster information and Node Group information by selecting Cluster Name in the **Name** column .

***

## Deploy a Workload <a href="#deploy-mot-workload" id="deploy-mot-workload"></a>

Below are instructions for deploying an nginx deployment and testing IP assignment for the pods deployed in your cluster.

**Step 1:** Access [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** The Cluster list is displayed, select the **Download** icon and select **Download Config File** to download the kubeconfig file. This file will give you full access to your Cluster.

**Step 3** : Rename this file to config and save it to the **\~/.kube/config folder**

**Step 4:** Perform Cluster check via command:

* Run the following command to check **the node**

```bash
kubectl get nodes
```

* If the result is as below, it means your Cluster is successfully initialized with 5 nodes:

```bash
NAME                                  STATUS   ROLES    AGE   VERSION
vks-cluster01-nodegroup-536d9-452f1   Ready    <none>   15h   v1.28.8
vks-cluster01-nodegroup-998b1-14f64   Ready    <none>   16h   v1.28.8
vks-cluster01-nodegroup01-22e98       Ready    <none>   19h   v1.28.8
vks-cluster01-nodegroup01-36911       Ready    <none>   19h   v1.28.8
vks-cluster01-nodegroup01-9102e       Ready    <none>   19h   v1.28.8
```

* Continue running the following command to check the pods **deployed** on your kube-system namespace:

```bash
k get pods -A
```

* If the result is as below, it means that the pods supporting **Calico Overlay** have been successfully run:

```bash
NAMESPACE     NAME                                           READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-868b574465-wbxlx       1/1     Running   0          19h
kube-system   calico-node-65ql2                              1/1     Running   0          16h
kube-system   calico-node-d9hc7                              1/1     Running   0          19h
kube-system   calico-node-gp2s7                              1/1     Running   0          19h
kube-system   calico-node-hgk86                              1/1     Running   0          19h
kube-system   calico-node-vj9ts                              1/1     Running   0          15h
kube-system   calico-typha-74d79bf5f6-zzdn9                  1/1     Running   0          19h
kube-system   coredns-1727334072-86776977c9-l9tcp            1/1     Running   0          19h
kube-system   coredns-1727334072-86776977c9-xqcn9            1/1     Running   0          19h
kube-system   konnectivity-agent-bj7wc                       1/1     Running   0          15h
kube-system   konnectivity-agent-fnm7j                       1/1     Running   0          16h
kube-system   konnectivity-agent-gvnbl                       1/1     Running   0          19h
kube-system   konnectivity-agent-jj764                       1/1     Running   0          19h
kube-system   konnectivity-agent-vgmwf                       1/1     Running   0          19h
kube-system   kube-proxy-8r85m                               1/1     Running   0          15h
kube-system   kube-proxy-bddf5                               1/1     Running   0          19h
kube-system   kube-proxy-kwskl                               1/1     Running   0          16h
kube-system   kube-proxy-zv6m4                               1/1     Running   0          19h
kube-system   kube-proxy-zw65v                               1/1     Running   0          19h
kube-system   vngcloud-controller-manager-67cf7f868c-jc66k   1/1     Running   0          19h
kube-system   vngcloud-csi-controller-746b67bcb8-dn5d7       7/7     Running   0          19h
kube-system   vngcloud-csi-controller-746b67bcb8-hqm24       7/7     Running   0          19h
kube-system   vngcloud-csi-node-24nlb                        3/3     Running   0          15h
kube-system   vngcloud-csi-node-fgxpg                        3/3     Running   0          19h
kube-system   vngcloud-csi-node-q9npf                        3/3     Running   0          19h
kube-system   vngcloud-csi-node-tw5sv                        3/3     Running   0          19h
kube-system   vngcloud-csi-node-z2sk9                        3/3     Running   0          16h
kube-system   vngcloud-ingress-controller-0                  1/1     Running   0          19h
```

**Step 2: Deploy nginx on the newly created cluster:**

* Initialize the **nginx-deployment.yaml** file with the following content:

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-app
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 20
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

* Perform this deployment via command:

```bash
kubectl apply -f nginx-deployment.yaml
```

**Step 3: Check the deployed nginx pods and the IP address assigned to each pod**

* Perform a check of the **pods** via the command:

```bash
kubectl get pods -o wide
```

* You can observe below, the **nginx pods** are assigned IPs 172.16.xx which satisfy the **Calico CIDR condition 172.16.0.0/16** that we specified above:

```bash
NAME                         READY   STATUS    RESTARTS   AGE   IP               NODE                                  NOMINATED NODE   READINESS GATES
nginx-app-7c79c4bf97-2xbwd   1/1     Running   0          49s   172.16.197.136   vks-cluster01-nodegroup01-22e98       <none>           <none>
nginx-app-7c79c4bf97-5hcds   1/1     Running   0          49s   172.16.197.137   vks-cluster01-nodegroup01-22e98       <none>           <none>
nginx-app-7c79c4bf97-5hgwp   1/1     Running   0          49s   172.16.197.138   vks-cluster01-nodegroup01-22e98       <none>           <none>
nginx-app-7c79c4bf97-5l79h   1/1     Running   0          49s   172.16.83.4      vks-cluster01-nodegroup01-36911       <none>           <none>
nginx-app-7c79c4bf97-5q2f4   1/1     Running   0          49s   172.16.226.196   vks-cluster01-nodegroup01-9102e       <none>           <none>
nginx-app-7c79c4bf97-5szc6   1/1     Running   0          49s   172.16.83.6      vks-cluster01-nodegroup01-36911       <none>           <none>
nginx-app-7c79c4bf97-9272q   1/1     Running   0          49s   172.16.167.71    vks-cluster01-nodegroup-998b1-14f64   <none>           <none>
nginx-app-7c79c4bf97-cgwrj   1/1     Running   0          49s   172.16.67.195    vks-cluster01-nodegroup-536d9-452f1   <none>           <none>
nginx-app-7c79c4bf97-fhlg4   1/1     Running   0          49s   172.16.167.70    vks-cluster01-nodegroup-998b1-14f64   <none>           <none>
nginx-app-7c79c4bf97-fj865   1/1     Running   0          49s   172.16.83.3      vks-cluster01-nodegroup01-36911       <none>           <none>
nginx-app-7c79c4bf97-gh6hj   1/1     Running   0          49s   172.16.167.69    vks-cluster01-nodegroup-998b1-14f64   <none>           <none>
nginx-app-7c79c4bf97-hx2rn   1/1     Running   0          49s   172.16.83.5      vks-cluster01-nodegroup01-36911       <none>           <none>
nginx-app-7c79c4bf97-jv26j   1/1     Running   0          49s   172.16.167.68    vks-cluster01-nodegroup-998b1-14f64   <none>           <none>
nginx-app-7c79c4bf97-km7p4   1/1     Running   0          49s   172.16.226.198   vks-cluster01-nodegroup01-9102e       <none>           <none>
nginx-app-7c79c4bf97-lrh2r   1/1     Running   0          49s   172.16.167.67    vks-cluster01-nodegroup-998b1-14f64   <none>           <none>
nginx-app-7c79c4bf97-lvj6g   1/1     Running   0          49s   172.16.67.196    vks-cluster01-nodegroup-536d9-452f1   <none>           <none>
nginx-app-7c79c4bf97-nhhdk   1/1     Running   0          49s   172.16.226.197   vks-cluster01-nodegroup01-9102e       <none>           <none>
nginx-app-7c79c4bf97-qr2lm   1/1     Running   0          49s   172.16.67.198    vks-cluster01-nodegroup-536d9-452f1   <none>           <none>
nginx-app-7c79c4bf97-x4ztb   1/1     Running   0          49s   172.16.226.195   vks-cluster01-nodegroup01-9102e       <none>           <none>
nginx-app-7c79c4bf97-xrqwx   1/1     Running   0          49s   172.16.67.197    vks-cluster01-nodegroup-536d9-452f1   <none>           <none>
```

* You can also perform a detailed description of each pod to check this pod information via the command:

```bash
kubectl describe pod nginx-app-7c79c4bf97-2xbwd
```
