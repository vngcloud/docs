# Ingress for an Application Load Balancer

In order for the Ingress resource (Ingress Yaml file) to work, the cluster must have a running VNGCloud LoadBalancer Controller. Unlike other Controller types that run as part of **kube-controller-manager** . VNGCloud LoadBalancer Controller is not automatically started with the cluster. Please follow the instructions below to install VNGCloud LoadBalancer Controller as well as work with Ingress Yaml files.

## Prepare <a href="#ingressforanapplicationloadbalancer-chuanbi" id="ingressforanapplicationloadbalancer-chuanbi"></a>

* Create a Kubernetes cluster on VNGCloud, or use an existing cluster. Note: make sure you have downloaded the cluster configuration file once the cluster has been successfully initialized and accessed your cluster.
* Create or use a **service account** created on IAM and attach policy: **vLBFullAccess** , **vServerFullAccess** . To create a service account, go here [and](https://iam.console.vngcloud.vn/service-accounts) follow these steps:
  * Select " **Create a Service Account** ", enter a name for the Service Account and click **Next Step** to assign permissions to the Service Account
  * Find and select **Policy: vLBFullAccess and Policy: vServerFullAccess** , then click " **Create a Service Account** " to create Service Account, Policy: vLBFullAccess and Policy: vServerFullAccess created by GreenNode, you cannot delete these policies.
  * After successful creation, you need to save **the Client\_ID** and **Secret\_Key** of the Service Account to perform the next step.
* Change **the Security Group** information to allow ALBs to connect to Nodes in your Node Group. You need to change them on vServer Portal when:
  * The Security Group attached to your **Cluster/Node Group is different from the default parameters** we created.
  * You need **to change the security level** for your Cluster or you need to **open more ports** for specific services to operate on the Cluster. Details information here [.](https://docs.vngcloud.vn/display/vServer/Security+Groups)

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
  * Find and select **Policy: vLBFullAccess and Policy: vServerFullAccess** , then click " **Create a Service Account** " to create Service Account, Policy: vLBFullAccess and Policy: vServerFullAccess created by GreenNode, you cannot delete these policies.
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

### **Step 3: Create Ingress Resource** <a href="#tao-ingress-resource" id="tao-ingress-resource"></a>

**1.If you do not have an Application Load Balancer previously created on the vLB system.**

Now, when creating an Ingress, leave the Load Balancer ID information blank at the [vks.vngcloud.vn/load-balancer-id](http://vks.vngcloud.vn/load-balancer-id) annotation .

* For example, suppose you have deployed a service named nginx-service. At this point, you can create the **nginx-ingress.yaml** file as follows:

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
          - path: /4
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

Once you have deployed Ingress, we will automatically create an ALB on your cluster. This ALB will be displayed on vLB Portal, details can be accessed here [.](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb) This ALB will have default information:

| **Ingredient** | **Quantity** | **Properties**                                                                                                  |
| -------------- | ------------ | --------------------------------------------------------------------------------------------------------------- |
| ALB Package    | first        | VNG ALB\_Small                                                                                                  |
| Listener       | 2            | <ul><li>1 listener with HTTP protocol and port 80</li><li>1 listener with HTTPS protocol and port 443</li></ul> |
| Pool           | first        | <ul><li>1 pool default HTTP protocol and ROUND ROBIN algorithm</li></ul>                                        |
| Health Check   | first        | <ul><li>Use TCP to check health of members.</li></ul>                                                           |

For example:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FgLlYv2XB4ILWcMpCCcMV%252Fimage.png%3Falt%3Dmedia%26token%3Da554fc67-7a6d-4199-b007-72a50e777a60&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ef4760e7&#x26;sv=1" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention**:

* Currently Ingress only supports TLS port 443 and is the termination point for TLS (TLS termination). TLS Secret must contain fields with key names tls.crt and tls.key, which are the certificate and private key to use for TLS. If you want to use a Certificate for a host, please upload the Certificate according to the instructions at \[Upload a certificate] and use them as an annotation. For example:
{% endhint %}

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    # kubernetes.io/ingress.class: "vngcloud" # this annotation is deprecated will cause warning, can use option `ingressClassName` below instead
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
          - path: /4
            pathType: Exact
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```

***

**2.If you already have a previously initialized Application Load Balancer on the vLB system and you want to reuse the ALB for your cluster.**

Now, when creating an Ingress, enter the Load Balancer ID information into the **vks.vngcloud.vn/load-balancer-id annotation.** For example, in this case I reused the ALB with ID = lb-2b9d8974-3760-4d60-8203-9671f229fb96:

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    # kubernetes.io/ingress.class: "vngcloud" # this annotation is deprecated will cause warning, can use option `ingressClassName` below instead.
    vks.vngcloud.vn/load-balancer-id: "lb-2b9d8974-3760-4d60-8203-9671f229fb96"
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
          - path: /4
            pathType: Exact
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```

* After you have created ingress according to the instructions at [Ingress for an Application Load Balancer](https://docs.vngcloud.vn/display/VKSVI/Ingress+for+an+Application+Load+Balancer) . If:
  * Your ALB currently has 2 listeners in it:
    * 1 listener has HTTP protocol configuration and port 80
    * If a listener has HTTPS protocol configuration and port 443, we will use these 2 listeners.
  * Your ALB does not have either or both listeners with the above configuration, we will automatically create them.

{% hint style="info" %}
**Attention**:

If your ALB has:

* 1 listener has HTTP protocol configuration and port 443
* Or a listener configured with HTTPS protocol and portal 80

then when creating Ingress an error will occur. At this point, you need to edit valid listener information on the vLB system and recreate ingress.
{% endhint %}

***

**3. After successfully creating ingress with an ALB , you are good to go**

* Edit your ingress configuration according to the specific instructions at [Configure for an Application Load Balancer](https://docs.vngcloud.vn/display/VKSVI/Configure+for+an+Application+Load+Balancer) .
* Or you can add/edit/delete policies in your ALB by editing the following parameters in the ingress resource (Ingress Yaml file). For example, below, I have set up **2 rules** as follows:

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress
  annotations:
    vks.vngcloud.vn/certificate-ids: "secret-58542bfb-f410-4095-9e1c-34cd39995c6d, secret-893b67e2-0286-434d-9e11-a8af997aefb8"
spec:
  ingressClassName: "vngcloud"
  defaultBackend:
    service:
      name: nginx-service
      port:
        number: 80
  tls:
    - hosts:
       - '*.example.com'
       - 'example.com'
  rules:
    - host: example.com
      http:
        paths:
          - path: /1
            pathType: Exact
            backend:
              service:
                name: nginx-service1
                port:
                  number: 80
    - http:
        paths:
          - path: /2
            pathType: Exact
            backend:
              service:
                name: nginx-service2
                port:
                  number: 80
```

* Like other Kubernetes resources, Ingress has a structure including the following information fields:
  * **apiVersion:** API version for Ingress.
  * **kind:** Resource type, in this case "Ingress".
  * **ingressClassName** : you need to specify this field value as "vngcloud" to use vngcloud-ingress-controller.
  * **metadata:** Information describing Ingress, including name, annotations.
  * **spec:** Ingress configuration, including traffic route rules according to the conditions of incoming requests. Ingress resources only support rules to direct HTTP traffic.

For general information about working with Ingress resources (Ingress Yaml files), see \[Configure for an Application Load Balancer]).

***

### Step 4: Check and edit the created Ingress resource <a href="#ingressforanapplicationloadbalancer-trienkhaiingress" id="ingressforanapplicationloadbalancer-trienkhaiingress"></a>

* After successfully creating ingress, you can view the ingress list via command

```
kubectl get ingress
```

For example, below we have successfully created nginx-ingress:

```
NAME            CLASS      HOSTS   ADDRESS          PORTS   AGE
nginx-ingress   vngcloud   *       180.93.181.129   80      103m
```

* Or view details of an ingress by

```
kubectl describe ingress nginx-ingress
```

For example, below are the details of nginx-ingress that I created:

```
Name:             nginx-ingress
Labels:           <none>
Namespace:        default
Address:          180.93.181.129
Ingress Class:    vngcloud
Default backend:  nginx-service:80 (172.16.24.202:80)
Rules:
  Host        Path  Backends
  ----        ----  --------
  *
              /path1   nginx-service:80 (172.16.24.202:80)
Annotations:  vks.vngcloud.vn/load-balancer-id: lb-6cdea8fd-4589-410e-933f-c3bc46fa9d25
Events:       <none>
```

*   To update an existing nginx-ingress, we can do so by updating the Ingress Yaml file as follows:

    Copy

    ```
    kubectl edit ingress nginx-ingress
    ```

***

### **Step 5: To access the nginx app, you can use the Load Balancer Endpoint that the system has created.**

```
http://Endpoint/
```

You can get Load Balancer Public Endpoint information at the vLB interface. Specifically, access at

For example, below I have successfully accessed the nginx app with the address: [http://180.93.181.129/](http://180.93.181.129/)

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FA0m2HnZCZDt45tSSBcU1%252Fimage.png%3Falt%3Dmedia%26token%3D8531eccd-bbe2-4ba3-a1f9-2e69e7258118&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=9e883d90&#x26;sv=1" alt=""><figcaption></figcaption></figure>
