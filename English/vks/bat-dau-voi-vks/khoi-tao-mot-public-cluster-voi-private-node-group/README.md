# Create a Public Cluster with Private Node Group

## Prerequisites <a href="#khoitaomotpublicclustervoiprivatenodegroup-dieukiencan" id="khoitaomotpublicclustervoiprivatenodegroup-dieukiencan"></a>

To be able to initialize a **Cluster** and **Deploy** a **Workload** , you need:

* There is at least 1 **VPC** and 1 **Subnet in ACTIVE** state . If you do not have a VPC or Subnet yet, please create a VPC or Subnet according to the instructions here [.](../../../vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc.md)
* There is at least 1 **SSH key in ACTIVE** state . If you do not have any SSH key, please create an SSH key according to the instructions here [.](../../../vserver/compute-hcm03-1a/security/ssh-key-bo-khoa.md)
* Installed and configured **kubectl** on your device. Please refer here [if](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) you are not sure how to install and use kuberctl. In addition, you should not use a kubectl version that is too old, we recommend that you use a kubectl version that is no more than one version different from the cluster version.

**Attention:**

* **To ensure that VMs in NodeGroups on the subnet can go outbound to the internet and connect to the Control Plane, you must set up a NAT Gateway. For more details, please refer to the section below.**

***

## Create Palo Alto or Pfsense as an alternative to NAT Gateway <a href="#khoitaomotpublicclustervoiprivatenodegroup-khoitaopfsense" id="khoitaomotpublicclustervoiprivatenodegroup-khoitaopfsense"></a>

**Attention:**

* For the best support when using Palo Alto or Pfsense, please contact our team of experts via Hotline **1900 1549** or email **support@vngcloud.vn** .

Or you can choose to use Palo Alto or Pfsense to work with Private Node Group according to instructions at:

* [Palo Alto as a NAT Gateway](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vks/bat-dau-voi-vks/khoi-tao-mot-public-cluster-voi-private-node-group/palo-alto-as-a-nat-gateway)
* [Pfsense as a NAT Gateway](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vks/bat-dau-voi-vks/khoi-tao-mot-public-cluster-voi-private-node-group/pfsense-as-a-nat-gateway)

***

## Initialize Route Table <a href="#khoitaomotpublicclustervoiprivatenodegroup-khoitaoroutetable" id="khoitaomotpublicclustervoiprivatenodegroup-khoitaoroutetable"></a>

After Palo Alto, Pfsense is successfully initialized, you need to create a Route table to connect to different networks. Specifically, follow these steps to create a Route table:

