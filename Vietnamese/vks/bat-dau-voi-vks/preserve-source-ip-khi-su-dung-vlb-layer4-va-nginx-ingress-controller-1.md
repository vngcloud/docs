# Preserve Source IP khi sử dụng vLB Layer4 và Istio Ingress Gateway

**Preserve Source IP khi sử dụng vLB Layer 4 và Istio Ingress Gateway trong Kubernetes** là quá trình duy trì địa chỉ IP gốc của client khi lưu lượng được chuyển tiếp qua load balancer và đi vào cụm Kubernetes. Điều này rất quan trọng trong các trường hợp cần thông tin chi tiết về kết nối của client, như địa chỉ IP và cổng nguồn của client, để có thể thực hiện các quyết định xử lý lưu lượng hoặc ghi log chính xác. Dưới đây là hướng dẫn cụ thể để giúp bạn thực hiện trường hợp sử dụng này.

***

### Điều kiện cần

*   Bạn đã thực hiện khởi tạo Cluster trên hệ thống VKS theo các hướng dẫn tại [đây ](expose-mot-service-thong-qua-vlb-layer4.md)và trên cụm của bạn đã được cài đặt **VNGCloud Controller Manager** với appversion từ **v0.2.1** trở lên. Nếu appversion của bạn thấp hơn version tiêu chuẩn này, bạn có thể thực hiện upgrade theo các hướng dẫn sau:

    * Đầu tiên, bạn cần lấy release name của **vngcloud-controller-manager** đã cài trên cụm của bạn:

    ```bash
    $ helm list -A | grep vngcloud-controller-manager

    vngcloud-controller-manager-1716448250          kube-system     10              2024-06-10 17:00:17.866548653 +0700 +07 deployed        vngcloud-controller-manager-0.2.3       v0.2.0
    ```

    * Sau đó, bạn hãy thực hiện upgrade lên version mới nhất thông qua lệnh:

    ```bash
    helm upgrade vngcloud-controller-manager-1716448250 oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/vngcloud-controller-manager \
      --namespace kube-system
    ```
* Tiếp theo, bạn cần thực hiện cài đặt Istio Ingress Gateway theo lệnh:

```bash
helm repo add istio https://istio-release.storage.googleapis.com/charts
helm repo update

helm install istio-base istio/base -n istio-system --create-namespace --wait

kubectl get crd gateways.gateway.networking.k8s.io &> /dev/null || \
{ kubectl kustomize "github.com/kubernetes-sigs/gateway-api/config/crd?ref=v1.1.0" | kubectl apply -f -; }


helm install istiod istio/istiod --namespace istio-system --set profile=ambient
helm install istio-ingressgateway istio/gateway -n istio-system
```

***

### **Thiết lập môi trường**

* Đầu tiên, bạn cần đánh dấu namespace default với lable `istio-injection=enabled`

```bash
kubectl label namespace default istio-injection=enabled
```

* Tiếp theo, bạn có thể thực hiện tạo deployment.&#x20;

{% hint style="info" %}
**Chú ý:**&#x20;

* Bạn không nên sử dụng nginx pod bới vì có thể sẽ có lỗi xảy ra. Chi tiết tham khảo thêm tại [đây](https://medium.com/@syedhassaniiui/istio-common-issues-59340ae20241).
{% endhint %}

```bash
kubectl create deployment echo-server --image=mccutchen/go-httpbin
kubectl expose deployment echo-server --name=clusterip --port=80 --target-port=8080
```

* Sau đó, bạn có thể tạo một service theo lệnh:&#x20;

```bash
cat > config.yaml <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
  name: clusterip-gateway
spec:
  selector:
    istio: ingressgateway # Choose the appropriate selector for your environment
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
      - "clusterip.jimmysong.io" # Replace with the desired hostname
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: clusterip-virtualservice
spec:
  hosts:
  - "clusterip.jimmysong.io" # Replace with the same hostname as in the Gateway
  gateways:
  - clusterip-gateway # Use the name of the Gateway here
  http:
  - route:
      - destination:
          host: clusterip.default.svc.cluster.local # Replace with the actual hostname of your Service
          port:
            number: 80 # Port of the Service

EOF
```

```bash
kubectl apply -f config.yaml
```

* Sau khi triển khai service và deployment, bạn có thể mở 3 terminal để xem log chi tiết từ `istio-ingressgateway` và `echo-server` pod. Cụ thể:&#x20;

```bash
kubectl -n istio-system logs -l app=istio-ingressgateway -f
```

```
kubectl logs -l app=echo-server -f -c istio-proxy
```

```
kubectl logs -l app=echo-server -f
```

* Bạn cũng có thể mở một terminal để gửi request tới service qua lệnh:&#x20;

```bash
watch -n 1 "curl -H \"Host: clusterip.jimmysong.io\" ________________" # Replace with the IP of the Istio Ingress Gateway
```

Kết quả nhận được thông qua log: tất cả request tới đều có Source IP là IP Private của Load Balancer.

***



### Cấu hình vLB Layer 4

* Tiếp theo, bạn cần cấu hình vLB Layer4 cho phép sử dụng proxy protocol cho service Load Balancer Istio Gateway.&#x20;

```
kubectl annotate service -n istio-system istio-ingressgateway vks.vngcloud.vn/enable-proxy-protocol="*"
```

***

### Cấu hình Istio Gateway Pod

* Tiếp theo, bạn cần cấu hình Istio Gateway Pod nhận `proxy protocol`

```
kubectl patch deployment istio-ingressgateway -n istio-system -p '{"spec":{"template":{"metadata":{"annotations":{"proxy.istio.io/config":"{\"gatewayTopology\":{\"proxyProtocol\":{}}}"}}}}}'
```

Tiếp theo, bạn hãy đợi cho Pod mới running và kiểm tra lại log. Kết quả mong muốn: tất cả các request tới đều có Source IP là của Client (IP của Terminal send request ở bên trên).
