# Preserve Source IP when using NLB and Nginx Ingress Controller

Preserve Source IP when using vLB Layer 4 and Nginx Ingress Controller in Kubernetes is the process of maintaining the original IP address of the client as traffic is forwarded through the load balancer and into the Kubernetes cluster. This is important in some cases where you need detailed information about the client connection, such as the original IP address and the original port of the client, to be able to make accurate traffic handling or logging decisions. Below is our specific guide to help you implement this usecase.

***

### Điều kiện cần

*   Bạn đã thực hiện khởi tạo Cluster trên hệ thống VKS theo các hướng dẫn tại [đây ](expose-mot-service-thong-qua-vlb-layer4.md)và trên cụm của bạn đã được cài đặt **VNGCloud Controller Manager** với appversion từ **v0.2.1** trở lên. Nếu appversion của bạn thấp hơn version tiêu chuẩn này, bạn có thể thực hiện upgrade theo các hướng dẫn sau:

    * Đầu tiên, bạn cần lấy release name của **vngcloud-controller-manager** đã cài trên cụm của bạn:

    ```
    $ helm list -A | grep vngcloud-controller-manager

    vngcloud-controller-manager-1716448250          kube-system     10              2024-06-10 17:00:17.866548653 +0700 +07 deployed        vngcloud-controller-manager-0.2.3       v0.2.0
    ```

    * Sau đó, bạn hãy thực hiện upgrade lên version mới nhất thông qua lệnh:

    ```
    helm upgrade vngcloud-controller-manager-1716448250 oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/vngcloud-controller-manager \
      --namespace kube-system
    ```
* Tiếp theo, bạn cần thực hiện cài đặt nginx-ingress-controller theo lệnh:

```
helm install nginx-ingress-controller oci://ghcr.io/nginxinc/charts/nginx-ingress --namespace kube-system
```

***

### **Cấu hình ConfigMap cho Nginx Ingress Controller**

* Thêm vào ConfigMap của Nginx Ingress Controller các thiết lập để kích hoạt proxy protocol thông qua lệnh:

```
kubectl edit cm -n kube-system nginx-ingress-controller
```

* Đoạn mã bạn cần thêm như sau:

```
data:
  proxy-protocol: "True"
  real-ip-header: proxy_protocol
  real-ip-recursive: "True"
  set-real-ip-from: 0.0.0.0/0
```

***

### Cấu hình vLB Layer 4

* Tiếp theo, bạn cần cấu hình vLB Layer4 cho phép sử dụng proxy protocol cho service Load Balancer Nginx qua lệnh:

```
kubectl annotate service -n kube-system nginx-ingress-controller-controller vks.vngcloud.vn/enable-proxy-protocol="http,https"
```

* Cuối cùng, bạn hãy thực hiện kiểm tra NLB trên vLB Portal cho tới khi các Load Balancer này được ACTIVE với đầy đủ listener, pool.

***

### Cách sử dụng

* Giả sử, bạn có một service prometheus-node-exporter với port 9100 trong namespace default, bạn có thể apply yaml sau để có thể truy cập thông qua NLB

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

* Sau đó tôi sử dụng IP 103.245.252.75 để curl vào host kkk.example.com như sau:

<figure><img src="../../.gitbook/assets/image%20(383).png" alt=""><figcaption></figcaption></figure>

* Kết quả log ghi nhận được đã có thông tin Client IP này như hình:

<figure><img src="../../.gitbook/assets/image%20(384).png" alt=""><figcaption></figcaption></figure>
