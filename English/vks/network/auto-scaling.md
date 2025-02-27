# Auto Scaling

## Overview <a href="#tong-quan" id="tong-quan"></a>

Auto Scaling allows vLB to automatically adjust the number of Slaves based on traffic, optimizing performance and costs. Auto Scaling helps you:

* **Optimize performance:** Ensure vLB always has enough resources to handle traffic, avoiding overload.
* **Cost savings:** Automatically reduce the number of LBs when traffic is low, or increase the number of LBs when traffic increases, helping you save and optimize costs in the best way.
* **Simplified management:** No need to manually monitor and scale vLBs.

## **Enable/Disable Auto Scaling** <a href="#bat-tat-auto-scaling" id="bat-tat-auto-scaling"></a>

* Auto Scaling **can only be enabled when initializing the vLB** and **cannot be disabled** afterwards. If you initialize the LoadBalancer via the vLB Portal, select the option: **Enable auto scaling** .

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

* If your LoadBalancer is automatically initialized through the VKS system, please add the annotation `vks.vngcloud.vn/enable-autoscale: true` when creating the LoadBalancer or Ingress service with the vngcloud Class. Updating this annotation after the LoadBalancer has been created will not have any effect. For example:

```bash
// For NLB
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
    vks.vngcloud.vn/enable-autoscale: true
spec:
  selector:
    app: nginx
  type: LoadBalancer
  ports:
  - name: http
    port: 80
    targetPort: 80
```

```bash
// For ALB
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    vks.vngcloud.vn/enable-autoscale: true
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

## **Auto Scaling Policy** <a href="#chinh-sach-auto-scaling" id="chinh-sach-auto-scaling"></a>

* Policy based on percentage of active connections compared to max connection limit.
  * **Scaling out:**
    * When reaching 80% active connection/max connection threshold for 3 consecutive minutes, the system will automatically add 1 LB member.
  * **Scaling in:**
    * When the threshold drops below 20% active connection/max connection for 3 consecutive minutes, the system will automatically delete 1 LB member.

{% hint style="info" %}
**Attention:**

* **Resize disabled:** For vLBs with Auto Scaling enabled, you cannot change the service plan (resize) manually.
* **Scaling Status:** During the process of scaling up or down the LB, the status of the LB will change from "Active" to "Scaling in/Scaling out". Once completed, the status will return to "Active".
* **Scaling Time:** The time to scale up or down a Slave role LB is about 5-10 minutes, from the time the connection exceeds the allowed threshold, depending on the number of listeners of that LB.
* **CNAME resolution** : For LBs with auto scale enabled, the system will automatically create a domain name for the LB cluster according to the template `lb_name-{userid}.{region}.vlb.vngcloud.vn`. After that, the user needs to proactively update the CNAME record to point the private domain name to the LB domain name. When there is a change in the number of slave LBs (scale up/down), the system will automatically update the DNS record corresponding to the LB domain name.
{% endhint %}

## **View Scaling History** <a href="#xem-lich-su-scaling" id="xem-lich-su-scaling"></a>

* Visit LB detail page.
* Select the "Scale History" tab to view the history of scaling up/down and the current number of LB members. The meaning of the information fields is explained as follows:
  * **Event type:** Scale in or Scale out action
  * **Adjustment number:** The number of member LBs that will change. For example, Adjustment number is 1, Event type is Scale out, then this Scale out action will scale 1 more member LB into the LB cluster.
  * **Total number:** Number of LBs after scaling
  * **Scale at:** Time to complete the scaling process.
