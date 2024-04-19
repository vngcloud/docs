# Integrate with Network Load Balancer

Để tích hợp một Network Load Balancer với một Kubernetes cluster, bạn có thể sử dụng một Service với type là [LoadBalancer](loadbalancerhttps://www.airplane.dev/blog/kubernetes-load-balancer). Khi bạn tạo một Service như vậy, VNGCloud Controller Manager sẽ tự động một NLB để chuyển tiếp lưu lượng đến các pod trên node của bạ[n](nhttps://www.airplane.dev/blog/kubernetes-load-balancer). Bạn cũng có thể sử dụng các annotation để tùy chỉnh các thuộc tính của Network Load Balancer, như port, protocol,...

### Chuẩn bị <a href="#integratewithnetworkloadbalancer-chuanbi" id="integratewithnetworkloadbalancer-chuanbi"></a>

* Tạo một Kubernetes cluster trên VNGCloud, hoặc sử dụng một cluster đã có. Lưu ý: đảm bảo bạn đã tải xuống cluster configuration file sau khi cluster được khởi tạo thành công và truy cập vào cluster của bạn.
* Khởi tạo hoặc sử dụng một **service account** đã tạo trên IAM và gắn policy: **vLBFullAccess**, **vServerFullAccess**. Để tạo service account bạn truy cập tại [đây](https://hcm-3.console.vngcloud.vn/iam/service-accounts) và thực hiện theo các bước sau:
  * Chọn "**Create a Service Account**", điền tên cho Service Account và nhấn **Next Step** để gắn quyền cho Service Account
  * Tìm và chọn **Policy:** **vLBFullAccess và Policy:** **vServerFullAccess**, sau đó nhấn "**Create a Service Account**" để tạo Service Account, Policy: vLBFullAccess vàPolicy: vServerFullAccess do VNG Cloud tạo ra, bạn không thể xóa các policy này.
  * Sau khi tạo thành công bạn cần phải lưu lại **Client\_ID** và **Secret\_Key** của Service Account để thực hiện bước tiếp theo.
* Gỡ cài đặt cloud-controller-manager&#x20;

```
kubectl get daemonset -n kube-system | grep -i "cloud-controller-manager"

# if your output is similar to the following, you MUST delete the old plugin
kubectl delete daemonset cloud-controller-manager -n kube-system --force
```

Ví dụ:&#x20;

![](https://docs-admin.vngcloud.vn/download/attachments/73760978/image2024-3-17\_21-42-44.png?version=1\&modificationDate=1710686565000\&api=v2)

* &#x20;Bên cạnh đó, bạn có thể xóa Service Account đang sử dụng cho cloud-controller-manager vừa gỡ

```
kubectl get sa -n kube-system | grep -i "cloud-controller-manager"

# if your output is similar to the above, you MUST delete this service account
kubectl delete sa cloud-controller-manager -n kube-system --force
```

***

### Cài đặt Helm <a href="#integratewithnetworkloadbalancer-caidathelm" id="integratewithnetworkloadbalancer-caidathelm"></a>

* Cài đặt Helm phiên bản từ 3.0 trở lên. Tham khảo tại [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/) để biết cách cài đặt.

***

### Cài đặt VNGCloud Controller Manager <a href="#integratewithnetworkloadbalancer-caidatvngcloudcontrollermanager" id="integratewithnetworkloadbalancer-caidatvngcloudcontrollermanager"></a>

* Đầu tiên, thêm repo này vào cluster của bạn qua lệnh:

```
helm repo add vks-helm-charts https://vngcloud.github.io/vks-helm-charts
helm repo update
```

* Thay thế thông tin ClientID, Client Secret và ClusterID của cụm K8S của bạn và tiếp tục chạy:

```
helm install  vngcloud-controller-manager vks-helm-charts/vngcloud-controller-manager --replace \
  --namespace kube-system \
  --set cloudConfig.global.clientID= <Lấy ClientID của Service Account được tạo trên IAM theo hướng dẫn bên trên> \
  --set cloudConfig.global.clientSecret= <Lấy ClientSecret của Service Account được tạo trên IAM theo hướng dẫn bên trên>\
  --set cluster.clusterID= <Lấy Cluster ID của cluster mà bạn đã khởi tạo trước đó>
```

* Sau khi việc cài đặt hoàn tất, thực hiện kiểm tra trạng thái của vngcloud-Integrate-controller pods:

```
kubectl get pods -n kube-system | grep vngcloud-controller-manager
```

Ví dụ như ảnh bên dưới là bạn đã cài đặt thành công vngcloud-controller-manager:

![](https://docs-admin.vngcloud.vn/download/attachments/73760978/image2024-3-17\_21-45-14.png?version=1\&modificationDate=1710686715000\&api=v2)

* Ngoài ra, chúng tôi sẽ có các bản cập nhật cho plugin này. Bạn có thể cập nhật chúng lên phiên bản mới nhất mà chúng tôi cung cấp bằng cách:

```
helm upgrade vngcloud-controller-manager vks-helm-charts/vngcloud-controller-manager -n kube-system
```

***

### Thiết lập tài nguyên <a href="#integratewithnetworkloadbalancer-thietlaptainguyen" id="integratewithnetworkloadbalancer-thietlaptainguyen"></a>

#### **1.Nếu bạn chưa có sẵn một Network Load Balancer** đã khởi tạo trước đó trên hệ thống vLB. <a href="#integratewithnetworkloadbalancer-1.neubanchuacosanmotnetworkloadbalancerdakhoitaotruocdotrenhethongv" id="integratewithnetworkloadbalancer-1.neubanchuacosanmotnetworkloadbalancerdakhoitaotruocdotrenhethongv"></a>

Lúc này, khi tạo một Ingress, bạn hãy để trống thông tin Load Balancer ID tại annotation [vks.vngcloud.vn/load-balancer-id](http://vks.vngcloud.vn/load-balancer-id).

* Ví dụ, dưới đây là tập tin YAML mẫu để triển khai Nginx với External LoadBalancer sử dụng vngcloud-controller-manager để tự động expose dịch vụ tới internet bằng bộ cân bằng tải L4:

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
spec:
  selector:
    app: nginx
  type: LoadBalancer
  ports:
  - name: http
    port: 80
    targetPort: 80
```

* Hoặc tập tin YAML mẫu để triển khai Máy chủ HTTP Apache trên Kubernetes với Internal LoadBalancer cho phép truy cập nội bộ trên cổng 8080:

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
    vks.vngcloud.vn/internal-load-balancer: "true"  # MUST set like this to create an internal loadbalancer
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

* Hoặc tập tin YAML mẫu để tạo Deployment và Service cho ứng dụng máy chủ UDP trong một cụm Kubernetes:

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

* Sau khi bạn đã thực hiện apply yaml file. Chúng tôi sẽ tự động tạo 1 NLB trên cluster của bạn. NLB này sẽ hiển thị trên vLB Portal, chi tiết truy cập tại [đây.](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb)&#x20;

Ví dụ

![](https://docs-admin.vngcloud.vn/download/attachments/73760978/image2024-3-17\_21-57-20.png?version=1\&modificationDate=1710687441000\&api=v2)

#### **2.Nếu bạn đã có sẵn một Network Load Balancer** đã khởi tạo trước đó trên hệ thống vLB và bạn muốn tái sử dụng NLB cho cluster của bạn. <a href="#integratewithnetworkloadbalancer-2.neubandacosanmotnetworkloadbalancerdakhoitaotruocdotrenhethongvlb" id="integratewithnetworkloadbalancer-2.neubandacosanmotnetworkloadbalancerdakhoitaotruocdotrenhethongvlb"></a>

Lúc này, bạn hãy nhập thông tin Load Balancer ID vào annotation [vks.vngcloud.vn/load-balancer-id](http://vks.vngcloud.vn/load-balancer-id).

* Ví dụ dưới đây là tập tin YAML mẫu để triển khai Nginx với External LoadBalancer sử dụng vngcloud-controller-manager để tự động expose dịch vụ tới internet bằng bộ cân bằng tải L4 sử dụng một NLB có sẵn với ID = lbp-ddbf9313-3f4c-471b-afd5-f6a3305159fc

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
    vks.vngcloud.vn/load-balancer-name: "my-nginx-service"                  # Name of the load balancer
    vks.vngcloud.vn/package-id: "lbp-ddbf9313-3f4c-471b-afd5-f6a3305159fc"  # ID of the load balancer package
spec:
  selector:
    app: nginx
  type: LoadBalancer
  ports:
  - name: http
    port: 80
    targetPort: 80
```

#### **3.Sau khi một NLB mới đã được chúng tôi tự động khởi tạo**, lúc này bạn có thể thực hiện <a href="#integratewithnetworkloadbalancer-3.saukhimotnlbmoidaduocchungtoitudongkhoitao-lucnaybancothethuchien" id="integratewithnetworkloadbalancer-3.saukhimotnlbmoidaduocchungtoitudongkhoitao-lucnaybancothethuchien"></a>

* Chỉnh sửa cấu hình NLB của bạn theo hướng dẫn cụ thể tại [Configure for a Network Load Balancer](https://docs.vngcloud.vn/display/VKSVI/Configure+for+a+Network+Load+Balancer). Ví dụ như bên dưới, tôi đã thực hiện chỉnh sửa protocol và port như sau:

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

* Cũng giống như các tài nguyên Kubernetes khác, **vngcloud-controller-manager** có cấu trúc gồm các trường thông tin như sau:
  * **apiVersion:** Phiên bản API cho Ingress.
  * **kind:** Loại tài nguyên, trong trường hợp này là "Service".
  * **metadata:** Thông tin mô tả Ingress, bao gồm tên, annotations.&#x20;
  * **spec:** Cấu hình điều kiện của các incoming request.

Để biết thông tin chung về cách làm việc với **vngcloud-controller-manager,**, hãy xem tại [Configure for a Network Load Balancer](https://docs-admin.vngcloud.vn/display/VKSVI/Configure+for+a+Network+Load+Balancer).

***

### Triển khai  <a href="#integratewithnetworkloadbalancer-trienkhai" id="integratewithnetworkloadbalancer-trienkhai"></a>

* Sau khi đã tạo tập tin yaml với nội dung theo mẫu, lưu tập tin với định dạng \<tên tập tin>.yaml
* Chạy lệnh bên dưới để apply tập tin cho cụm K8S:

```
kubectl apply -f <name>.yaml
```

Ví dụ như ảnh bên dưới là bạn đã apply thành công&#x20;

![](https://docs-admin.vngcloud.vn/download/attachments/73760978/image2024-3-17\_21-50-18.png?version=1\&modificationDate=1710687018000\&api=v2)

* Kiểm tra thông tin chi tiết cũng như địa chỉ External IP theo cú pháp

```
kubectl get pods,svc -owide
```

Ví dụ

![](https://docs-admin.vngcloud.vn/download/attachments/73760978/image2024-3-17\_22-3-45.png?version=1\&modificationDate=1710687825000\&api=v2)

* Cuối cùng, truy cập địa chỉ IP trên các port mà bạn đã thiết lập trên tập tin yaml và kiểm tra kết nối.
