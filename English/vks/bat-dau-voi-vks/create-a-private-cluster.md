# Create a Private Cluster

Previously, public clusters on VKS were using Public IP addresses to communicate between nodes and the control plane. To improve the security of your cluster, we have launched the private cluster model. The Private Cluster feature helps your K8S cluster to be as secure as possible, all connections are completely private from the connection between nodes to the control plane, the connection from the client to the control plane, or the connection from nodes to other products and services in VNG Cloud such as: vStorage, vCR, vMonitor, VNGCloud APIs,... Private Cluster is the ideal choice for services that require strict access control, ensuring compliance with regulations on security and data privacy.

## Model <a href="#khoitaomotpublicclustervoiprivatenodegroup-dieukiencan" id="khoitaomotpublicclustervoiprivatenodegroup-dieukiencan"></a>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FejaDqxomA5i6nvC2Dlay%252Fimage.png%3Falt%3Dmedia%26token%3Db701029d-0a23-4685-996d-9b8dc03d705a&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ccccfdc5&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**In which:**

* **Control plane** : Managed by VNG Cloud, responsible for coordinating and managing the entire cluster.
* **Nodes** : When created, Nodes in the Cluster will only have internal IPs and cannot go to the public internet. If you want the node to access the internet, you need to use a NAT Gateway. For more details, refer [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/bat-dau-voi-vks/khoi-tao-mot-public-cluster/khoi-tao-mot-public-cluster-voi-private-node-group/pfsense-as-a-nat-gateway) .
* **Private Load Balancer** : Managed by VNG Cloud, responsible for helping Private Nodes communicate with Control Plane.
* **Private Service Endpoint** : When you create a private cluster, the system automatically creates 4 endpoints to help connect to other services on VNG Cloud including:
  * **Endpoint** to connect to the **IAM** service (Endpoint Name: vks-iam-endpoint-...)
  * **Endpoint** to connect to **vCR** service (Endpoint Name: vks-vcr-endpoint-...)
  * **Endpoint to connect to vServer** service (Endpoint Name: vks-vserver-endpoint-...)
  * **Endpoint** to connect to **vStorage** service (Endpoint Name: vks-vstorage-endpoint-...)

You can view information about the 4 private service endpoints through the vServer portal by following the link [here](https://hcm-3.console.vngcloud.vn/vserver/vnetwork/endpoint/list) .

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FOdI0xwO1gNS0GDkVkxbl%252Fimage.png%3Falt%3Dmedia%26token%3D010cc2be-311d-48d0-8005-c0ca67536fd3&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4d3f8c2d&#x26;sv=1" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Warning:**

*   <mark style="color:red;background-color:red;">**Do not delete Private Service Endpoints**</mark> <mark style="color:red;background-color:red;">:</mark> To ensure stable operation of the cluster, you should not delete the 4 pre-created service endpoints. If you accidentally delete or edit these 4 endpoints, within a maximum of 5 minutes, the system will automatically recreate them but may cause disruption to running services. At this time, because the recreated service endpoint may have changed the Endpoint IP compared to the original, in order for the cluster to work, you need to manually add Endpoint IP to the previously running servers via command:

    ```
    vks-bootstraper add-host -i <IP> -d <DOMAIN>
    ```

    Example, if you delete private service endpoint of vCR, you must add host via command:

    ```
    vks-boostraper add-host -i 10.10.10.10 -d vcr.vngcloud.vn
    ```
* <mark style="color:red;background-color:red;">**Reuse Private Service Endpoints**</mark>**:** Service endpoints can be used by multiple private clusters. When private clusters share a VPC, we will reuse them for these clusters.
* <mark style="color:red;background-color:red;">**Delete Private Service Endpoints automatically:**</mark> When you delete a cluster, if there are no more clusters that reuse these service endpoints, the system will automatically delete them.
* <mark style="color:red;background-color:red;">**Cost of using Private Service Endpoint:**</mark> Using a private cluster will incur additional costs for 4 private service endpoints, but it brings many security benefits to your project. Please carefully consider the factors to decide whether to use public or private for your cluster.
{% endhint %}

***

## Prerequisites <a href="#khoitaomotpublicclustervoiprivatenodegroup-dieukiencan-1" id="khoitaomotpublicclustervoiprivatenodegroup-dieukiencan-1"></a>

To be able to initialize a **Cluster** and **Deploy** a **Workload** , you need:

* There is at least 1 **VPC** and 1 **Subnet in ACTIVE** state . If you do not have a VPC or Subnet yet, please create a VPC and Subnet according to the instructions here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc)
* There is at least 1 **SSH key in ACTIVE** state . If you do not have any SSH key, please create an SSH key according to the instructions here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/security/ssh-key-bo-khoa)
* Installed and configured **kubectl** on your device. Please refer here [if](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) you are not sure how to install and use kuberctl. In addition, you should not use a kubectl version that is too old, we recommend that you use a kubectl version that is no more than one version different from the cluster version.

