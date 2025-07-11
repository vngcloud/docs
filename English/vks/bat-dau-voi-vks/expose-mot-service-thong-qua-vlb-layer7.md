# Expose a service through vLB Layer7

## Prerequisites <a href="#exposemotservicethongquavlblayer7-dieukiencan" id="exposemotservicethongquavlblayer7-dieukiencan"></a>

To be able to initialize a **Cluster** and **Deploy** a **Workload** , you need:

* There is at least 1 **VPC** and 1 **Subnet in ACTIVE** state . If you do not have a VPC or Subnet yet, please create a VPC or Subnet according to the instructions here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc)
* There is at least 1 **SSH key in ACTIVE** state . If you do not have any SSH key, please create an SSH key according to the instructions here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc)
* Installed and configured **kubectl** on your device. Please refer here [if](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) you are not sure how to install and use kuberctl. In addition, you should not use a kubectl version that is too old, we recommend that you use a kubectl version that is no more than one version different from the cluster version.

***

## Initialize Cluster <a href="#exposemotservicethongquavlblayer7-khoitaocluster" id="exposemotservicethongquavlblayer7-khoitaocluster"></a>

**A cluster in Kubernetes** is a collection of one or more virtual machines (VMs) connected together to run containerized applications. Cluster provides a unified environment to deploy, manage, and operate containers at scale.

To initialize a Cluster, follow the steps below:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select **Activate.**

**Step 3:** Wait until we successfully create your VKS account. After Activate successfully, select **Create a Cluster**

**Step 4:** At the Cluster initialization screen, we have set up information for the Cluster and a **Default Node Group** for you. You can keep these default values ​​or adjust the desired parameters for the Cluster and Node Group at Cluster Configuration, Default Node Group Configuration, Plugin. **When you choose to enable option**![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762059%2Fimage2024-4-16_14-18-22.png%3Fversion%3D1%26modificationDate%3D1713252320000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=fc29a090\&sv=1) **, by default we will pre-install this plugin into your Cluster.**

**Step 5:** Select **Create Kubernetes cluster.** Please wait a few minutes for us to initialize your Cluster, the Cluster's status is now **Creating** .

**Step 6: When the Cluster** status is **Active** , you can view Cluster information and Node Group information by selecting Cluster Name in the **Name** column .

***

## Connect and check the newly created Cluster information <a href="#exposemotservicethongquavlblayer7-ketnoivakiemtrathongtinclustervuatao" id="exposemotservicethongquavlblayer7-ketnoivakiemtrathongtinclustervuatao"></a>

After the Cluster is successfully initialized, you can connect and check the newly created Cluster information by following these steps:

**Step 1:** Visit [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** The Cluster list is displayed, select the icon![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762059%2Fimage2024-4-4_14-37-11.png%3Fversion%3D1%26modificationDate%3D1712222544000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=87ec4908\&sv=1)and select **Download Config File** to download the kubeconfig file. This file will give you full access to your Cluster.

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

## Create Service Account and install VNGCloud LoadBalancer Controller <a href="#exposemotservicethongquavlblayer7-khoitaoserviceaccountvacaidatvngcloudingresscontroller" id="exposemotservicethongquavlblayer7-khoitaoserviceaccountvacaidatvngcloudingresscontroller"></a>

{% hint style="info" %}
**Attention:**

When you initialize the Cluster according to the instructions above, if you have not enabled the **Enable vLB Native Integration Driver** option , by default we will not pre-install this plugin into your Cluster. You need to manually create Service Account and install VNGCloud LoadBalancer Controller according to the instructions below. If you have enabled the **Enable vLB Native Integration Driver** option , then we have pre-installed this plugin into your Cluster, skip the Service Account Initialization step, install VNGCloud LoadBalancer Controller and continue following the instructions from Deploy once. Workload.
{% endhint %}

<details>

<summary>Create Service Account and install VNGCloud LoadBalancer Controller</summary>

**Initialize Service Account**

* Create or use a **service account** created on IAM and attach policy: **vLBFullAccess** , **vServerFullAccess** . To create a service account, go here [and](https://iam.console.vngcloud.vn/service-accounts) follow these steps:
  * Select " **Create a Service Account** ", enter a name for the Service Account and click **Next Step** to assign permissions to the Service Account
  * Find and select **Policy: vLBFullAccess and Policy: vServerFullAccess** , then click " **Create a Service Account** " to create Service Account, Policy: vLBFullAccess and Policy: vServerFullAccess created by VNG Cloud, you cannot delete these policies.
  * After successful creation, you need to save **the Client\_ID** and **Secret\_Key** of the Service Account to perform the next step.

**Install VNGCloud LoadBalancer Controller**

* Install Helm version 3.0 or higher. Refer to [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/) for instructions on how to install.
* Replace your K8S cluster's ClientID, Client Secret, and ClusterID information and continue running:

```
helm install vngcloud-load-balancer-controller oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/vngcloud-load-balancer-controller \
  --namespace kube-system \
  --set mysecret.global.clientID= __________________ \
  --set mysecret.global.clientSecret= __________________
```

* After the installation is complete, check the status of pods:

```
kubectl -n kube-system get pod -l app.kubernetes.io/name=vngcloud-load-balancer-controller
```

For example, in the image below you have successfully installed:

```
NAME                                                              READY   STATUS    RESTARTS   AGE
vngcloud-load-balancer-controller-1736217866-manager-77599vrxpz   1/1     Running   0          4h24m
```

</details>

***

## Deploy a Workload <a href="#exposemotservicethongquavlblayer7-deploymotworkload" id="exposemotservicethongquavlblayer7-deploymotworkload"></a>

The following is a guide for you to deploy the nginx service on Kubernetes.

### **Step 1** : **Create Deployment for Nginx app.**

* Create **nginx-service-lb7.yaml** file with the following content:

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
  type: NodePort 
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

* Deploy This deployment equals:

```
kubectl apply -f nginx-service-lb7.yaml
```

***

### **Step 2: Check the Deployment and Service information just deployed**

* Run the following command to test **Deployment**

```
kubectl get svc,deploy,pod -owide
```

* If the results are returned as below, it means you have deployed Deployment successfully.

```
NAME                    TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE     SELECTOR
service/kubernetes      ClusterIP   10.96.0.1      <none>        443/TCP        5h4m    <none>
service/nginx-service   NodePort    10.96.25.133   <none>        80:32572/TCP   2m50s   app=nginx

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
deployment.apps/nginx-app   1/1     1            1           2m50s   nginx        nginx:1.19.1   app=nginx

NAME                             READY   STATUS    RESTARTS   AGE     IP            NODE                                            NOMINATED NODE   READINESS GATES
pod/nginx-app-7f45b65946-6wlgw   1/1     Running   0          2m49s   172.16.54.3   ng-e0fc7245-0c6e-4336-abcc-31a70eeed71d-972a9   <none>           <none>
```

***

### **Create Ingress Resource** <a href="#tao-ingress-resource" id="tao-ingress-resource"></a>

* Create **nginx-ingress.yaml** file with the following content:

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress
spec:
  ingressClassName: "vngcloud"
  defaultBackend:
    service:
      name: nginx-service
      port:
        number: 80
  rules:
    - http:
        paths:
          - path: /path1
            pathType: Exact
            backend:
              service:
                name: nginx-service
                port:
                  number: 80               
```

* Run the following command to deploy Ingress

```
kubectl apply -f nginx-ingress.yaml
```

At this time, the vLB system will automatically create a LB corresponding to the Ingress resource above, for example:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FgLlYv2XB4ILWcMpCCcMV%252Fimage.png%3Falt%3Dmedia%26token%3Da554fc67-7a6d-4199-b007-72a50e777a60&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ef4760e7&#x26;sv=1" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* Currently Ingress only supports TLS port 443 and is the termination point for TLS (TLS termination). TLS Secret must contain fields with key names tls.crt and tls.key, which are the certificate and private key to use for TLS. If you want to use a Certificate for a host, please upload the Certificate according to the instructions at \[Upload a certificate] and use them as an annotation. For example:
{% endhint %}

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    # kubernetes.io/ingress.class: "vngcloud" # this annotation is deprecated will cause warning, can use option `ingressClassName` below instead.
    vks.vngcloud.vn/load-balancer-id: "lb-6cdea8fd-4589-410e-933f-c3bc46fa9d25"
    vks.vngcloud.vn/certificate-ids: "secret-a6d20ec6-f3e5-499a-981b-b1484e340cec"
spec:
  ingressClassName: "vngcloud"
  defaultBackend:
    service:
      name: apache-service
      port:
        number: 80
  tls:
    - hosts:
        - host.example.com
  rules:
    - host: host.example.com
      http:
        paths:
          - path: /path1
            pathType: Exact
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```

***

### **To access the nginx app, you can use the Load Balancer Endpoint that the system has created.**

```
http://Endpoint/
```

You can get Load Balancer Public Endpoint information at the vLB interface. Specifically, access at

For example, below I have successfully accessed the nginx app with the address: [http://180.93.181.129/](http://180.93.181.129/)

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FA0m2HnZCZDt45tSSBcU1%252Fimage.png%3Falt%3Dmedia%26token%3D8531eccd-bbe2-4ba3-a1f9-2e69e7258118&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=9e883d90&#x26;sv=1" alt=""><figcaption></figcaption></figure>

You can see more about ALB at [Working with Application Load Balancer (ALB](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/network/lam-viec-voi-application-load-balancer-alb) ).

{% hint style="info" %}
**Attention:**

* Changing the name or size (Rename, Resize) of the Load Balancer resource on vServer Portal can cause incompatibility with resources on the Kubernetes Cluster. This can lead to resources becoming inactive on the Cluster, or resources being resynchronized, or resource information between vServer Portal and the Cluster not matching. To prevent this problem, use `kubectl`Cluster resource management.
{% endhint %}
