# Expose a service through vLB Layer4

## Prerequisites <a href="#exposemotservicethongquavlblayer4-dieukiencan" id="exposemotservicethongquavlblayer4-dieukiencan"></a>

To be able to initialize a **Cluster** and **Deploy** a **Workload** , you need:

* There is at least 1 **VPC** and 1 **Subnet in ACTIVE** state . If you do not have a VPC or Subnet yet, please create a VPC or Subnet according to the instructions here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc)
* There is at least 1 **SSH key in ACTIVE** state . If you do not have any SSH key, please create an SSH key according to the instructions here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/security/ssh-key-bo-khoa)
* Installed and configured **kubectl** on your device. Please refer here [if](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) you are not sure how to install and use kuberctl. In addition, you should not use a kubectl version that is too old, we recommend that you use a kubectl version that is no more than one version different from the cluster version.

***

## Initialize Cluster <a href="#exposemotservicethongquavlblayer4-khoitaocluster" id="exposemotservicethongquavlblayer4-khoitaocluster"></a>

**A cluster in Kubernetes** is a collection of one or more virtual machines (VMs) connected together to run containerized applications. Cluster provides a unified environment to deploy, manage, and operate containers at scale.

To initialize a Cluster, follow the steps below:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select **Activate.**

**Step 3:** Wait until we successfully create your VKS account. After Activate successfully, select **Create a Cluster**

**Step 4:** At the Cluster initialization screen, we have set up information for the Cluster and a **Default Node Group** for you. You can keep these default values ​​or adjust the desired parameters for the Cluster and Node Group at Cluster Configuration, Default Node Group Configuration, Plugin. **When you choose to enable option**![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762054%2Fimage2024-4-16\_14-18-22.png%3Fversion%3D1%26modificationDate%3D1713251905000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=8cf23091\&sv=1)**, by default we will pre-install this plugin into your Cluster.**

**Step 5:** Select **Create Kubernetes cluster.** Please wait a few minutes for us to initialize your Cluster, the Cluster's status is now **Creating** .

**Step 6: When the Cluster** status is **Active** , you can view Cluster information and Node Group information by selecting Cluster Name in the **Name** column .

***

## Connect and check the newly created Cluster information <a href="#exposemotservicethongquavlblayer4-ketnoivakiemtrathongtinclustervuatao" id="exposemotservicethongquavlblayer4-ketnoivakiemtrathongtinclustervuatao"></a>

After the Cluster is successfully initialized, you can connect and check the newly created Cluster information by following these steps:

