# Ingress for an Application Load Balancer

Để cho tài nguyên Ingress (Ingress Yaml file) có thể hoạt động được, cluster phải có 1 VNGCloud Ingress Controller đang chạy. Không giống các loại Controller khác được chạy như là 1 phần của **kube-controller-manager**. VNGCloud Ingress Controller không được tự động khởi động cùng với cluster. Hãy làm theo hướng dẫn sau đây để cài đặt VNGCloud Ingress Controller cũng như làm việc với Ingress Yaml file.

### Chuẩn bị <a href="#ingressforanapplicationloadbalancer-chuanbi" id="ingressforanapplicationloadbalancer-chuanbi"></a>

* Tạo một Kubernetes cluster trên VNGCloud, hoặc sử dụng một cluster đã có. Lưu ý: đảm bảo bạn đã tải xuống cluster configuration file sau khi cluster được khởi tạo thành công và truy cập vào cluster của bạn.
* Khởi tạo hoặc sử dụng một **service account** đã tạo trên IAM và gắn policy: **vLBFullAccess**, **vServerFullAccess**. Để tạo service account bạn truy cập tại [đây](https://hcm-3.console.vngcloud.vn/iam/service-accounts) và thực hiện theo các bước sau:
  * Chọn "**Create a Service Account**", điền tên cho Service Account và nhấn **Next Step** để gắn quyền cho Service Account
  * Tìm và chọn **Policy:** **vLBFullAccess và Policy:** **vServerFullAccess**, sau đó nhấn "**Create a Service Account**" để tạo Service Account, Policy: vLBFullAccess vàPolicy: vServerFullAccess do VNG Cloud tạo ra, bạn không thể xóa các policy này.
  * Sau khi tạo thành công bạn cần phải lưu lại **Client\_ID** và **Secret\_Key** của Service Account để thực hiện bước tiếp theo.
* Thay đổi thông tin **Security Group** để cho phép các ALB có thể kết nối được tới các Node trong Node Group của bạn. Bạn cần thay đổi chúng trên vServer Portal khi:
  * Security Group được gắn vào **Cluster/Node Group** của bạn **khác với thông số mặc định** mà chúng tôi đã tạo.
  * Bạn cần **thay đổi mức độ bảo mật** cho Cluster của mình hoặc bạn cần **mở thêm cổng** cho các dịch vụ cụ thể hoạt động trên Cluster. Chi tiết tham khảo tại [đây.](https://docs.vngcloud.vn/display/vServer/Security+Groups)

***

### Cài đặt Helm <a href="#ingressforanapplicationloadbalancer-caidathelm" id="ingressforanapplicationloadbalancer-caidathelm"></a>

* Cài đặt Helm phiên bản từ 3.0 trở lên. Tham khảo tại [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/) để biết cách cài đặt.

***

### Cài đặt VNGCloud Ingress Controller <a href="#ingressforanapplicationloadbalancer-caidatvngcloudingresscontroller" id="ingressforanapplicationloadbalancer-caidatvngcloudingresscontroller"></a>

* Đầu tiên, thêm repo này vào cluster của bạn qua lệnh:

```
helm repo add vks-helm-charts https://vngcloud.github.io/vks-helm-charts
helm repo update
```

* Thay thế thông tin ClientID, Client Secret và ClusterID của cluster của bạn và tiếp tục chạy:

```
helm install vngcloud-ingress-controller vks-helm-charts/vngcloud-ingress-controller \
  --set cloudConfig.global.clientID= <Lấy ClientID của Service Account được tạo trên IAM theo hướng dẫn bên trên> \
  --set cloudConfig.global.clientSecret= <Lấy ClientSecret của Service Account được tạo trên IAM theo hướng dẫn bên trên>\
  --set cloudConfig.clusterID= <Lấy Cluster ID của cluster mà bạn đã khởi tạo trước đó>
```

* Sau khi việc cài đặt hoàn tất, thực hiện kiểm tra trạng thái của vngcloud-ingress-controller pods:

```
kubectl get pods -n kube-system | grep vngcloud-ingress-controller
```

Ví dụ như ảnh bên dưới là bạn đã cài đặt thành công vngcloud-ingress-controller:

<figure><img src="https://docs-admin.vngcloud.vn/download/attachments/73760770/image2024-3-17_20-10-58.png?version=1&#x26;modificationDate=1710681058000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Bên cạnh đó, bạn cũng có thể xem logs của plugin này bằng lệnh:&#x20;

```
kubectl logs -n kube-system vngcloud-ingress-controller-0 -f
```

<figure><img src="https://docs-admin.vngcloud.vn/download/attachments/73760770/image2024-3-17_20-12-1.png?version=1&#x26;modificationDate=1710681122000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Ngoài ra, chúng tôi sẽ có các bản cập nhật cho plugin này. Bạn có thể cập nhật chúng lên phiên bản mới nhất mà chúng tôi cung cấp bằng cách:

```
helm upgrade vngcloud-ingress-controller vks-helm-charts/vngcloud-ingress-controller
```

***

### Deploy một Workload <a href="#ingressforanapplicationloadbalancer-deploymotworkload" id="ingressforanapplicationloadbalancer-deploymotworkload"></a>

Sau đây là hướng dẫn để bạn deploy service nginx trên Kubernetes.

**Bước 1**: **Tạo Deployment cho Nginx app.**

* Tạo file **nginx.yaml** với nội dung sau:

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
```

* Deploy Deployment này bằng lệch:&#x20;

```
kubectl apply -f nginx.yaml
```

***

**Bước 2: Tạo Service cho Nginx app**

* Tạo file **nginx-service.yaml** với nội dung sau:

```
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

* Deploy Service này bằng lệch:&#x20;

```
kubectl apply -f nginx-service.yaml
```

***

**Bước 3: Kiểm tra thông tin Deployment, Service vừa deploy**

* Chạy câu lệnh sau đây để kiểm tra **Deployment**

```
 kubectl get deploy -o wide
```

* Nếu kết quả trả về như bên dưới tức là bạn đã deploy Deployment thành công.

```
NAME        READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
nginx-app   1/1     1            1           44m   nginx        nginx:1.19.1   app=nginx
```

* Chạy câu lệnh sau đây để kiểm tra **Service**

```
kubectl get service
```

* Nếu kết quả trả về như bên dưới tức là bạn đã deploy Service thành công.

```
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP   18h
nginx-service   ClusterIP   10.96.101.160   <none>        80/TCP    2m7s
```

***

### Thiết lập tài nguyên Ingress( Ingress yaml file) <a href="#ingressforanapplicationloadbalancer-thietlaptainguyeningress-ingressyamlfile" id="ingressforanapplicationloadbalancer-thietlaptainguyeningress-ingressyamlfile"></a>

#### **1.Nếu bạn chưa có sẵn một Application Load Balancer nào** đã khởi tạo trước đó trên hệ thống vLB. <a href="#ingressforanapplicationloadbalancer-1.neubanchuacosanmotapplicationloadbalancernaodakhoitaotruocdotr" id="ingressforanapplicationloadbalancer-1.neubanchuacosanmotapplicationloadbalancernaodakhoitaotruocdotr"></a>

Lúc này, khi tạo một Ingress, bạn hãy để trống thông tin Load Balancer ID tại annotation [vks.vngcloud.vn/load-balancer-id](http://vks.vngcloud.vn/load-balancer-id).

* Ví dụ, giả sử bạn đã deployment một service có tên nginx-service. Lúc này, bạn có thể tạo file **nginx-ingress.yaml** như sau:
* Tạo file **nginx-ingress.yaml** với nội dung sau:

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

* Chạy câu lệnh sau đây để triển khai Ingress

```
kubectl apply -f nginx-ingress.yaml
```

Lúc này, hệ thống vLB sẽ tự động tạo một LB tương ứng với Ingress resource bên trên, ví dụ:&#x20;

<figure><img src="https://docs-admin.vngcloud.vn/download/attachments/73760770/image2024-4-15_14-17-42.png?version=1&#x26;modificationDate=1713262815000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Chú ý:

* Hiện tại Ingress chỉ hỗ trợ duy nhất TLS port 443 và là điểm kết thúc cho TLS (TLS termination). TLS Secret phải chứa các trường với tên key là tls.crt và tls.key, đây chính là certificate và private key để sử dụng cho TLS. Nếu bạn muốn sử dụng Certificate cho một host, hãy thực hiện tải lên Certificate theo hướng dẫn tại [Upload a certificate](https://docs-admin.vngcloud.vn/display/vServer/Upload+a+certificate) và sử dụng chúng như một annotation. Ví dụ:&#x20;

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    # kubernetes.io/ingress.class: "vngcloud" # this annotation is deprecated will cause warning, can use option `ingressClassName` below instead.
    vks.vngcloud.vn/load-balancer-id: "lb-6cdea8fd-4589-410e-933f-c3bc46fa9d25"
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
          - path: /nginx
            pathType: Exact
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```
{% endhint %}



* Sau khi bạn đã thực hiện triển khai Ingress theo hướng dẫn tại [Ingress for an Application Load Balancer](https://docs.vngcloud.vn/display/VKSVI/Ingress+for+an+Application+Load+Balancer). Chúng tôi sẽ tự động tạo 1 ALB trên cluster của bạn. ALB này sẽ hiển thị trên vLB Portal, chi tiết truy cập tại [đây.](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb) ALB này sẽ có thông tin mặc định:&#x20;

| Thành phần   | Số lượng | Thuộc tính                                                                                                  |
| ------------ | -------- | ----------------------------------------------------------------------------------------------------------- |
| ALB Package  | 1        | VNG ALB\_Small                                                                                              |
| Listener     | 2        | <ul><li>1 listener với protocol HTTP và port 80</li><li>1 listener với protocol HTTPS và port 443</li></ul> |
| Pool         | 1        | <ul><li>1 pool default protocol HTTP và algorithm ROUND ROBIN</li></ul>                                     |
| Health Check | 1        | <ul><li>Sử dụng TCP để health check các member.</li></ul>                                                   |

Ví dụ:&#x20;

<figure><img src="https://docs-admin.vngcloud.vn/download/attachments/73760770/image2024-3-17_21-4-44.png?version=1&#x26;modificationDate=1710684285000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### **2.Nếu bạn đã có sẵn một Application Load Balancer** đã khởi tạo trước đó trên hệ thống vLB và bạn muốn tái sử dụng ALB cho cluster của bạn. <a href="#ingressforanapplicationloadbalancer-2.neubandacosanmotapplicationloadbalancerdakhoitaotruocdotrenhet" id="ingressforanapplicationloadbalancer-2.neubandacosanmotapplicationloadbalancerdakhoitaotruocdotrenhet"></a>

Lúc này, khi tạo một Ingress, bạn hãy nhập thông tin Load Balancer ID vào annotation [vks.vngcloud.vn/load-balancer-id](http://vks.vngcloud.vn/load-balancer-id).

Ví dụ, trong trường hợp này tôi đã tái sử dụng ALB có ID = lb-2b9d8974-3760-4d60-8203-9671f229fb96:

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    # kubernetes.io/ingress.class: "vngcloud" # this annotation is deprecated will cause warning, can use option `ingressClassName` below instead.
    vks.vngcloud.vn/load-balancer-id: "lb-6cdea8fd-4589-410e-933f-c3bc46fa9d25"
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
          - path: /nginx
            pathType: Exact
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```

* Sau khi bạn đã thực hiện tạo ingress theo hướng dẫn tại [Ingress for an Application Load Balancer](https://docs.vngcloud.vn/display/VKSVI/Ingress+for+an+Application+Load+Balancer). Nếu:&#x20;
  * ALB của bạn đang có sẵn 2 listener trong đó:&#x20;
    * 1 listener có cấu hình protocol HTTP và port 80
    * 1 listener có cấu hình protocol HTTPS và port 443 thì chúng tôi sẽ sử dụng 2 listener này.
  * ALB của bạn chưa có một trong hai hoặc cả 2 listener có cấu hình trên, chúng tôi sẽ tự động khởi tạo chúng.

Chú ý:

Nếu ALB của bạn có:

* 1 listener có cấu hình protocol HTTP và port 443
* Hoặc 1 listener có cấu hình protocol HTTPS và portal 80

thì khi tạo Ingress sẽ xảy ra lỗi. Lúc này, bạn cần chỉnh sửa lại thông tin listener hợp lệ trên hệ thống vLB và thực hiện tạo lại ingress.

#### **3. Sau khi tạo ingress thành công với một ALB**, bạn có thể thực hiện <a href="#ingressforanapplicationloadbalancer-3.saukhitaoingressthanhcongvoimotalb-bancothethuchien" id="ingressforanapplicationloadbalancer-3.saukhitaoingressthanhcongvoimotalb-bancothethuchien"></a>

* Chỉnh sửa cấu hình ingress của bạn theo hướng dẫn cụ thể tại [Configure for an Application Load Balancer](https://docs.vngcloud.vn/display/VKSVI/Configure+for+an+Application+Load+Balancer).
* Hoặc bạn có thể thêm/ sửa/ xóa policy trong ALB của bạn bằng các chỉnh sửa các thông số sau trong tài nguyên ingress (Ingress Yaml file). Ví dụ như bên dưới, tôi đã thực hiện thiết lập **2 rule** như sau:

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    vks.vngcloud.vn/load-balancer-id: "lb-2b9d8974-3760-4d60-8203-9671f229fb96"
    vks.vngcloud.vn/package-id: ""
spec:
  ingressClassName: "vngcloud"
  defaultBackend:
    service:
      name: example-svc-1
      port:
        number: 8080
  tls:
    - hosts:
        - example.com
      secretName: secret-example-tls
  rules:
  - host: example.com
    http:
      paths:
        - path: /payment
          pathType: Exact
          backend:
            service:
              name: example-svc-payment
              port:
                number: 8000
        - path: /dashboard
          pathType: Exact
          backend:
            service:
              name: example-svc-dashboard
              port:
                number: 8001
  - host: myapp.com
    http:
      paths:
        - path: /
          pathType: Exact
          backend:
            service:
              name: default
              port:
                number: 8088
```

* Cũng giống như các tài nguyên Kubernetes khác, Ingress có cấu trúc gồm các trường thông tin như sau:
  * **apiVersion:** Phiên bản API cho Ingress.
  * **kind:** Loại tài nguyên, trong trường hợp này là "Ingress".
  * **ingressClassName**: bạn cần chỉ định giá trị field này là "vngcloud" để sử dụng vngcloud-ingress-controller.
  * **metadata:** Thông tin mô tả Ingress, bao gồm tên, annotations.&#x20;
  * **spec:** Cấu hình Ingress, bao gồm các rule route traffic theo điều kiện của các incoming request. Tài nguyên Ingress chỉ hỗ trợ các rule để điều hướng HTTP traffic.

Để biết thông tin chung về cách làm việc với tài nguyên Ingress (Ingress Yaml file), hãy xem tại [Configure for an Application Load Balancer](https://docs-admin.vngcloud.vn/display/VKSVI/Configure+for+an+Application+Load+Balancer).

***

### Triển khai Ingress <a href="#ingressforanapplicationloadbalancer-trienkhaiingress" id="ingressforanapplicationloadbalancer-trienkhaiingress"></a>

* Tạo Ingress trên với lệnh:

```
kubectl apply -f example-ingress.yaml
```

Ví dụ như ảnh bên dưới là bạn đã tạo thành công ingress

<figure><img src="https://docs-admin.vngcloud.vn/download/attachments/73760770/image2024-3-17_20-14-42.png?version=1&#x26;modificationDate=1710681283000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Sau khi tạo ingress thành công, bạn có thể xem danh sách ingress qua lệnh

```
kubectl get ingress
```

Ví dụ

<figure><img src="https://docs-admin.vngcloud.vn/download/attachments/73760770/image2024-3-17_20-15-56.png?version=1&#x26;modificationDate=1710681357000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Hoặc xem chi tiết một ingress bằng cách

```
kubectl describe ingress example-ingress
```

Ví dụ, bên dưới là thông tin chi tiết của example-ingress mà tôi đã tạo:

<figure><img src="https://docs-admin.vngcloud.vn/download/attachments/73760770/image2024-3-17_21-14-42.png?version=1&#x26;modificationDate=1710684883000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

### Cập nhật Ingress <a href="#ingressforanapplicationloadbalancer-capnhatingress" id="ingressforanapplicationloadbalancer-capnhatingress"></a>

* Để cập nhật 1 Ingress hiện có và thêm vào Host mới, ta có thể thực hiện bằng cách cập nhật Ingress Yaml file như sau:
  * Chỉnh sửa trực tiếp

```
kubectl edit ingress example-ingress
```

* &#x20;Hoặc chỉnh sửa trên trình soạn thảo riêng và replace lên cấu hình cũ

```
kubectl replace -f example-ingress
```
