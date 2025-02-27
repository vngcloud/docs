# Fleet Management

## Overview <a href="#tong-quan" id="tong-quan"></a>

Fleet Management is a feature that helps group Kubernetes clusters across multiple **zones/regions** , allowing flexible traffic management between clusters. When using **Global Load Balancer (GLB)** , there are two main traffic distribution mechanisms:

1. **North-South Traffic Management with GLB**
   * **How it works** : A single **GLB will route traffic to clusters** by geographic region (eg: HAN, HCM...), helping to optimize performance and reduce costs compared to using multiple individual Load Balancers.
   * **Support for clusters with Network Type:** ✅ Calico Overlay ✅ Cilium Overlay ✅ Cilium VPC Native
2. **East-West Traffic Management with GLB**
   * **How it works** : If a backend service in a cluster fails, traffic will **failover** to the backends of other clusters in **the fleet** , ensuring **no downtime** .
   * **Only supports clusters with Network Type** : ✅ Cilium VPC Native

***

## Create fleet <a href="#tao-fleet" id="tao-fleet"></a>

Follow these instructions to create a Fleet and manage traffic distribution with GLB:

**Step 1:** Log in to **VKS Portal** at the link: [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Step 2:** Select **Fleet Management**

**Step 3:** Select **Create a fleet**

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

**Step 4:** Enter a memorable name for the fleet in the **Fleet Name** field . The **Fleet** name must be between 5 and 50 characters long, including the characters a-z, 0-9, '-'

**Step 5:** Select **the Region** containing your **Cluster**

**Step 6:** Select the cluster list you want to add to the fleet and select **Register** .

**Step 7:** In the list of added **Clusters , you need to specify a cluster** as **host** . The remaining **Clusters will be members** . For example, in the picture, I specify the cluster named demo-fleet-03 as host and the cluster named demo-cluster-04 as member.

**Step 8:** Select the type of **Traffic flow** you want, depending on the **Network type** of the **cluster** you have selected, the type of **Traffic flow** you can choose will be displayed accordingly.

**Step 9:** Select **Create**

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**Step 10:** Deploy a service on the host cluster.

* With Traffic Flow: **East West Traffic Management with Multi Cluster Service** : you can create service type **LoadBalancer, NodePort or ClusterIP.**
* With Traffic Flow: **North South Traffic Management with GLB** : you can create service type **LoadBalance or NodePort** .

For example below, I create an nginx service of type LoadBalancer at namespace default:

```bash
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

**Step 11:** Create GLB service via the following sample YAML:

```bash
apiVersion: vks.vngcloud.vn/v1alpha1
kind: VngcloudGlobalLoadBalancer
metadata:
  name: nginx-service
  namespace: default
```

**Step 12:** Apply GLB configuration using command:

```bash
kubectl apply -f glb-nginx.yaml
```

Replace `glb-nginx.yaml`with your YAML file name.

**Step 13:** Check the status of GLB with the command:

```bash
kubectl get vngcloudgloballoadbalancer -n default
```

You will see a list of created GLBs along with their status.

For example:

```bash
NAME            FLEET ID                                  GLB ID                                     ADDRESS
                                                   AGE
nginx-service   fl-cadc9e8c-0930-44aa-a37f-cb330a8c4af9   glb-09108dcc-5d3d-4067-8700-02941acd7d68   vks-fl-cadc9e8-default-nginx-serv-33be0-53461-2354c.glb.vngcloud.vn   4h30m
```

**Step 14:** Get the IP address or hostname of GLB to access the service using the command:

```bash
kubectl get svc nginx-service -n default
```

You will see the External IP or hostname section, this is the address to access the service from outside.

For example:

```bash
NAME            TYPE           CLUSTER-IP     EXTERNAL-IP           PORT(S)        AGE
nginx-service   LoadBalancer   10.96.155.25   49.213.65.86.nip.io   80:30342/TCP   4h36m
```

**Step 15:** Test Fleet's performance by sending a request to GLB:

```bash
curl http://<EXTERNAL-IP>
```

Replace `<EXTERNAL-IP>`with the IP address or hostname obtained from the step above.

For example:

```bash
curl http://49.213.65.86.nip.io
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
                    Date: Thu, 27 Feb 2025 08:53:15 GMT
                    ETag: "5e9efe7d-264"
                    Last-Modified: Tue, 21 Apr 2020 ...
Forms             : {}
Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 612], [Content-Type,
                    text/html]...}
Images            : {}
InputFields       : {}
Links             : {@{innerHTML=nginx.org; innerText=nginx.org; outerHTML=<A href="http://nginx.org/">nginx.org</A>;
                    outerText=nginx.org; tagName=A; href=http://nginx.org/}, @{innerHTML=nginx.com;
                    innerText=nginx.com; outerHTML=<A href="http://nginx.com/">nginx.com</A>; outerText=nginx.com;
                    tagName=A; href=http://nginx.com/}}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 612
```

Or access directly as picture:

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

**Step 16:** Test failover by shutting down the backend service in one cluster and observing how traffic is distributed to another cluster in the Fleet:

**Test Traffic Flow MCS (East-West):**

```bash
kubectl scale deployment nginx-app --replicas=0 -n default
```

* Then, test GLB access again to confirm that traffic has been routed to the other cluster.
* Coming soon

**Test North-South Traffic with GLB:**

* Coming soon

After completing the above steps, you have successfully set up Fleet Management on VKS with Global Load Balancer to effectively manage traffic between clusters.

***

## Register and unregister a cluster to the fleet <a href="#dang-ky-va-huy-dang-ky-mot-cluster-vao-fleet" id="dang-ky-va-huy-dang-ky-mot-cluster-vao-fleet"></a>

After creating a Fleet, you can add existing Kubernetes clusters to the Fleet in two ways:

* **Method 1:** In **Fleet Management** , select **Edit Fleet** then select a cluster from the available list and click **"Register"** to add to Fleet.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

* **Method 2:** Register the cluster directly to Fleet during the cluster creation process.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

If you no longer need a cluster in Fleet, you can **Unregister it** by:

**Step 1:** Access the **Fleet Management** section .

**Step 2:** Select the cluster to remove.

**Step 3:** Click **"Remove"** or **"Unregister"** (only delete cluster from Fleet, not delete cluster from VKS system).

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

***

## Changing host clusters within a fleet <a href="#thay-doi-host-cluster-trong-mot-fleet" id="thay-doi-host-cluster-trong-mot-fleet"></a>

Once you create a Fleet, you can edit its configuration:

* **Change Host Cluster** in existing Fleet.
* **Add or remove cluster members** as needed, but always ensure Fleet has at least one cluster host.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

***

## Delete a fleet <a href="#xoa-mot-fleet" id="xoa-mot-fleet"></a>

When you no longer need a Fleet, you can delete it by:

**Step 1:** Access **Fleet Management** .

**Step 2:** Select **the Fleet** to delete.

**Step 3:** Click **"Delete"** and confirm.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Deleting a Fleet **does not delete the clusters within it** .

{% hint style="info" %}
**Attention:**

* Each Fleet needs to have at least **one host cluster** , the remaining clusters will act as **member clusters** . You can add or remove member clusters after the Fleet has been created.
* Each cluster can only belong to one Fleet at a time.
* A cluster cannot be deleted if it is a host cluster in a Fleet. The host role must be transferred to another cluster before deletion.
* If you want to use Private cluster for Fleet, you need to create NAT so that the clusters can connect to GLB because we currently do not support Private Endpoint to GLB.
* Deleting a Fleet does not delete the clusters within it.
{% endhint %}
