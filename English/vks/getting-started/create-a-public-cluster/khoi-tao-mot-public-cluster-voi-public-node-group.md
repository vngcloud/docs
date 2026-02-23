# Create a Public Cluster with Public Node Group

## Prerequisites <a href="#khoitaomotpublicclustervoipublicnodegroup-dieukiencan" id="khoitaomotpublicclustervoipublicnodegroup-dieukiencan"></a>

To be able to initialize a **Cluster** and **Deploy** a **Workload** , you need:

* There is at least 1 **VPC** and 1 **Subnet in ACTIVE** state . If you do not have a VPC or Subnet yet, please create a VPC or Subnet according to the instructions here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc)
* There is at least 1 **SSH key in ACTIVE** state . If you do not have any SSH key, please create an SSH key according to the instructions here [.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vserver/compute-hcm03-1a/security/ssh-key-bo-khoa)
* Installed and configured **kubectl** on your device. Please refer here [if](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) you are not sure how to install and use kuberctl. In addition, you should not use a kubectl version that is too old, we recommend that you use a kubectl version that is no more than one version different from the cluster version.

***

## Initialize Cluster <a href="#khoitaomotpublicclustervoipublicnodegroup-khoitaocluster" id="khoitaomotpublicclustervoipublicnodegroup-khoitaocluster"></a>

**A cluster in Kubernetes** is a collection of one or more virtual machines (VMs) connected together to run containerized applications. Cluster provides a unified environment to deploy, manage, and operate containers at scale.

To initialize a Cluster, follow the steps below:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Step 2: At the Overview** screen , select **Activate.**

**Step 3:** Wait until we successfully create your VKS account. After Activate successfully, select **Create a Cluster**

**Step 4:** At the Cluster initialization screen, we have set up information for the Cluster and a **Default Node Group** for you. You can keep these default values ​​or adjust the desired parameters for the Cluster and Node Group at Cluster Configuration, Default Node Group Configuration, Plugin. **By default we will create a Public Cluster for you with Public Node Group.**

**Step 5:** Select **Create Kubernetes cluster.** Please wait a few minutes for us to initialize your Cluster, the Cluster's status is now **Creating** .

**Step 6: When the Cluster** status is **Active** , you can view Cluster information and Node Group information by selecting Cluster Name in the **Name** column .

***

## Connect and check the newly created Cluster information <a href="#khoitaomotpublicclustervoipublicnodegroup-ketnoivakiemtrathongtinclustervuatao" id="khoitaomotpublicclustervoipublicnodegroup-ketnoivakiemtrathongtinclustervuatao"></a>

After the Cluster is successfully initialized, you can connect and check the newly created Cluster information by following these steps:

**Step 1:** Visit [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** The Cluster list is displayed, select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73761995%2Fimage2024-4-4_14-37-11.png%3Fversion%3D1%26modificationDate%3D1712216232000%26api%3Dv2\&width=40\&dpr=4\&quality=100\&sign=7c12e1b3\&sv=1)and select **Download Config File** to download the kubeconfig file. This file will give you full access to your Cluster.

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

## Deploy a Workload <a href="#khoitaomotpublicclustervoipublicnodegroup-deploymotworkload" id="khoitaomotpublicclustervoipublicnodegroup-deploymotworkload"></a>

The following is a guide for you to deploy the nginx service on Kubernetes.

### **Step 1** : **Create Deployment and Service for Nginx app**

* Create **nginx-service.yaml** file with the following content:

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
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

* Deploy This deployment equals:

```
kubectl apply -f nginx-service.yaml
```

***

### **Step 2: Check Deployment and Service information before exposing it to the Internet.**

* Run the following command to test **Deployment**

```
kubectl get svc,deploy,pod -owide
```

* If the results are returned as below, it means you have successfully deployed the nginx service.

```
NAME                    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE    SELECTOR
service/kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP   2d4h   <none>
service/nginx-service   ClusterIP   10.96.178.229   <none>        80/TCP    74s    app=nginx

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
deployment.apps/nginx-app   1/1     1            1           74s   nginx        nginx:1.19.1   app=nginx

NAME                             READY   STATUS    RESTARTS   AGE   IP              NODE                                            NOMINATED NODE   READINESS GATES
pod/nginx-app-7f45b65946-5pcvz   1/1     Running   0          74s   172.16.24.201   ng-3f06013a-f6a5-47ba-a51f-bc5e9c2b10a7-ecea1   <none>           <none>
```

### **Step 3: Expose Nginx Service to the Internet** <a href="#expose-nginx-service-ra-internet" id="expose-nginx-service-ra-internet"></a>

* Run the following command to expose nginx-service to the internet:

```
kubectl expose deployment nginx-app --type=NodePort --port=30080 --target-port=80
```

* If the results are returned as below, it means you have successfully exposed the Service to the Internet.

```
NAME                    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)           AGE     SELECTOR
service/kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP           2d4h    <none>
service/nginx-app       NodePort    10.96.215.192   <none>        30080:31289/TCP   4s      app=nginx
service/nginx-service   ClusterIP   10.96.178.229   <none>        80/TCP            2m43s   app=nginx

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
deployment.apps/nginx-app   1/1     1            1           2m43s   nginx        nginx:1.19.1   app=nginx

NAME                             READY   STATUS    RESTARTS   AGE     IP              NODE                                            NOMINATED NODE   READINESS GATES
pod/nginx-app-7f45b65946-5pcvz   1/1     Running   0          2m43s   172.16.24.201   ng-3f06013a-f6a5-47ba-a51f-bc5e9c2b10a7-ecea1   <none>           <none
```

***

### **Step 4: To access the just exported Nginx app, you can use the URL with the format:**

```
http://<node_ip>:31289/
```

Where node\_ip can be the node\_port address of any node in the cluster. You can get Node's External IP information at the vServer interface. Specifically, access at [https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) .

For example, below I have successfully accessed the nginx app with the address: [http://61.28.231.65:31007/](http://61.28.231.65:31007/)

If you want to expose this service through vLB Layer4, vLB Layer7, please refer to:

* [Expose a service through vLB Layer4](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/bat-dau-voi-vks/expose-mot-service-thong-qua-vlb-layer4)
* [Expose a service through vLB Layer7](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/bat-dau-voi-vks/expose-mot-service-thong-qua-vlb-layer7)<br>