**Step 1:** Visit [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** The Cluster list is displayed, select the icon![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762054%2Fimage2024-4-4\_14-37-11.png%3Fversion%3D1%26modificationDate%3D1712222503000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=f64230d8\&sv=1)and select **Download Config File** to download the kubeconfig file. This file will give you full access to your Cluster.

**Step 3** : Rename this file to config and save it to the **\~/.kube/config directory**

**Step 4:** Perform Cluster check via command:

* Run the following command to test **node**

```
kubectl get nodes
```

* If the results are returned as below, it means your Cluster was successfully initialized with 3 nodes as below.

```
NAME                                            STATUS     ROLES    AGE   VERSION
ng-0e10592c-e70e-404d-a4e8-5e3b80f805e4-834b7   Ready      <none>   50m   v1.28.8
ng-0e10592c-e70e-404d-a4e8-5e3b80f805e4-cf652   Ready      <none>   23m   v1.28.8
ng-0f4ed631-1252-49f7-8dfc-386fa0b2d29b-a8ef0   Ready      <none>   28m   v1.28.8
```

***

## Create Service Account and install VNGCloud LoadBalancer Controller <a href="#exposemotservicethongquavlblayer4-khoitaoserviceaccountvacaidatvngcloudcontrollermanager" id="exposemotservicethongquavlblayer4-khoitaoserviceaccountvacaidatvngcloudcontrollermanager"></a>

{% hint style="info" %}
**Note:**

When you initialize the Cluster according to the instructions above, if you have not enabled the **Enable vLB Native Integration Driver** option , by default we will not pre-install this plugin into your Cluster. You need to manually create Service Account and install VNGCloud LoadBalancer Controller according to the instructions below. If you have enabled the **Enable vLB Native Integration Driver** option , then we have pre-installed this plugin into your Cluster, skip the Service Account Initialization step, install VNGCloud LoadBalancer Controller and continue following the instructions from Deploy once. Workload.
{% endhint %}

<details>

<summary>Instructions for creating Service Account and installing VNGCloud LoadBalancer Controller</summary>

**Initialize Service Account**

* Create or use a **service account** created on IAM and attach policy: **vLBFullAccess** , **vServerFullAccess** . To create a service account, go here [and](https://iam.console.vngcloud.vn/service-accounts) follow these steps:
  * Select " **Create a Service Account** ", enter a name for the Service Account and click **Next Step** to assign permissions to the Service Account
  * Find and select **Policy: vLBFullAccess and Policy: vServerFullAccess** , then click " **Create a Service Account** " to create Service Account, Policy: vLBFullAccess and Policy: vServerFullAccess created by GreenNode, you cannot delete these policies.
  * After successful creation, you need to save **the Client\_ID** and **Secret\_Key** of the Service Account to perform the next step.
* Uninstall cloud-controller-manager

```
kubectl get daemonset -n kube-system | grep -i "cloud-controller-manager"

# if your output is similar to the following, you MUST delete the old plugin
kubectl delete daemonset cloud-controller-manager -n kube-system --force
```

* Besides, you can delete the Service Account being used for the cloud-controller-manager you just removed

```
kubectl get sa -n kube-system | grep -i "cloud-controller-manager"

# if your output is similar to the above, you MUST delete this service account
kubectl delete sa cloud-controller-manager -n kube-system --force
```

**Install VNGCloud LoadBalancer Controller**

* Install Helm version 3.0 or higher. Refer to [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/) for instructions on how to install.
* Add this repo to your cluster via the command:

```
helm repo add vks-helm-charts https://vngcloud.github.io/vks-helm-charts
helm repo update
```

* Replace your K8S cluster's ClientID, Client Secret, and ClusterID information and continue running:

```
helm install  vngcloud-controller-manager vks-helm-charts/vngcloud-controller-manager --replace \
  --namespace kube-system \
  --set cloudConfig.global.clientID= <Lấy ClientID của Service Account được tạo trên IAM theo hướng dẫn bên trên> \
  --set cloudConfig.global.clientSecret= <Lấy ClientSecret của Service Account được tạo trên IAM theo hướng dẫn bên trên>\
  --set cluster.clusterID= <Lấy Cluster ID của cluster mà bạn đã khởi tạo trước đó>
```

* After the installation is complete, check the status of vngcloud-Integrate-controller pods:

```
kubectl get pods -n kube-system | grep vngcloud-controller-manager
```

For example, in the image below you have successfully installed vngcloud-controller-manager:

```
NAME                                          READY   STATUS    RESTARTS      AGE
vngcloud-controller-manager-8864c754c-bqhvz   1/1     Running   5 (91s ago)   3m13sc
```

</details>

***

## Deploy a Workload <a href="#exposemotservicethongquavlblayer4-deploymotworkload" id="exposemotservicethongquavlblayer4-deploymotworkload"></a>

The following is a guide for you to deploy the nginx service on Kubernetes.

### **Step 1** : **Create Deployment, Service for Nginx app.**

* Create **nginx-service-lb4.yaml** file with the following content:

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
        image: nginx:1.19.1
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

* Deploy this Service using:

```
kubectl apply -f nginx-service-lb4.yaml
```

***

### **Step 2: Check the Deployment and Service information just deployed**

* Run the following command to test **Deployment**

```
kubectl get svc,deploy,pod -owide
```

* If the results are returned as below, it means you have deployed Deployment successfully.

```
NAME                    TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE     SELECTOR
service/kubernetes      ClusterIP      10.96.0.1      <none>        443/TCP        5h15m   <none>
service/nginx-service   LoadBalancer   10.96.74.154   <pending>     80:31623/TCP   2s      app=nginx

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
deployment.apps/nginx-app   0/1     1            0           2s    nginx        nginx:1.19.1   app=nginx

NAME                             READY   STATUS              RESTARTS   AGE   IP       NODE                                            NOMINATED NODE   READINESS GATES
pod/nginx-app-7f45b65946-bmrcf   0/1     ContainerCreating   0          2s    <none>   ng-e0fc7245-0c6e-4336-abcc-31a70eeed71d-46179   <none>           <non
```

At this point, the vLB system will automatically create a corresponding LB for the deployed nginx app, for example:

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FzD11c32iEIzE2hnbzbrv%252Fimage.png%3Falt%3Dmedia%26token%3D8010e3b8-fb5b-428a-9940-e7ff245895d2\&width=768\&dpr=4\&quality=100\&sign=58607080\&sv=1)

### **Step 3: To access the just exported nginx app, you can use the URL with the format:**

```
http://Endpoint/
```

You can get Load Balancer Public Endpoint information at the vLB interface. Specifically, access at [https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb/](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb/detail/lb-927c0b5f-5bcf-4ee1-b645-41d6a0caeecb)

For example, below I have successfully accessed the nginx app with the address: [http://180.93.181.20/](http://180.93.181.20/)

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FWRLfY9NlcRgvi7B2c3b7%252Fimage.png%3Falt%3Dmedia%26token%3D9aea9889-1f6f-478a-889e-8b936c2b3bb6&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b1f9d46b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

You can see more about ALB at [Working with Network load balancing (NLB)](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/network/lam-viec-voi-network-load-balancing-nlb) .

{% hint style="info" %}
**Attention:**

* Changing the name or size (Rename, Resize) of the Load Balancer resource on vServer Portal can cause incompatibility with resources on the Kubernetes Cluster. This can lead to resources becoming inactive on the Cluster, or resources being resynchronized, or resource information between vServer Portal and the Cluster not matching. To prevent this problem, use `kubectl`Cluster resource management.
{% endhint %}