***

## Initialize Cluster <a href="#khoitaomotpublicclustervoiprivatenodegroup-khoitaocluster" id="khoitaomotpublicclustervoiprivatenodegroup-khoitaocluster"></a>

**A cluster in Kubernetes** is a collection of one or more virtual machines (VMs) connected together to run containerized applications. Cluster provides a unified environment to deploy, manage, and operate containers at scale.

To initialize a Cluster, follow the steps below:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select **Activate.**

**Step 3:** Wait until we successfully create your VKS account. After Activate successfully, select **Create a Cluster**

**Step 4:** At the Cluster initialization screen, we have set up information for the Cluster and a **Default Node Group** for you. You can keep these default values ​​or adjust the desired parameters for the Cluster and Node Group at Cluster Configuration, Default Node Group Configuration, Plugin.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fk4TCpipxdEvY9kVAQ8gd%252Fimage.png%3Falt%3Dmedia%26token%3D1c7c2cd2-174a-49de-af92-677017044547&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=776c0c18&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 5:** Select **Create Kubernetes cluster.** Please wait a few minutes for us to initialize your Cluster, the Cluster's status is now **Creating** .

**Step 6: When the Cluster** status is **Active** , you can view Cluster information and Node Group information by selecting Cluster Name in the **Name** column .

{% hint style="info" %}
**Warning:**

* **A Cluster** can have **many Node Groups** , each Node Group can operate in Public/Private mode depending on your needs.
* Because your **Cluster** is initialized in **Private** mode , to be able to access Control Plane's **kube-api , you need to be in the VPC** you choose to use for your Cluster.
{% endhint %}

***

## Connect and check the newly created Cluster information <a href="#khoitaomotpublicclustervoiprivatenodegroup-ketnoivakiemtrathongtinclustervuatao" id="khoitaomotpublicclustervoiprivatenodegroup-ketnoivakiemtrathongtinclustervuatao"></a>

After the Cluster is successfully initialized, you can connect and check the newly created Cluster information by following these steps:

**Step 1:** Visit [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** The Cluster list is displayed, select the **Download** icon and select **Download config file** to download the kubeconfig file. This file will give you full access to your Cluster.

**Step 3** : Rename this file to config and save it to the **\~/.kube/config folder**

**Step 4:** Because your Cluster is initialized in Private mode, to be able to access kube-api, you need to be in the VPC you have chosen to use for your Cluster. For example, when you are not in the VPC and execute get nodes, the results will display as follows:

```
kubectl get nodes
E0821 14:27:03.793829   23348 memcache.go:265] couldn't get current server API group list: Get "https://10.7.8.9:6443/api?timeout=32s": dial tcp 10.7.8.9:6443: connectex: No connection could be made because the target machine actively refused it.
E0821 14:27:05.866230   23348 memcache.go:265] couldn't get current server API group list: Get "https://10.7.8.9:6443/api?timeout=32s": dial tcp 10.7.8.9:6443: connectex: No connection could be made because the target machine actively refused it.
E0821 14:27:07.922272   23348 memcache.go:265] couldn't get current server API group list: Get "https://10.7.8.9:6443/api?timeout=32s": dial tcp 10.7.8.9:6443: connectex: No connection could be made because the target machine actively refused it.
E0821 14:27:09.989832   23348 memcache.go:265] couldn't get current server API group list: Get "https://10.7.8.9:6443/api?timeout=32s": dial tcp 10.7.8.9:6443: connectex: No connection could be made because the target machine actively refused it.
E0821 14:27:12.055864   23348 memcache.go:265] couldn't get current server API group list: Get "https://10.7.8.9:6443/api?timeout=32s": dial tcp 10.7.8.9:6443: connectex: No connection could be made because the target machine actively refused it.
Unable to connect to the server: dial tcp 10.7.8.9:6443: connectex: No connection could be made because the target machine actively refused it.
```

In the example below I will stand at a server with a VPC along with the VPC used for the Cluster. You can perform SSH to the server according to instructions [here](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/server/ket-noi-vao-may-chu-ao/ket-noi-vao-may-chu-linux-bang-cong-cu-ssh-client) . After SSH into the server, install kubectl according to the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/bat-dau-voi-vks/huong-dan-cai-dat-va-cau-hinh-cong-cu-kubectl-trong-kubernetes) .

* For example, I am using a linux server to perform get nodes, I can install kubectl via command:

```
sudo snap install kubectl --classic
```

* Then I tested kubectl via command:

```
kubectl version
```

* Create folder . `kube` via command:

```
mkdir -p .kube
```

* Then, enter the kubeconfig file via the command:

```
vim .kube/config
```

* Then, enter **:wq** to save the kubeconfig file and exit vim.
* Run the following command to test **the cluster**

```
kubectl get svc
```

* You should see a return similar to the following:

```
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   10m
```

* Run the following command to test **node**

```
kubectl get nodes
```

* If the results are returned as below, it means your Cluster was successfully initialized with 1 node as below.

```
NAME                                    STATUS   ROLES    AGE     VERSION
vks-demo-cluster-nodegroup-demo-7c9aa   Ready    <none>   8m11s   v1.28.8
```

***

## Use Docker to Pull/Push images <a href="#khoitaomotpublicclustervoiprivatenodegroup-deploymotworkload" id="khoitaomotpublicclustervoiprivatenodegroup-deploymotworkload"></a>

Because Private Cluster can only connect privately to the vContainer Registry (vCR) system and cannot connect to other Container Registry outside the internet, you need to pull/push the image to vCR to use according to the following instructions:

**Step 1: Install Docker**

