# Using CNI Cilium VPC Native Routing

## Overview <a href="#tong-quan" id="tong-quan"></a>

**CNI (Container Network Interface) Cilium VPC Native Routing** is a mechanism that helps Kubernetes manage networks without using overlay networks. Instead of using virtual network layers, **CNI Cilium VPC Native Routing** leverages the direct routing capabilities of cloud service providers' VPCs (Virtual Private Clouds) to optimize data transfer between nodes and pods in the Kubernetes cluster.

***

## Model <a href="#model" id="model"></a>

On VKS, **CNI (Container Network Interface) Cilium VPC Native Routing** operates according to the following model:

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

**In there:**

* Each **Node** has a private IP address range for pods (Pod CIDR). Pods in each node use addresses from this CIDR and communicate over the virtual network.
* **Cilium** and **eBPF** perform network management for all pods on each node, including handling traffic going from pod to pod, or from node to node. When necessary, eBPF performs **masquerading** to hide the internal IP address of the pod when communicating with the external network.
* **Cilium** ensures that pods can communicate with each other both within the same node and between different nodes.

***

## Necessary conditions <a href="#dieu-kien-can" id="dieu-kien-can"></a>

To be able to initialize a **Cluster** and **Deploy** a **Workload** , you need:

* There is at least 1 **VPC** and 1 **Subnet in ACTIVE** state . If you do not have any VPC, Subnet, please initialize VPC, Subnet according to the instructions below:
  * **Step 1**: Access the vServer homepage at the link [https://hcm-3.console.vngcloud.vn/vserver](https://hcm-3.console.vngcloud.vn/vserver)
  * **Step 2**: Select the **VPCs** menu in the left menu of the screen.
  * **Step 3**: Here, if you don't have any VPC yet, please select **Create VPC** by entering the **VPC name** and defining the desired **CIDR/16 range**.
  * **Step 4**: After having at least 1 VPC, to create a subnet, you need to select **View Detail** to expand the control panel at the bottom, including the **Subnet** section.
  * **Step 5**: In the **Subnet** section, select **Add Subnet**. Now, you need to enter:
    * **Subnet name**: the subnet's mnemonic name
    * **Primary CIDR** : :This is the primary IP address range of the subnet. All internal IP addresses of virtual machines (VMs) in this subnet will be taken from this address range. For example, if you set Primary CIDR to 10.1.0.0/16, the IP addresses of the VMs will be in the range of 10.1.0.1 to 10.1.255.254.
    * **Secondary CIDR** : This is a secondary IP address range, used to provide additional IP addresses or to separate different services within the same subnet. Each Node has a private IP address range for its pods (Pod CIDR). The pods in each node use addresses from this CIDR and communicate over the virtual network.

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* The IP address ranges of **Primary CIDR** and **Secondary CIDR** cannot overlap. This means that the address range of **Secondary CIDR** must be outside the range of **Primary CIDR** and vice versa. For example, if Primary CIDR is 10.1.0.0/16, then Secondary CIDR cannot be 10.1.0.0/20 because it is within the range of Primary CIDR. Instead, you can use a different address range like 10.2.0.0/20.
{% endhint %}

* There is at least 1 **SSH key in ACTIVE** state . If you do not have any SSH key, please initialize SSH key following the instructions here [.](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/security/ssh-key-bo-khoa)
* **kubectl** installed and configured on your device. please refer here [if](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) you are not sure how to install and use kuberctl. In addition, you should not use an outdated version of kubectl, we recommend that you use a kubectl version that is no more than one version different from the cluster version.

{% hint style="info" %}
**Hint:**

* When using Cilium's native routing mode, it is crucial to configure **Security Groups** correctly to allow necessary connections. For example, when running an NGINX pod on a node, you must permit traffic on port 80 to ensure requests from other nodes can connect. This configuration is not required when using the network overlay mode.
{% endhint %}



***

## **Create a Cluster using CNI Cilium VPC Native Routing** <a href="#khoi-tao-mot-cluster-su-dung-cni-cilium-vpc-native-routing" id="khoi-tao-mot-cluster-su-dung-cni-cilium-vpc-native-routing"></a>

To initialize a Cluster, follow the steps below:

**Step 1:** Access [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Step 2: On the Overview** screen , select **Activate.**

**Step 3:** Wait until we successfully initialize your VKS account. After successfully Activating, select **Create a Cluster.**

**Step 4:** At the Cluster initialization screen, we have set up the information for the Cluster and a **Default Node Group** for you. To use **CNI Cilium VPC Native Routing** for your **Cluster** , please select:

* **Network type** : Cilium VPC Native Routing and other parameters as follows:

| Field                    | Meaning                                                                                                                                                                                                                                                                                                                                                                             | Illustrative example                                                                                                                                                 |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **VPC**                  | The IP address range that the Cluster nodes will use to communicate.                                                                                                                                                                                                                                                                                                                | In the picture, we choose VPC with IP range **10.111.0.0/16** , corresponding to **65536 IPs**                                                                       |
| **Subnet**               | A smaller IP address range belonging to the VPC. Each node in the Cluster will be assigned an IP from this Subnet. The Subnet must be within the IP range of the selected VPC.                                                                                                                                                                                                      | In the picture, we choose Subnet with **Primary IP range** of **10.111.0.0/24** , corresponding to **256 IPs**                                                       |
| **Default Pod IP range** | This is the secondary IP address range used for pods. It is called **Secondary IP range** because it does not match the primary IP range of the node. Pods in the Cluster will be assigned IPs from this range.                                                                                                                                                                     | In the picture, we choose **Secondary IP range** as **10.111.160.0/20** - Corresponding to **4096 IPs** for pods                                                     |
| **Node CIDR mask size**  | CIDR size for nodes. This parameter indicates how many IP addresses each node will be assigned from the pod IP range. This size should be chosen to ensure that there are enough IP addresses for all pods on each node. You can refer to the table below to understand how to calculate the number of IP addresses that can be used to allocate to nodes and pods in your cluster. | In the picture, we choose **Node CIDR mask size** as **/25** - Each node will have **128 IP addresses** , suitable for the number of pods you want to run on a node. |

#### **Calculating the number of IPs for pods and nodes:** <a href="#cac-tinh-toan-so-luong-ip-cho-pod-va-node" id="cac-tinh-toan-so-luong-ip-cho-pod-va-node"></a>

<figure><img src="../../../.gitbook/assets/image (7) (1).png" alt="" width="563"><figcaption></figcaption></figure>

Suppose, when initializing the cluster, I choose:

* **VPC** : 10.111.0.0/16
* **Subnet:**
  * **Primary IP Range:** 10.111.0.0/24
  * **Secondary IP Range:** 10.111.160.0/20
* **Node CIDR mask size:** Selectable values ​​range from **/24** to **/26** .

| **Node CIDR mask size** | **Number of IPs per node** | **Number of nodes that can be created in the /20 range (4096 IPs)** | **Number of IPs allocated to pods on each node** | **Actual number of pods that can be created** |
| ----------------------- | -------------------------- | ------------------------------------------------------------------- | ------------------------------------------------ | --------------------------------------------- |
| **/24**                 | 256                        | 16                                                                  | 256                                              | 128                                           |
| **/25**                 | 128                        | 32                                                                  | 128                                              | 64                                            |
| **/26**                 | 64                         | 64                                                                  | 64                                               | 32                                            |

<figure><img src="../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* **Only one networktype:** In a cluster, you can use only one of three networktypes: Calico Overlay, Cilium Overlay, or Cilium VPC Native Routing
* **Multiple subnets for a cluster:** VKS supports the use of multiple subnets for a cluster. This allows you to configure each node group in the cluster to be located on different subnets within the same VPC, helping to optimize resource allocation and network management.
* **Cilium VPC Native Routing and Secondary IP Range** : When using Cilium VPC Native Routing for a cluster, you can use multiple Secondary IP Ranges. However, each Secondary IP Range can only be used by a single cluster. This helps avoid IP address conflicts and ensures consistency in network management.
* When there are not enough IP addresses in **the Node CIDR range** or **Secondary IP range** to create more nodes, specifically:
  * If you **cannot use the new Node because of** running out of IP addresses in **the Secondary IP range** . At this time, new nodes will still be created and joined to the cluster but you cannot use them. The pods that are required to launch on this new node will be stuck in the " **ContainerCreating** " state because no suitable node can be found to deploy. At this time, you need to create a new node group with a secondary IP range that is not used on any cluster.
{% endhint %}

**Step 5:** Select **Create Kubernetes cluster.** Please wait a few minutes for us to initialize your Cluster, the status of the Cluster is now **Creating** .

**Step 6: When the Cluster** status is **Active** , you can view Cluster information and Node Group information by selecting Cluster Name in the **Name** column .

***

## Deploy a Workload <a href="#deploy-mot-workload" id="deploy-mot-workload"></a>

Below are instructions for deploying an nginx deployment and testing IP assignment for the pods deployed in your cluster.

**Step 1:** Access [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** The Cluster list is displayed, select the icon **Download** and select **Download Config File** to download the kubeconfig file. This file will give you full access to your Cluster.

**Step 3** : Rename this file to config and save it to the **\~/.kube/config folder**

**Step 4:** Perform Cluster check via command:

* Run the following command to check **the node**

```bash
kubectl get nodes
```

* If the result is as below, it means your Cluster is successfully initialized with 3 nodes:

```bash
NAME                                           STATUS   ROLES    AGE     VERSION
vks-cluster-democilium-nodegroup-558f4-39206   Ready    <none>   5m35s   v1.28.8
vks-cluster-democilium-nodegroup-558f4-63344   Ready    <none>   5m45s   v1.28.8
vks-cluster-democilium-nodegroup-558f4-e6e4d   Ready    <none>   6m24s   v1.28.8
```

* Continue by running the following command to check the pods **deployed** on your kube-system namespace:

```bash
k get pods -A
```

* If the result is as below, it means that the **pods** supporting Cilium VPC Native have been running:

```bash
NAMESPACE     NAME                                          READY   STATUS    RESTARTS        AGE
kube-system   cilium-envoy-2g22l                            1/1     Running   0               6m41s
kube-system   cilium-envoy-h9mjb                            1/1     Running   0               5m53s
kube-system   cilium-envoy-ngz89                            1/1     Running   0               6m3s
kube-system   cilium-ft98g                                  1/1     Running   1 (5m33s ago)   6m2s
kube-system   cilium-operator-5fc5c56c4c-66l6d              1/1     Running   0               10m
kube-system   cilium-operator-5fc5c56c4c-qfnw2              1/1     Running   0               10m
kube-system   cilium-rfrr7                                  1/1     Running   1 (6m10s ago)   6m41s
kube-system   cilium-xmlq5                                  1/1     Running   1 (5m24s ago)   5m53s
kube-system   coredns-1727334052-85db76748b-fpmfr           1/1     Running   0               6m22s
kube-system   coredns-1727334052-85db76748b-jqv79           1/1     Running   0               6m22s
kube-system   hubble-relay-8578649fdb-bgzzz                 1/1     Running   1 (4m35s ago)   10m
kube-system   hubble-ui-574c5bb99b-g7l6c                    2/2     Running   0               10m
kube-system   konnectivity-agent-hmf2x                      1/1     Running   0               5m24s
kube-system   konnectivity-agent-q69n2                      1/1     Running   0               6m15s
kube-system   konnectivity-agent-wgqbw                      1/1     Running   0               5m14s
kube-system   vngcloud-controller-manager-d4d4f7b84-m65nb   1/1     Running   0               11m
kube-system   vngcloud-csi-controller-565c55dbcc-88pt4      7/7     Running   8 (4m59s ago)   11m
kube-system   vngcloud-csi-controller-565c55dbcc-v22q4      7/7     Running   8 (4m59s ago)   11m
kube-system   vngcloud-csi-node-665r2                       3/3     Running   3 (5m15s ago)   6m41s
kube-system   vngcloud-csi-node-8x542                       3/3     Running   3 (52s ago)     6m3s
kube-system   vngcloud-csi-node-gx7zd                       3/3     Running   2 (83s ago)     5m53s
kube-system   vngcloud-ingress-controller-0                 1/1     Running   1 (5m55s ago)   11m
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

* You can observe below, the **nginx pods** are assigned IPs 10.111.16x.x which satisfy **the Secondary IP range and Node CIDR mask size** conditions that we specified above:

```bash
NAME                         READY   STATUS    RESTARTS   AGE   IP               NODE                                           
nginx-app-7c79c4bf97-6v88s   1/1     Running   0          31s   10.111.161.53    vks-cluster-democilium-nodegroup-558f4-39206   
nginx-app-7c79c4bf97-754m7   1/1     Running   0          31s   10.111.161.1     vks-cluster-democilium-nodegroup-558f4-39206   
nginx-app-7c79c4bf97-9tjw7   1/1     Running   0          31s   10.111.160.212   vks-cluster-democilium-nodegroup-558f4-63344   
nginx-app-7c79c4bf97-c6vx7   1/1     Running   0          31s   10.111.160.46    vks-cluster-democilium-nodegroup-558f4-e6e4d   
nginx-app-7c79c4bf97-c7nch   1/1     Running   0          31s   10.111.161.3     vks-cluster-democilium-nodegroup-558f4-39206   
nginx-app-7c79c4bf97-cggfq   1/1     Running   0          31s   10.111.161.74    vks-cluster-democilium-nodegroup-558f4-39206   
nginx-app-7c79c4bf97-cz4xc   1/1     Running   0          31s   10.111.160.115   vks-cluster-democilium-nodegroup-558f4-e6e4d   
nginx-app-7c79c4bf97-d84rb   1/1     Running   0          31s   10.111.160.152   vks-cluster-democilium-nodegroup-558f4-63344   
nginx-app-7c79c4bf97-dbmt7   1/1     Running   0          31s   10.111.160.184   vks-cluster-democilium-nodegroup-558f4-63344   
nginx-app-7c79c4bf97-gtx8b   1/1     Running   0          31s   10.111.161.57    vks-cluster-democilium-nodegroup-558f4-39206   
nginx-app-7c79c4bf97-km7tx   1/1     Running   0          31s   10.111.160.94    vks-cluster-democilium-nodegroup-558f4-e6e4d   
nginx-app-7c79c4bf97-lmk7c   1/1     Running   0          31s   10.111.161.26    vks-cluster-democilium-nodegroup-558f4-39206   
nginx-app-7c79c4bf97-mc24h   1/1     Running   0          31s   10.111.160.98    vks-cluster-democilium-nodegroup-558f4-e6e4d   
nginx-app-7c79c4bf97-n4zvf   1/1     Running   0          31s   10.111.160.204   vks-cluster-democilium-nodegroup-558f4-63344   
nginx-app-7c79c4bf97-n84tc   1/1     Running   0          31s   10.111.161.106   vks-cluster-democilium-nodegroup-558f4-39206   
nginx-app-7c79c4bf97-qtjjx   1/1     Running   0          31s   10.111.160.32    vks-cluster-democilium-nodegroup-558f4-e6e4d   
nginx-app-7c79c4bf97-rp4bt   1/1     Running   0          31s   10.111.160.202   vks-cluster-democilium-nodegroup-558f4-63344   
nginx-app-7c79c4bf97-sk7tf   1/1     Running   0          31s   10.111.160.196   vks-cluster-democilium-nodegroup-558f4-63344   
nginx-app-7c79c4bf97-x8jxm   1/1     Running   0          31s   10.111.160.135   vks-cluster-democilium-nodegroup-558f4-63344   
nginx-app-7c79c4bf97-zlstg   1/1     Running   0          31s   10.111.160.121   vks-cluster-democilium-nodegroup-558f4-e6e4d 
```

* You can also perform a detailed description of each pod to check this pod information via the command:

```bash
kubectl describe pod nginx-app-7c79c4bf97-6v88s
```

**Step 4: There are a few steps you can take to thoroughly test the performance of Cilium. Specifically:**

* First, you need to install Cilium CLI following the instructions [here](https://docs.cilium.io/en/stable/gettingstarted/k8s-install-default/#install-the-cilium-cli) .
* After installing Cilium CLS, check **the status** of Cilium in your cluster via the command:

```bash
cilium status wait
```

* If the result is displayed as below, it means that **Cilium** is **working properly and fully** :

```bash
    /¯¯\
 /¯¯\__/¯¯\    Cilium:             OK
 \__/¯¯\__/    Operator:           OK
 /¯¯\__/¯¯\    Envoy DaemonSet:    OK
 \__/¯¯\__/    Hubble Relay:       OK
    \__/       ClusterMesh:        disabled

DaemonSet              cilium-envoy       Desired: 3, Ready: 3/3, Available: 3/3
Deployment             hubble-relay       Desired: 1, Ready: 1/1, Available: 1/1
Deployment             hubble-ui          Desired: 1, Ready: 1/1, Available: 1/1
Deployment             cilium-operator    Desired: 2, Ready: 2/2, Available: 2/2
DaemonSet              cilium             Desired: 3, Ready: 3/3, Available: 3/3
Containers:            hubble-ui          Running: 1
                       cilium-operator    Running: 2
                       cilium             Running: 3
                       cilium-envoy       Running: 3
                       hubble-relay       Running: 1
Cluster Pods:          32/32 managed by Cilium
Helm chart version:
Image versions         cilium             vcr.vngcloud.vn/81-vks-public/cilium/cilium:v1.16.1: 3
                       cilium-envoy       vcr.vngcloud.vn/81-vks-public/cilium/cilium-envoy:v1.29.7-39a2a56bbd5b3a591f69dbca51d3e30ef97e0e51: 3
                       hubble-relay       vcr.vngcloud.vn/81-vks-public/cilium/hubble-relay:v1.16.1: 1
                       hubble-ui          vcr.vngcloud.vn/81-vks-public/cilium/hubble-ui-backend:v0.13.1: 1
                       hubble-ui          vcr.vngcloud.vn/81-vks-public/cilium/hubble-ui:v0.13.1: 1
                       cilium-operator    vcr.vngcloud.vn/81-vks-public/cilium/operator-generic:v1.16.1: 2
```

**Step 5: You can perform a healthy check to check Cilium in your cluster**

* Run the following command to perform a healthy check

```bash
kubectl -n kube-system exec ds/cilium -- cilium-health status --probe
```

* Reference results

```bash
Probe time:   2024-09-26T07:11:57Z
Nodes:
  vks-cluster-democilium-nodegroup-558f4-e6e4d (localhost):
    Host connectivity to 10.111.0.8:
      ICMP to stack:   OK, RTT=306.523µs
      HTTP to agent:   OK, RTT=206.191µs
    Endpoint connectivity to 10.111.160.91:
      ICMP to stack:   OK, RTT=307.205µs
      HTTP to agent:   OK, RTT=365.113µs
  vks-cluster-democilium-nodegroup-558f4-39206:
    Host connectivity to 10.111.0.14:
      ICMP to stack:   OK, RTT=1.90859ms
      HTTP to agent:   OK, RTT=344.725µs
    Endpoint connectivity to 10.111.161.9:
      ICMP to stack:   OK, RTT=1.889682ms
      HTTP to agent:   OK, RTT=549.887µs
  vks-cluster-democilium-nodegroup-558f4-63344:
    Host connectivity to 10.111.0.9:
      ICMP to stack:   OK, RTT=1.920985ms
      HTTP to agent:   OK, RTT=706.376µs
    Endpoint connectivity to 10.111.160.223:
      ICMP to stack:   OK, RTT=1.919709ms
      HTTP to agent:   OK, RTT=1.090877ms
```

Additionally, you can also perform additional End-to-End connectivity tests or Network performance tests following the instructions at [End-To-End Connectivity Testing](https://docs.cilium.io/en/stable/contributing/testing/e2e/) or [Network Performance Test](https://docs.cilium.io/en/stable/contributing/testing/e2e/#network-performance-test) .

**Step 6: Check the connection between Pods**

* Perform a connectivity test between pods, ensuring that the **pods can communicate via the VPC IP address without going through overlay networks** . For example, below I perform a ping from the pod nginx-app-7c79c4bf97-6v88s with IP address: 10.111.161.53 to a server in the same VPC with IP address: 10.111.0.10:

```bash
kubectl exec -it nginx-app-7c79c4bf97-6v88s -- ping 10.111.0.10
```

* If the result is as follows, the connection is successful:

```bash
PING 10.111.0.10 (10.111.0.10): 56 data bytes
64 bytes from 10.111.0.10: seq=0 ttl=62 time=3.327 ms
64 bytes from 10.111.0.10: seq=1 ttl=62 time=0.541 ms
64 bytes from 10.111.0.10: seq=2 ttl=62 time=0.472 ms
64 bytes from 10.111.0.10: seq=3 ttl=62 time=0.463 ms
--- 10.111.0.10 ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 0.463/1.200/3.327 ms
```
