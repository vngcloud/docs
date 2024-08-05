# Preserve Source IP when using NLB and Nginx Ingress Controller

Preserve Source IP when using vLB Layer 4 and Nginx Ingress Controller in Kubernetes is the process of maintaining the original IP address of the client as traffic is forwarded through the load balancer and into the Kubernetes cluster. This is important in some cases where you need detailed information about the client connection, such as the original IP address and the original port of the client, to be able to make accurate traffic handling or logging decisions. Below is our specific guide to help you implement this usecase.

***

## Prerequisites <a href="#dieu-kien-can" id="dieu-kien-can"></a>

*   You have initialized the Cluster on the VKS system according to the instructions here [and ](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vks/bat-dau-voi-vks/expose-mot-service-thong-qua-vlb-layer4)**VNGCloud Controller Manager** has been installed on your cluster with appversion from **v0.2.1** or higher. If your appversion is lower than this standard version, you can perform the upgrade according to the following instructions:

    * First, you need to get the release name of **vngcloud-controller-manager** installed on your cluster:

    ```
    $ helm list -A | grep vngcloud-controller-manager

    vngcloud-controller-manager-1716448250          kube-system     10              2024-06-10 17:00:17.866548653 +0700 +07 deployed        vngcloud-controller-manager-0.2.3       v0.2.0
    ```

    * Then, please upgrade to the latest version via the command:

    ```
    helm upgrade vngcloud-controller-manager-1716448250 oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/vngcloud-controller-manager \
      --namespace kube-system
    ```
* Next, you need to install nginx-ingress-controller with the command:

```
helm install nginx-ingress-controller oci://ghcr.io/nginxinc/charts/nginx-ingress --namespace kube-system
```

***

## **ConfigMap for Nginx Ingress Controller** <a href="#cau-hinh-configmap-cho-nginx-ingress-controller" id="cau-hinh-configmap-cho-nginx-ingress-controller"></a>

* Add to Nginx Ingress Controller's ConfigMap the settings to enable proxy protocol via command:

```
kubectl edit cm -n kube-system nginx-ingress-controller
```

* The code you need to add is as follows:

```
data:
  proxy-protocol: "True"
  real-ip-header: proxy_protocol
  real-ip-recursive: "True"
  set-real-ip-from: 0.0.0.0/0
```

***

## Configure vLB Layer 4 <a href="#cau-hinh-vlb-layer-4" id="cau-hinh-vlb-layer-4"></a>

* Next, you need to configure vLB Layer4 to allow the use of proxy protocol for the Load Balancer Nginx service via the command:

Copy

```
kubectl annotate service -n kube-system nginx-ingress-controller-controller vks.vngcloud.vn/enable-proxy-protocol="http,https"
```

* Finally, please perform NLB testing on vLB Portal until these Load Balancers are ACTIVE with full listener and pool.

***

## Using <a href="#cach-su-dung" id="cach-su-dung"></a>

* Suppose, you have a service prometheus-node-exporter with port 9100 in the default namespace, you can apply the following yaml to make it accessible via NLB

Copy

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: default
spec:
  ingressClassName: nginx
  rules:
  - host: kkk.example.com
    http:
      paths:
      - backend:
          service:
            name: prometheus-node-exporter
            port:
              number: 9100
        path: /metrics
        pathType: Exact
```

* Then I use IP 103.245.252.75 to curl to host kkk.example.com as follows:
* The recorded log result has this Client IP information as shown:
