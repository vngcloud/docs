# Fleet Management

## Overview <a href="#tong-quan" id="tong-quan"></a>

Fleet Management is a feature that helps group Kubernetes clusters across multiple **zones/regions** , allowing flexible traffic management between clusters. When using **Global Load Balancer (GLB)** , there are two main traffic distribution mechanisms:

1.  **North-South Traffic Management with GLB**

    * **How it works** : A single **GLB will route traffic to clusters** by geographic region (eg: HAN, HCM...), helping to optimize performance and reduce costs compared to using multiple individual Load Balancers.
    * **Support for clusters with Network Type:**&#x20;

    ✅ Calico Overlay ✅ Cilium Overlay ✅ Cilium VPC Native
2.  **East-West Traffic Management with GLB**

    * **How it works** : If a backend service in a cluster fails, traffic will **failover** to the backends of other clusters in **the fleet** , ensuring **no downtime** .
    * **Only supports clusters with Network Type** :&#x20;

    ✅ Cilium VPC Native

***

## Create fleet <a href="#tao-fleet" id="tao-fleet"></a>

Follow these instructions to create a Fleet and manage traffic distribution with GLB:

**Step 1:** Log in to **VKS Portal** at the link: [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Step 2:** Select **Fleet Management**

**Step 3:** Select **Create a fleet**

<figure><img src="../../.gitbook/assets/image (507).png" alt=""><figcaption></figcaption></figure>

**Step 4:** Enter a memorable name for the fleet in the **Fleet Name** field . The **Fleet** name must be between 5 and 50 characters long, including the characters a-z, 0-9, '-'

**Step 5:** Select **the Region** containing your **Cluster**

**Step 6:** Select the cluster list you want to add to the fleet and select **Register** .

**Step 7:** In the list of added **Clusters , you need to specify a cluster** as **host** . The remaining **Clusters will be members** . For example, in the picture, I specify the cluster named demo-fleet-03 as host and the cluster named demo-cluster-04 as member.

**Step 8:** Select the type of **Traffic flow** you want, depending on the **Network type** of the **cluster** you have selected, the type of **Traffic flow** you can choose will be displayed accordingly.

**Step 9:** Select **Create**

<figure><img src="../../.gitbook/assets/image (508).png" alt=""><figcaption></figcaption></figure>

**Step 10:** Deploy a service on the host cluster. First, you need to download **the KubeConfig** of **the Host Cluster** and connect to this host cluster. After downloading the **KubeConfig** file and updating it to a **config** file in the directory `~/.kube`, you can check the connection to the cluster with the command:

```
kubectl get nodes
```

Next, let's implement a service, which:

* With Traffic Flow: **East West Traffic Management with Multi Cluster Service** : you can create service type **LoadBalancer, NodePort or ClusterIP.**
* With Traffic Flow: **North South Traffic Management with GLB** : you can create service type **LoadBalance or NodePort** .

For example below, I create a file `nginx.yaml`containing nginx service type LoadBalancer at namespace `default`:

```yaml
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
        image: nginx:1.18.0
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

```
kubectl apply -f nginx.yaml
```

**Step 11:** Create a file `glb-nginx.yaml`containing the GLB service using the following sample YAML:

```yaml
apiVersion: vks.vngcloud.vn/v1alpha1
kind: VngcloudGlobalLoadBalancer
metadata:
  name: nginx-service
  namespace: default
```

**Step 12:** Apply GLB configuration using command:

```
kubectl apply -f glb-nginx.yaml
```

Replace `glb-nginx.yaml`with your YAML file name.

At this time, the system will create a new vGLB on the vGLB system, you can check the created vGLB [here](https://glb.console.vngcloud.vn/glb/list) .

<figure><img src="../../.gitbook/assets/image (509).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* A **vGLB** can only be used for **a single Fleet** .
* However, if you have a vGLB **that is not used in any Fleet** , you can **reuse** it by **adding annotations to the YAML file** when creating the vGLB.
{% endhint %}

**Step 13:** Check the status of GLB with the command:

```
kubectl get vngcloudgloballoadbalancer -n default
```

You will see a list of created GLBs along with their status.

For example:

```
NAME            FLEET ID                                  GLB ID                                     ADDRESS
                                                   AGE
nginx-service   fl-cadc9e8c-0930-44aa-a37f-cb330a8c4af9   glb-09108dcc-5d3d-4067-8700-02941acd7d68   vks-fl-cadc9e8-default-nginx-serv-33be0-53461-2354c.glb.vngcloud.vn   4h30m
```

**Step 14:** Get the IP address or hostname of GLB to access the service using the command:

<figure><img src="../../.gitbook/assets/image (510).png" alt=""><figcaption></figcaption></figure>

**Step 15:** Test Fleet's performance by sending a request to GLB:

```
curl http://<GLB_Endpoint>
```

Replace `<GLB_Endpoint>`with the IP address or hostname obtained from the step above.

For example:

```sh
curl http://vks-fl-25757a5-default-nginx-serv-33a00-53461-38e3a.glb.vngcloud.vn
StatusCode        : 200
StatusDescription : OK
Content           : <!DOCTYPE html>
                    <html>
                    <head>
                    <title>Welcome to nginx!</title>
                    <style>
                        body {
                            width: 35em;
                            margin: 0 auto;
                            font-family: Tahoma, Verdana, Arial, sans-serif;
                        }
                    </style>
                    <...
RawContent        : HTTP/1.1 200 OK
                    Connection: keep-alive
                    Accept-Ranges: bytes
                    Content-Length: 612
                    Content-Type: text/html
                    Date: Fri, 28 Feb 2025 08:48:50 GMT
                    ETag: "5e9efe7d-264"
                    Last-Modified: Tue, 21 Apr 2020 ...
Forms             : {}
Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 612], [Content-Type, text/html]...}
Images            : {}
InputFields       : {}
Links             : {@{innerHTML=nginx.org; innerText=nginx.org; outerHTML=<A href="http://nginx.org/">nginx.org</A>; outerText=nginx.org; tagName=A; href=http://nginx.org/}, @{innerHTML=nginx.com;    
                    innerText=nginx.com; outerHTML=<A href="http://nginx.com/">nginx.com</A>; outerText=nginx.com; tagName=A; href=http://nginx.com/}}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 612
```

Or access directly as picture:

<figure><img src="../../.gitbook/assets/image (511).png" alt=""><figcaption></figcaption></figure>

### **Check North-South Traffic with GLB** <a href="#kiem-tra-north-south-traffic-voi-glb" id="kiem-tra-north-south-traffic-voi-glb"></a>

Suppose, you have initialized Fleet with 2 clusters on 2 regions HAN, HCM and selected Flow Traffic as GLB. The general steps to perform the test are as follows:

1. First, on Host Cluster, you need to deploy glb-nginx.yaml to create GLB via command:

```
kubectl apply -f glb-nginx.yaml
```

1. Next, on each Cluster A, B, you create a deploy nginx service but you need to edit the service output to Hello Nginx HAN, Hello Nginx HCM to easily observe how traffic is distributed.

* **On Cluster A in Region HCM:**
  * Create files `nginx-configmap.yaml` and `nginx.yaml`following the pattern, deploy them on cluster A:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-custom-page
  namespace: default
data:
  index.html: |
    Hello Nginx HCM
```

```
kubectl apply -f nginx-configmap.yaml
```

```yaml
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
          image: nginx
          volumeMounts:
            - name: nginx-html
              mountPath: /usr/share/nginx/html/
      volumes:
        - name: nginx-html
          configMap:
            name: nginx-custom-page

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

```
kubectl apply -f nginx.yaml
```

* **On Cluster B in Region HAN:**
  * Create files `nginx-configmap.yaml` and `nginx.yaml`following the pattern, deploy them on cluster A:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-custom-page
  namespace: default
data:
  index.html: |
    Hello Nginx HAN
```

```
kubectl apply -f nginx-configmap.yaml
```

```yaml
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
          image: nginx
          volumeMounts:
            - name: nginx-html
              mountPath: /usr/share/nginx/html/
      volumes:
        - name: nginx-html
          configMap:
            name: nginx-custom-page

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

```
kubectl apply -f nginx.yaml
```

3. Finally, on ClusterA, B, do curl to GLB\_Domain.

* **On Cluster A in Region HCM:**

```
kubectl get pod   
NAME                           READY   STATUS    RESTARTS   AGE
nginx-app-5dc57d48b6-phtz4     1/1     Running   0          23m
```

```
kubectl exec nginx-app-5dc57d48b6-phtz4 -it -- curl vks-fl-c4289d0-default-nginx-serv-82e59-53461-93a04.glb.vngcloud.vn
```

The curl result will be as follows:

```
Hello Nginx HCM
```

* **On Cluster B in Region HAN:**

```
kubectl get pod
NAME                         READY   STATUS    RESTARTS   AGE
nginx-app-5dc57d48b6-tvc5f   1/1     Running   0          16h
```

Copy

```
kubectl exec nginx-app-5dc57d48b6-tvc5f -it -- curl vks-fl-c4289d0-default-nginx-serv-82e59-53461-93a04.glb.vngcloud.vn
```

The curl result will be as follows:

```
Hello Nginx HAN
```

### **Check** East-West Traffic with MCS <a href="#kiem-tra-east-west-traffic-voi-mcs" id="kiem-tra-east-west-traffic-voi-mcs"></a>

Test failover by shutting down the backend service in one cluster and observing how traffic is distributed to another cluster in Fleet:

* For example, on a Cluster belonging to Region HAN, I perform scale deployment with the command:

```
kubectl scale deployment nginx-app --replicas=0 -n default
```

* At this time, all traffic will be transferred to the cluster in Region HCM, you can check by curling to GLB Endpoint:

```
curl vks-fl-c4289d0-default-nginx-serv-82e59-53461-93a04.glb.vngcloud.vn
```

The curl result will be as follows:

```
Hello Nginx HCM
```

After completing the above steps, you have successfully set up Fleet Management on VKS with Global Load Balancer to effectively manage traffic between clusters.

***

## Register and unregister a cluster to the fleet <a href="#dang-ky-va-huy-dang-ky-mot-cluster-vao-fleet" id="dang-ky-va-huy-dang-ky-mot-cluster-vao-fleet"></a>

After creating a Fleet, you can add existing Kubernetes clusters to the Fleet in two ways:

* **Method 1:** In **Fleet Management** , select **Edit Fleet** then select a cluster from the available list and click **"Register"** to add to Fleet.

<figure><img src="../../.gitbook/assets/image (512).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (513).png" alt=""><figcaption></figcaption></figure>

* **Method 2:** Register the cluster directly to Fleet during the cluster creation process.

<figure><img src="../../.gitbook/assets/image (514).png" alt=""><figcaption></figcaption></figure>

If you no longer need a cluster in Fleet, you can **Unregister it** by:

**Step 1:** Access the **Fleet Management** section .

**Step 2:** Select the cluster to remove.

**Step 3:** Click **"Remove"** or **"Unregister"** (only delete cluster from Fleet, not delete cluster from VKS system).

<figure><img src="../../.gitbook/assets/image (515).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (516).png" alt=""><figcaption></figcaption></figure>

***

## Changing host clusters within a fleet <a href="#thay-doi-host-cluster-trong-mot-fleet" id="thay-doi-host-cluster-trong-mot-fleet"></a>

Once you create a Fleet, you can edit its configuration:

* **Change Host Cluster** in existing Fleet.
* **Add or remove cluster members** as needed, but always ensure Fleet has at least one cluster host.

<figure><img src="../../.gitbook/assets/image (518).png" alt=""><figcaption></figcaption></figure>

***

## Delete a fleet <a href="#xoa-mot-fleet" id="xoa-mot-fleet"></a>

When you no longer need a Fleet, you can delete it by:

**Step 1:** Access **Fleet Management** .

**Step 2:** Select **the Fleet** to delete.

**Step 3:** Click **"Delete"** and confirm.

<figure><img src="../../.gitbook/assets/image (519).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* Each Fleet needs to have at least **one host cluster** , the remaining clusters will act as **member clusters** . After the Fleet is created, you can **add/remove member clusters** or **change host clusters** .
* A cluster cannot register to **multiple Fleets at the same time** . If you want to change Fleet, you need **to Unregister from the old Fleet** before adding to the new Fleet.
* You cannot delete a cluster if it is a host cluster in a Fleet. If you want to delete a cluster that is **a host** , you need to **transfer the host role to another cluster** before deleting it. Without a host cluster, Fleet will not function properly.
* If you want to use Private cluster for Fleet, you **are required to set up NAT** to communicate with GLB because we currently do not support Private Service Endpoint to GLB.
* When a Fleet is deleted, **the clusters within the Fleet still exist** and can be used independently or added to another Fleet.
{% endhint %}