* Perform docker installation according to instructions [here](https://docs.docker.com/engine/install/) .

**Step 2: Initialize Public Repository and Repository User on vContainer Registry Portal:**

* Log in to the vCR portal at the link: [https://vcr.console.vngcloud.vn/list](https://vcr.console.vngcloud.vn/list)
* Perform Repository and Repository initialization according to instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vcontainer-registry/repository) . For example in the image below, I have initialized demo\_repo with demo\_user who can pull/push images:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FldaY7D8dz9T0h70dePRs%252Fimage.png%3Falt%3Dmedia%26token%3D75575e6c-c13f-4d72-a6d3-f8be61eb527b&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=8e092c75&#x26;sv=1" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FT7EiVWsVTgFyxkMueW1X%252Fimage.png%3Falt%3Dmedia%26token%3Dbef87be7-4e12-431e-8eb7-779c9e4cc813&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=937194ae&#x26;sv=1" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Warning:**

* If you want to create a Private Reposity, to pull an image from the Private Reposity, you need to create a secret key according to the instructions [here](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/) .
{% endhint %}

**Step 3:** Pull the nginx image according to the command:

```
docker pull nginx:latest
```

**Step 4:** Log in to vCR via command:

```
docker login vcr.vngcloud.vn -u <repository_user>
```

* For example, the command below I use to login to the demo repo:

```
docker login vcr.vngcloud.vn -u 53461-user_demo
```

**Step 5:** Assign tags to the nginx image

```
docker tag SOURCE_IMAGE[:TAG] vcr.vngcloud.vn/REPO_NAME/IMAGE[:TAG]
```

* For example, the command below I use to assign tags to the nginx image:

```
docker tag nginx:latest vcr.vngcloud.vn/53461-repo_demo/nginx-demo:latest
```

**Step 6:** Push the image to the repo via command:

```
docker push vcr.vngcloud.vn/REPO_NAME/IMAGE[:TAG]
```

* For example, the command below I use to push images to demo\_repo:

```
docker push vcr.vngcloud.vn/53461-repo_demo/nginx-demo:latest
```

***

## Deploy a Workload <a href="#khoitaomotpublicclustervoiprivatenodegroup-deploymotworkload-1" id="khoitaomotpublicclustervoiprivatenodegroup-deploymotworkload-1"></a>

The following are instructions for you to deploy the nginx service and expose this service via Network Load Balancer

**Step 1: Create the nginx-service-lb4.yaml file via the command:**

```
vi nginx.yaml
```

Then, enter the content for this file as follows: you need to replace the image with the image path saved on the vCR that you pushed in the step above:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-app
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 1
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: vcr.vngcloud.vn/53461-repo_demo/nginx-demo:latest
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  type: LoadBalancer 
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

* Enter **:wq** to save this file.
* Deploy This deployment equals:

```
kubectl apply -f nginx-service-lb4.yaml
```

***

**Step 2: Check Deployment and Service information before exposing it to the Internet.**

* Run the following command to test **Deployment**

```
kubectl get svc,deploy,pod -owide
```

* If the results are returned as below, it means you have successfully deployed the nginx service.

```
NAME                    TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)        AGE     SELECTOR
service/kubernetes      ClusterIP      10.96.0.1      <none>           443/TCP        91m     <none>
service/nginx-service   LoadBalancer   10.96.81.236   116.118.88.236   80:32333/TCP   3m32s   app=nginx

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES                                              SELECTOR
deployment.apps/nginx-app   1/1     1            1           3m32s   nginx        vcr.vngcloud.vn/53461-repo_demo/nginx-demo:latest   app=nginx

NAME                             READY   STATUS    RESTARTS   AGE     IP             NODE                                    NOMINATED NODE   READINESS GATES
pod/nginx-app-56bbc8fdd8-4pz68   1/1     Running   0          3m32s   172.16.4.207   vks-demo-cluster-nodegroup-demo-7c9aa   <none>           <none>
```

***

At this time, the vLB system will initialize a Network Load Balancer, you can view this LB information through the vLB portal [here](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb) .

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FLPLkTsdXXDMLkLwIafyq%252Fimage.png%3Falt%3Dmedia%26token%3Dfd8288ed-2324-4974-92af-61f0983ae6de&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b48c6767&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 3: To access the just exported nginx app, you can use the Endpoint of Load Balancer URL with the format:**

```
http://Endpoint/
```

You can get Load Balancer Public Endpoint information at the vLB interface. Specifically, access at [https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb/](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb/detail/lb-927c0b5f-5bcf-4ee1-b645-41d6a0caeecb)

For example, below I have successfully accessed the nginx app with the address: [http://116.118.88.236/](http://116.118.88.236/)

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F8W2DNtIT9yNuMusAMIjC%252Fimage.png%3Falt%3Dmedia%26token%3D7168ca69-64b8-47bc-8bc2-684fc32f22bd&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c50443ac&#x26;sv=1" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**A few other notes:**

* Above is an example showing you how to expose a service through vLB Layer 4. You can expose a service through vLB Layer 7 according to the instructions [here](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vks/bat-dau-voi-vks/expose-mot-service-thong-qua-vlb-layer7) .
* To ensure the private cluster works effectively, we have automatically added the Subnet you choose to use for the Cluster to the cluster's Whitelist. You can use the Whitelist feature to limit the Subnets in the VPC that have access to kube-api. Details on how to use the Whitelist feature please refer [here](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vks/clusters/whitelist) .
{% endhint %}
