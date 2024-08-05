# Integrate with Network Load Balancer

To integrate a Network Load Balancer with a Kubernetes cluster, you can use a Service with type [LoadBalancer](loadbalancerhttps://www.airplane.dev/blog/kubernetes-load-balancer) . When you create such a Service, VNGCloud Controller Manager will automatically create an NLB to forward traffic to pods on your [node](nhttps://www.airplane.dev/blog/kubernetes-load-balancer) . You can also use annotations to customize Network Load Balancer properties, such as port, protocol,...

#### Prepare <a href="#integratewithnetworkloadbalancer-chuanbi" id="integratewithnetworkloadbalancer-chuanbi"></a>

* Create a Kubernetes cluster on VNGCloud, or use an existing cluster. Note: make sure you have downloaded the cluster configuration file once the cluster has been successfully initialized and accessed your cluster.
* Create or use a **service account** created on IAM and attach policy: **vLBFullAccess** , **vServerFullAccess** . To create a service account, go here [and](https://hcm-3.console.vngcloud.vn/iam/service-accounts) follow these steps:
  * Select " **Create a Service Account** ", enter a name for the Service Account and click **Next Step** to assign permissions to the Service Account
  * Find and select **Policy: vLBFullAccess and Policy: vServerFullAccess** , then click " **Create a Service Account** " to create Service Account, Policy: vLBFullAccess and Policy: vServerFullAccess created by VNG Cloud, you cannot delete these policies.
  * After successful creation, you need to save **the Client\_ID** and **Secret\_Key** of the Service Account to perform the next step.

***

#### Create Service Account and install VNGCloud Controller Manager <a href="#exposemotservicethongquavlblayer4-khoitaoserviceaccountvacaidatvngcloudcontrollermanager" id="exposemotservicethongquavlblayer4-khoitaoserviceaccountvacaidatvngcloudcontrollermanager"></a>

Attention:

When you initialize the Cluster according to the instructions above, if you have not enabled the **Enable vLB Native Integration Driver** option , by default we will not pre-install this plugin into your Cluster. You need to manually create Service Account and install VNGCloud Controller Manager according to the instructions below. If you have enabled the **Enable vLB Native Integration Driver** option , then we have pre-installed this plugin into your Cluster, skip the Service Account Initialization step, install VNGCloud Controller Manager and continue following the instructions from Deploy once. Workload.

<details>

<summary>Instructions for creating Service Account and installing VNGCloud Controller Manager</summary>

*
  *
  *
  *
*

```
```

*

```
```

*
*

```
```

*

```
```

*

```
```

```
```

</details>

***

#### Deploy a Workload <a href="#exposemotservicethongquavlblayer4-deploymotworkload" id="exposemotservicethongquavlblayer4-deploymotworkload"></a>

**1.If you do not have a previously initialized Network Load Balancer available on the vLB system.**

At this point, you need to do:

**Step 1** : **Create Deployment, Service for Nginx app.**

* Create **nginx-service-lb4.yaml** file with the following content:

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

* Or use the following script file to deploy HTTP Apache Service with Internal LoadBalancer allowing internal access on port 8080:

Copy

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: internal-http-apache2-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: apache2
  template:
    metadata:
      labels:
        app: apache2
    spec:
      containers:
        - name: apache2
          image: httpd
          ports:
            - containerPort: 80
---

apiVersion: v1
kind: Service
metadata:
  name: internal-http-apache2-service
  annotations:
    vks.vngcloud.vn/scheme: "internal"              # MUST set like this to create an internal loadbalancer
spec:
  selector:
    app: apache2
  type: LoadBalancer                                # MUST set like this to create an internal loadbalancer
  ports:
    - name: http
      protocol: TCP
      port: 8080                                    # CAN be accessed via this port with other service in the same VPC
      targetPort: 80
```

* Or sample YAML file to create Deployment and Service for a UDP server application in a Kubernetes cluster:

Copy

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: udp-server-deployment
spec:
  selector:
    matchLabels:
      name: udp-server
  replicas: 5
  template:
    metadata:
      labels:
        name: udp-server
    spec:
      containers:
      - name: udp-server
        image: vcr.vngcloud.vn/udp-server
        imagePullPolicy: Always
        ports:
        - containerPort: 10001
          protocol: UDP
---

apiVersion: v1
kind: Service
metadata:
  name: udp-server-service
  annotations:
    vks.vngcloud.vn/pool-algorithm: "source-ip"
  labels:
    app: udp-server
spec:
  type: LoadBalancer
  sessionAffinity: ClientIP
  ports:
  - port: 10001
    protocol: UDP
  selector:
    name: udp-server
```

**2.If you already have a previously initialized Network Load Balancer on the vLB system and you want to reuse the NLB for your cluster.**

At this point, please enter the Load Balancer ID information into the **vks.vngcloud.vn/load-balancer-id annotation.** The example below is a sample YAML file to deploy Nginx with External LoadBalancer using vngcloud-controller-manager to automatically expose the service to the internet using an L4 load balancer using an available NLB with ID = lb-2b9d8974- 3760-4d60-8203-9671f229fb96

Copy

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: external-http-nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
---
kind: Service
apiVersion: v1
metadata:
  name: external-http-nginx-service
  annotations:
    vks.vngcloud.vn/package-id: "lbp-ddbf9313-3f4c-471b-afd5-f6a3305159fc"  # ID of the load balancer package
    vks.vngcloud.vn/load-balancer-id: "lb-2b9d8974-3760-4d60-8203-9671f229fb96"
spec:
  selector:
    app: nginx
  type: LoadBalancer
  ports:
  - name: http
    port: 80
    targetPort: 80
```

**3.Once a new NLB has been automatically created by us , you can now proceed**

* Edit your NLB configuration according to the specific instructions at [Configure for a Network Load Balancer](https://docs.vngcloud.vn/display/VKSVI/Configure+for+a+Network+Load+Balancer) . For example below, I have edited the protocol and port as follows:

Copy

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: http-apache2-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: apache2
  template:
    metadata:
      labels:
        app: apache2
    spec:
      containers:
        - name: apache2
          image: httpd
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: http-apache2-service
  annotations:
    vks.vngcloud.vn/load-balancer-id: "lb-f8c0d85b-cb0c-4c77-b382-37982c4d98af"
spec:
  selector:
    app: apache2
  type: LoadBalancer
  ports:
    - name: http
      protocol: TCP
      port: 8000
      targetPort: 80
```

* Like other Kubernetes resources, **vngcloud-controller-manager** has a structure including the following information fields:
  * **apiVersion:** API version for Ingress.
  * **kind:** Resource type, in this case "Service".
  * **metadata:** Information describing Ingress, including name, annotations.
  * **spec:** Configure the conditions of incoming requests.

For general information about working with **vngcloud-controller-manager,** see \[Configure for a Network Load Balancer]

* Deploy this Service using:

Copy

```
kubectl apply -f nginx-service-lb4.yaml
```

***

#### **Check Deployment and Service information just deployed** <a href="#kiem-tra-thong-tin-deployment-service-vua-deploy" id="kiem-tra-thong-tin-deployment-service-vua-deploy"></a>

* Run the following command to test **Deployment**

Copy

```
kubectl get svc,deploy,pod -owide
```

* If the results are returned as below, it means you have deployed Deployment successfully.

Copy

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

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FzD11c32iEIzE2hnbzbrv%252Fimage.png%3Falt%3Dmedia%26token%3D8010e3b8-fb5b-428a-9940-e7ff245895d2&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=58607080&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 3: To access the just exported nginx app, you can use the URL with the format:**

Copy

```
http://Endpoint/
```

You can get Load Balancer Public Endpoint information at the vLB interface. Specifically, access at [https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb/](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb/detail/lb-927c0b5f-5bcf-4ee1-b645-41d6a0caeecb)

For example, below I have successfully accessed the nginx app with the address: [http://180.93.181.20/](http://180.93.181.20/)

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FWRLfY9NlcRgvi7B2c3b7%252Fimage.png%3Falt%3Dmedia%26token%3D9aea9889-1f6f-478a-889e-8b936c2b3bb6&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b1f9d46b&#x26;sv=1" alt=""><figcaption></figcaption></figure>
