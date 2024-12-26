# Using CNI Cilium Overlay

Overview

**CNI Cilium Overlay** in VKS is a type of **overlay network** that uses **eBPF (extended Berkeley Packet Filter)** to enhance network performance and security. Compared to solutions like **Calico Overlay** , Cilium offers higher performance thanks to its ability to process traffic directly in the kernel using eBPF. In addition, Calico often uses **iptables** to manage traffic, while Cilium with eBPF can handle network policies and application-specific behaviors (Layer 7).

***

## Model <a href="#model" id="model"></a>

On VKS, **Cilium Overlay** works according to the following model:

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**In there:**

* **Pod (eth0)** -> **lxc01/lxc02** : Pods communicate over a virtual network created by Cilium.
* **lxc01/lxc02** -> **cilium\_host** : Packets from Pods are forwarded to `cilium_host`, which is the intermediate layer between the Pod's network and the physical network.
* **cilium\_host** -> **ens3** : After being processed by Cilium (and eBPF), packets are sent to the physical network via `ens3`.
* **ens3** -> **VPC Network** : Finally, packets are transmitted over the physical network to other nodes or out of the cluster.

***

## Necessary conditions <a href="#dieu-kien-can" id="dieu-kien-can"></a>

To be able to initialize a **Cluster** and **Deploy** a **Workload** , you need:

* There is at least 1 **VPC** and 1 **Subnet in ACTIVE** state . If you do not have any VPC, Subnet, please initialize VPC, Subnet according to the instructions here [.](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc)
* There is at least 1 **SSH key in ACTIVE** state . If you do not have any SSH key, please initialize SSH key following the instructions here [.](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/security/ssh-key-bo-khoa)
* **kubectl** installed and configured on your device. please refer here [if](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) you are not sure how to install and use kuberctl. In addition, you should not use an outdated version of kubectl, we recommend that you use a kubectl version that is no more than one version different from the cluster version.

***

## **Initialize a Cluster using Cilium Overlay** <a href="#khoi-tao-mot-cluster-su-dung-cilium-overlay" id="khoi-tao-mot-cluster-su-dung-cilium-overlay"></a>

To initialize a Cluster, follow the steps below:

**Step 1:** Access [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Step 2: On the Overview** screen , select **Activate.**

**Step 3:** Wait until we successfully initialize your VKS account. After successfully Activating, select **Create a Cluster.**

**Step 4:** At the Cluster initialization screen, we have set up the information for the Cluster and a **Default Node Group** for you. To use **Cilium Overlay** for your **Cluster , please select:**

* **Network type** : Cilium Overlay

| Field                        | Meaning                                                                                                                                                                        | Illustrative example                                                                                             |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| **VPC**                      | The IP address range that the Cluster nodes will use to communicate.                                                                                                           | In the picture, we choose VPC with IP range **10.111.0.0/16** , corresponding to **65536 IPs**                   |
| **Subnet**                   | A smaller IP address range belonging to the VPC. Each node in the Cluster will be assigned an IP from this Subnet. The Subnet must be within the IP range of the selected VPC. | In the picture, we choose Subnet with **Primary IP range** of **10.111.0.0/24** , corresponding to **256 IPs**   |
| **IP-IP encapsulation mode** | IP-IP encapsulation mode in VKS is Always                                                                                                                                      | **In the figure, we select Always** mode to always encapsulate packets.                                          |
| **CIDR**                     | The virtual network range that the pods will use                                                                                                                               | In the picture, we choose the virtual network range as `172.16.0.0/16`. The pods will get IP from this IP range. |

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

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

* If the result is as below, it means your Cluster is successfully initialized with 3 nodes:

```bash
NAME                                   STATUS   ROLES    AGE     VERSION
vks-cluster-02-nodegroup-7fb09-3a594   Ready    <none>   5m48s   v1.29.1
vks-cluster-02-nodegroup-7fb09-3cb67   Ready    <none>   5m34s   v1.29.1
vks-cluster-02-nodegroup-7fb09-430aa   Ready    <none>   5m52s   v1.29.1
```

* Continue running the following command to check the pods **deployed** on your kube-system namespace:

```bash
k get pods -A
```

* If the result is as below, it means that the pods supporting **Cilium Overlay** have been successfully run:

```bash
NAMESPACE     NAME                                           READY   STATUS    RESTARTS        AGE
kube-system   cilium-8xtwz                                   1/1     Running   1 (5m36s ago)   6m7s
kube-system   cilium-cpxvv                                   1/1     Running   0               5m53s
kube-system   cilium-envoy-b95pg                             1/1     Running   0               6m7s
kube-system   cilium-envoy-dx8qg                             1/1     Running   0               6m11s
kube-system   cilium-envoy-sqdn8                             1/1     Running   0               5m53s
kube-system   cilium-operator-75b8c6f6d4-7x4f6               1/1     Running   0               9m19s
kube-system   cilium-operator-75b8c6f6d4-k7j45               1/1     Running   0               9m19s
kube-system   cilium-zs2cm                                   1/1     Running   1 (5m35s ago)   6m11s
kube-system   coredns-1727408780-5fcf89468-7hmvp             1/1     Running   0               9m24s
kube-system   coredns-1727408780-5fcf89468-v9nbd             1/1     Running   0               9m24s
kube-system   hubble-relay-8899f8cdc-976zf                   1/1     Running   1 (4m3s ago)    9m20s
kube-system   hubble-ui-574c5bb99b-gg7jx                     2/2     Running   0               9m20s
kube-system   konnectivity-agent-46nvd                       1/1     Running   0               5m27s
kube-system   konnectivity-agent-qhq4m                       1/1     Running   0               5m24s
kube-system   konnectivity-agent-xs7bq                       1/1     Running   0               5m21s
kube-system   vngcloud-controller-manager-7c47d64584-z8827   1/1     Running   0               9m21s
kube-system   vngcloud-csi-controller-848f68f46-2hkxl        7/7     Running   2 (4m58s ago)   9m23s
kube-system   vngcloud-csi-controller-848f68f46-bkvkg        7/7     Running   2 (4m56s ago)   9m23s
kube-system   vngcloud-csi-node-8rxbx                        3/3     Running   2 (5m1s ago)    6m7s
kube-system   vngcloud-csi-node-mxknq                        3/3     Running   3 (4m54s ago)   5m53s
kube-system   vngcloud-csi-node-tfrsp                        3/3     Running   2 (5m2s ago)    6m11s
kube-system   vngcloud-ingress-controller-0                  1/1     Running   1 (5m16s ago)   9m7s
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

* Perform a check of the pods via the command:

```bash
kubectl get pods -o wide
```

* You can observe below, the **nginx pods** are assigned IPs 172.16.xx which satisfy the **Cilium CIDR condition 172.16.0.0/16** that we specified above:

```bash
NAME                         READY   STATUS    RESTARTS   AGE   IP             NODE                                   NOMINATED NODE   READINESS GATES
nginx-app-7c79c4bf97-4lcbn   1/1     Running   0          83s   172.16.0.6     vks-cluster-02-nodegroup-7fb09-430aa   <none>           <none>
nginx-app-7c79c4bf97-669z9   1/1     Running   0          83s   172.16.1.115   vks-cluster-02-nodegroup-7fb09-3a594   <none>           <none>
nginx-app-7c79c4bf97-7hqp5   1/1     Running   0          83s   172.16.1.32    vks-cluster-02-nodegroup-7fb09-3a594   <none>           <none>
nginx-app-7c79c4bf97-8fjhm   1/1     Running   0          83s   172.16.2.51    vks-cluster-02-nodegroup-7fb09-3cb67   <none>           <none>
nginx-app-7c79c4bf97-8xmfm   1/1     Running   0          83s   172.16.0.100   vks-cluster-02-nodegroup-7fb09-430aa   <none>           <none>
nginx-app-7c79c4bf97-9b4px   1/1     Running   0          83s   172.16.2.19    vks-cluster-02-nodegroup-7fb09-3cb67   <none>           <none>
nginx-app-7c79c4bf97-b7vlg   1/1     Running   0          83s   172.16.1.128   vks-cluster-02-nodegroup-7fb09-3a594   <none>           <none>
nginx-app-7c79c4bf97-bc6r4   1/1     Running   0          83s   172.16.0.160   vks-cluster-02-nodegroup-7fb09-430aa   <none>           <none>
nginx-app-7c79c4bf97-flkz5   1/1     Running   0          83s   172.16.2.253   vks-cluster-02-nodegroup-7fb09-3cb67   <none>           <none>
nginx-app-7c79c4bf97-k55j6   1/1     Running   0          83s   172.16.2.76    vks-cluster-02-nodegroup-7fb09-3cb67   <none>           <none>
nginx-app-7c79c4bf97-l9p8p   1/1     Running   0          83s   172.16.2.187   vks-cluster-02-nodegroup-7fb09-3cb67   <none>           <none>
nginx-app-7c79c4bf97-llnfq   1/1     Running   0          83s   172.16.1.30    vks-cluster-02-nodegroup-7fb09-3a594   <none>           <none>
nginx-app-7c79c4bf97-mg9t8   1/1     Running   0          83s   172.16.0.221   vks-cluster-02-nodegroup-7fb09-430aa   <none>           <none>
nginx-app-7c79c4bf97-mlh7g   1/1     Running   0          83s   172.16.2.191   vks-cluster-02-nodegroup-7fb09-3cb67   <none>           <none>
nginx-app-7c79c4bf97-n946h   1/1     Running   0          83s   172.16.1.82    vks-cluster-02-nodegroup-7fb09-3a594   <none>           <none>
nginx-app-7c79c4bf97-p9k42   1/1     Running   0          83s   172.16.0.112   vks-cluster-02-nodegroup-7fb09-430aa   <none>           <none>
nginx-app-7c79c4bf97-sl4b8   1/1     Running   0          83s   172.16.1.22    vks-cluster-02-nodegroup-7fb09-3a594   <none>           <none>
nginx-app-7c79c4bf97-tdtjc   1/1     Running   0          83s   172.16.2.109   vks-cluster-02-nodegroup-7fb09-3cb67   <none>           <none>
nginx-app-7c79c4bf97-zwxps   1/1     Running   0          83s   172.16.2.209   vks-cluster-02-nodegroup-7fb09-3cb67   <none>           <none>
nginx-app-7c79c4bf97-zxx87   1/1     Running   0          83s   172.16.0.212   vks-cluster-02-nodegroup-7fb09-430aa   <none>           <none>
```

* You can also perform a detailed description of each pod to check this pod information via the command:

```bash
kubectl describe pod nginx-app-7c79c4bf97-4lcbn
```
