# Create a Public Cluster with Public Node Group

### Prerequisites  <a href="#khoitaomotpublicclustervoipublicnodegroup-dieukiencan" id="khoitaomotpublicclustervoipublicnodegroup-dieukiencan"></a>

To be able to initialize a Cluster and Deploy a Workload, you need:

* Have at least 1 VPC and 1 Subnet in ACTIVE state. If you do not have any VPC, Subnet, please initialize VPC, Subnet according to the instructions here.&#x20;
* Have at least 1 SSH key in ACTIVE state. If you do not have any SSH key, please initialize SSH key according to the instructions here.&#x20;
* Have installed and configured kubectl on your device. Please refer here if you do not know how to install and use kuberctl. In addition, you should not use a kubectl version that is too old, we recommend that you use a kubectl version that is no more than one version different from the cluster version.

***

### Create a Cluster <a href="#khoitaomotpublicclustervoipublicnodegroup-khoitaocluster" id="khoitaomotpublicclustervoipublicnodegroup-khoitaocluster"></a>

A cluster in Kubernetes is a collection of one or more virtual machines (VMs) connected together to run containerized applications. Clusters provide a unified environment for deploying, managing, and operating containers at scale.

To initialize a Cluster, follow the steps below:\
Step 1: Go to https://vks.console.vngcloud.vn/overview\
Step 2: On the Overview screen, select Activate.\
Step 3: Wait until we successfully initialize your VKS account. After successful Activation, select Create a Cluster\
Step 4: On the Cluster initialization screen, we have set up the information for the Cluster and a Default Node Group for you; you can keep these default values or adjust the desired parameters for your Cluster and Node Group in Cluster Configuration, Default Node Group Configuration, Plugin. By default, we will initialize a Public Cluster with a Public Node Group for you.\
Step 5: Select Create Kubernetes cluster. Please wait a few minutes for us to initialize your Cluster; the status of the Cluster at this time is Creating.\
Step 6: When the Cluster status is Active, you can view the Cluster information, Node Group information by clicking on the Cluster Name in the Name column.

***

### Connect to a Cluster <a href="#khoitaomotpublicclustervoipublicnodegroup-ketnoivakiemtrathongtinclustervuatao" id="khoitaomotpublicclustervoipublicnodegroup-ketnoivakiemtrathongtinclustervuatao"></a>

Sau khi Cluster được khởi tạo thành công, bạn có thể thực hiện kết nối và kiểm tra thông tin Cluster vừa tạo theo các bước:

**Bước 1:** Truy cập vào [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Bước 2:** Danh sách Cluster được hiển thị, chọn biểu tượng <img src="https://docs-admin.vngcloud.vn/download/thumbnails/73761995/image2024-4-4_14-37-11.png?version=1&#x26;modificationDate=1712216232000&#x26;api=v2" alt="" data-size="line"> và chọn **Download Config File** để thực hiện tải xuống file kubeconfig. File này sẽ giúp bạn có toàn quyền truy cập vào Cluster của bạn.

**Bước 3**: Đổi tên file này thành config và lưu nó vào thư mục **\~/.kube/config**

**Bước 4:** Thực hiện kiểm tra Cluster thông qua lệnh:

* Chạy câu lệnh sau đây để kiểm tra **node**

```
kubectl get nodes
```

* Nếu kết quả trả về như bên dưới tức là bạn Cluster của bạn được khởi tạo thành công với 3 node như bên dưới.

```
NAME                                            STATUS     ROLES    AGE   VERSION
ng-0e10592c-e70e-404d-a4e8-5e3b80f805e4-834b7   Ready      <none>   50m   v1.28.8
ng-0e10592c-e70e-404d-a4e8-5e3b80f805e4-cf652   Ready      <none>   23m   v1.28.8
ng-0f4ed631-1252-49f7-8dfc-386fa0b2d29b-a8ef0   Ready      <none>   28m   v1.28.8
```

***

### Deploy một Workload <a href="#khoitaomotpublicclustervoipublicnodegroup-deploymotworkload" id="khoitaomotpublicclustervoipublicnodegroup-deploymotworkload"></a>

Sau đây là hướng dẫn để bạn deploy service nginx trên Kubernetes.

**Bước 1**: **Tạo Deployment và Service cho Nginx app**

* Tạo file **nginx-service.yaml** với nội dung sau:

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
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

* Deploy Deployment này bằng lệch:

```
kubectl apply -f nginx-service.yaml
```

***

**Bước 2: Kiểm tra thông tin Deployment, Service trước khi expose ra Internet.**

* Chạy câu lệnh sau đây để kiểm tra **Deployment**

```
kubectl get svc,deploy,pod -owide
```

* Nếu kết quả trả về như bên dưới tức là bạn đã deploy service nginx thành công.

```
NAME                    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE    SELECTOR
service/kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP   2d4h   <none>
service/nginx-service   ClusterIP   10.96.178.229   <none>        80/TCP    74s    app=nginx

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
deployment.apps/nginx-app   1/1     1            1           74s   nginx        nginx:1.19.1   app=nginx

NAME                             READY   STATUS    RESTARTS   AGE   IP              NODE                                            NOMINATED NODE   READINESS GATES
pod/nginx-app-7f45b65946-5pcvz   1/1     Running   0          74s   172.16.24.201   ng-3f06013a-f6a5-47ba-a51f-bc5e9c2b10a7-ecea1   <none>           <none>
```

### **Expose Nginx Service ra Internet**

* Chạy câu lệnh sau đây để expose nginx-service ra internet:

```
kubectl expose deployment nginx-app --type=NodePort --port=30080 --target-port=80
```

* Nếu kết quả trả về như bên dưới tức là bạn đã expose Service ra Internet thành công.

```
NAME                    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)           AGE     SELECTOR
service/kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP           2d4h    <none>
service/nginx-app       NodePort    10.96.215.192   <none>        30080:31289/TCP   4s      app=nginx
service/nginx-service   ClusterIP   10.96.178.229   <none>        80/TCP            2m43s   app=nginx

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
deployment.apps/nginx-app   1/1     1            1           2m43s   nginx        nginx:1.19.1   app=nginx

NAME                             READY   STATUS    RESTARTS   AGE     IP              NODE                                            NOMINATED NODE   READINESS GATES
pod/nginx-app-7f45b65946-5pcvz   1/1     Running   0          2m43s   172.16.24.201   ng-3f06013a-f6a5-47ba-a51f-bc5e9c2b10a7-ecea1   <none>           <none
```

***

**Để truy cập vào app nginx vừa export, bạn có thể sử dụng URL với định dạng:**

```
http://<node_ip>:31289/
```

Trong đó node\_ip có thể là địa chỉ node\_port của bất kỳ node nào trong cluster. Bạn có thể lấy thông tin External IP của Node tại giao diện vServer. Cụ thể truy cập tại [https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server).

Ví dụ, bên dưới tôi đã truy cập thành công vào app nginx với địa chỉ : [http://61.28.231.65:31007/](http://61.28.231.65:31007/)

Nếu bạn muốn expose service này thông qua vLB Layer4, vLB Layer7, vui lòng tham khảo tại:

* [Expose một service thông qua vLB Layer4](expose-mot-service-thong-qua-vlb-layer4.md)
* [Expose một service thông qua vLB Layer7](expose-mot-service-thong-qua-vlb-layer7.md)