**Step 1:** Visit [https://hcm-3.console.vngcloud.vn/vserver/network/route-table](https://hcm-3.console.vngcloud.vn/vserver/network/route-table)

**Step 2:** In the navigation menu bar, select **Network Tab/ Route table.**

**Step 3:** Select **Create Route table.**

**Step 4:** Enter a descriptive name for the Route table. Route table names can include letters (az, AZ, 0-9, '\_', '-'). The input data length is between 5 and 50. It must not include leading or trailing spaces.

**Step 5:** Select **VPC** for your Route table. If you do not have a VPC, you need to create a new VPC according to the instructions on [the VPC Page](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648039) . **The VPC used to set up the Route table must be the VPC selected for Palo Alto or Pfsense and your Cluster.**

**Step 6** : Select **Create** to create a new Route table.

**Step 7:** Select ![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762068%2Fimage2024-4-16\_15-40-3.png%3Fversion%3D1%26modificationDate%3D1713256805000%26api%3Dv2\&width=40\&dpr=4\&quality=100\&sign=7bf6e57b\&sv=1)the newly created Route table then select **Edit Routes.**

**Step 8:** In the add new **Route** section , enter the following information:

* For Destination, enter **Destination CIDR as 0.0.0.0/0**
* For Target, enter **Target CIDR as the corresponding Palo Alto or Pfsense Network Interface IP address.**

***

## Initialize Cluster <a href="#khoitaomotpublicclustervoiprivatenodegroup-khoitaocluster" id="khoitaomotpublicclustervoiprivatenodegroup-khoitaocluster"></a>

**A cluster in Kubernetes** is a collection of one or more virtual machines (VMs) connected together to run containerized applications. Cluster provides a unified environment to deploy, manage, and operate containers at scale.

To initialize a Cluster, follow the steps below:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select **Activate.**

**Step 3:** Wait until we successfully create your VKS account. After Activate successfully, select **Create a Cluster**

**Step 4:** At the Cluster initialization screen, we have set up information for the Cluster and a **Default Node Group** for you. You can keep these default values ​​or adjust the desired parameters for the Cluster and Node Group at Cluster Configuration, Default Node Group Configuration, Plugin. **By default we will create a Public Cluster for you with Public Node Group. You need to change your selection to Private Node Group .**

**Step 5:** Select **Create Kubernetes cluster.** Please wait a few minutes for us to initialize your Cluster, the Cluster's status is now **Creating** .

**Step 6: When the Cluster** status is **Active** , you can view Cluster information and Node Group information by selecting Cluster Name in the **Name** column .

***

## Connect and check the newly created Cluster information <a href="#khoitaomotpublicclustervoiprivatenodegroup-ketnoivakiemtrathongtinclustervuatao" id="khoitaomotpublicclustervoiprivatenodegroup-ketnoivakiemtrathongtinclustervuatao"></a>

After the Cluster is successfully initialized, you can connect and check the newly created Cluster information by following these steps:

**Step 1:** Visit [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** The Cluster list is displayed, select the icon![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762068%2Fimage2024-4-4\_14-37-11.png%3Fversion%3D1%26modificationDate%3D1712223012000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=57dcd547\&sv=1)and select **Download config file** to download the kubeconfig file. This file will give you full access to your Cluster.

**Step 3** : Rename this file to config and save it to the **\~/.kube/config directory**

**Step 4:** Perform Cluster check via command:

* Run the following command to test **node**

Copy

```
kubectl get nodes
```

* If the results are returned as below, it means your Cluster was successfully initialized with 3 nodes as below.

Copy

```
NAME                                            STATUS     ROLES    AGE   VERSION
ng-0e10592c-e70e-404d-a4e8-5e3b80f805e4-834b7   Ready      <none>   50m   v1.28.8
ng-0e10592c-e70e-404d-a4e8-5e3b80f805e4-cf652   Ready      <none>   23m   v1.28.8
ng-0f4ed631-1252-49f7-8dfc-386fa0b2d29b-a8ef0   Ready      <none>   28m   v1.28.8
```

***

## Deploy a Workload <a href="#khoitaomotpublicclustervoiprivatenodegroup-deploymotworkload" id="khoitaomotpublicclustervoiprivatenodegroup-deploymotworkload"></a>

The following is a guide for you to deploy the nginx service on Kubernetes.

**Step 1** : **Create Deployment for Nginx app.**

*   Create **nginx-service-lb4.yaml** file with the following content:

    Copy

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

    * Deploy This deployment equals:

    Copy

    ```
    kubectl apply -f nginx-service-lb4.yaml
    ```

    ***

    **Step 2: Check Deployment and Service information before exposing it to the Internet.**

    * Run the following command to test **Deployment**

    Copy

    ```
    kubectl get svc,deploy,pod -owide
    ```

    * If the results are returned as below, it means you have successfully deployed the nginx service.

    Copy

    ```
    NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)           AGE     SELECTOR
    service/kubernetes      ClusterIP      10.96.0.1       <none>        443/TCP           2d4h    <none>
    service/nginx-app       NodePort       10.96.215.192   <none>        30080:31289/TCP   8m12s   app=nginx
    service/nginx-service   LoadBalancer   10.96.179.221   <pending>     80:32624/TCP      2m16s   app=nginx

    NAME                        READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
    deployment.apps/nginx-app   1/1     1            1           2m16s   nginx        nginx:1.19.1   app=nginx

    NAME                             READY   STATUS    RESTARTS   AGE     IP              NODE                                            NOMINATED NODE   READINESS GATES
    pod/nginx-app-7f45b65946-t7d7k   1/1     Running   0          2m16s   172.16.24.202   ng-3f06013a-f6a5-47ba-a51f-bc5e9c2b10a7-ecea1   <none>           <none
    ```

***

**Step 3: To access the just exported nginx app, you can use the URL with the format:**

Copy

```
http://Endpoint/
```

You can get Load Balancer Public Endpoint information at the vLB interface. Specifically, access at [https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb/](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb/detail/lb-927c0b5f-5bcf-4ee1-b645-41d6a0caeecb)

For example, below I have successfully accessed the nginx app with the address: [http://180.93.181.20/](http://180.93.181.20/)
