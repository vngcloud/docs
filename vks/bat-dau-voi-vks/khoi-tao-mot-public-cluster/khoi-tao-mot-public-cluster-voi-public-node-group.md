# Khởi tạo một Public Cluster với Public Node Group

## 1. Điều kiện cần

Để có thể khởi tạo một **Cluster** và **Deploy** một **Workload**, bạn cần:

* Có ít nhất 1 **VPC** và 1 **Subnet** đang ở trạng thái **ACTIVE**. Nếu bạn chưa có VPC, Subnet nào, vui lòng khởi tạo VPC, Subnet theo hướng dẫn tại [đây.](broken-reference)&#x20;
* Có ít nhất 1 **SSH** key đang ở trạng thái **ACTIVE**. Nếu bạn chưa có SSH key nào, vui lòng khởi tạo SSH key theo hướng dẫn tại [đây.](broken-reference)
* Đã cài đặt và cấu hình **kubectl** trên thiết bị của bạn. vui lòng tham khảo tại [đây](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) nếu bạn chưa rõ cách cài đặt và sử dụng kuberctl. Ngoài ra, bạn không nên sử dụng phiên bản kubectl quá cũ, chúng tôi khuyến cáo bạn nên sử dụng phiên bản kubectl sai lệch không quá một phiên bản với version của cluster.

***

## 2. Khởi tạo Cluster

### 2.1. Định nghĩa về Cluster

**Cluster trong Kubernetes** là một tập hợp gồm một hoặc nhiều máy ảo (VM) được kết nối lại với nhau để chạy các ứng dụng được đóng gói dạng container. Cluster cung cấp một môi trường thống nhất để triển khai, quản lý và vận hành các container trên quy mô lớn.

### 2.2. Các bước khởi tạo Cluster

**Bước 1:** Truy cập vào [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Bước 2:** Tại màn hình **Overview**, chọn **Activate.**

**Bước 3:** Chờ đợi tới khi chúng tôi khởi tạo thành công tài khoản VKS của bạn. Sau khi Activate thành công, bạn hãy chọn **Create a Cluster**

**Bước 4:** Tại màn hình khởi tạo Cluster, chúng tôi đã thiết lập thông tin cho Cluster và một **Default Node Group** cho bạn, bạn có thể giữ các giá trị mặc định này hoặc điều chỉnh các thông số mong muốn cho Cluster và Node Group của bạn tại Cluster Configuration, Default Node Group Configuration, Plugin. **Mặc định chúng tôi sẽ khởi tạo cho bạn một Public Cluster với Public Node Group.**

**Bước 5:** Chọn **Create Kubernetes cluster.** Hãy chờ vài phút để chúng tôi khởi tạo Cluster của bạn, trạng thái của Cluster lúc này là **Creating**.

**Bước 6:** Khi trạng thái **Cluster** là **Active**, bạn có thể xem thông tin Cluster, thông tin Node Group bằng cách chọn vào Cluster Name tại cột **Name**.

***

## 3. Kết nối và kiểm tra thông tin Cluster

Sau khi Cluster được khởi tạo thành công, bạn có thể thực hiện kết nối và kiểm tra thông tin Cluster vừa tạo theo các bước:&#x20;

**Bước 1:** Truy cập vào [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Bước 2:** Danh sách Cluster được hiển thị, chọn biểu tượng **Action** và chọn **Download Config File** để thực hiện tải xuống file kubeconfig. File này sẽ giúp bạn có toàn quyền truy cập vào Cluster của bạn.

**Bước 3**: Đổi tên file này thành config và lưu nó vào thư mục **\~/.kube/config**

**Bước 4:** Thực hiện kiểm tra Cluster thông qua lệnh:&#x20;

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

## 4. Deploy một Workload

Dưới đây là hướng dẫn deploy **Nginx** trên Kubernetes.

### 4.1. Tạo Deployment và Service

#### Bước 1: Tạo file `nginx-service.yaml`

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

Triển khai bằng lệnh:

```
kubectl apply -f nginx-service.yaml
```

#### Bước 2: Kiểm tra trạng thái Deployment và Service

Chạy lệnh:

```
kubectl get svc,deploy,pod -owide
```

Nếu kết quả hiển thị thông tin **Deployment** và **Service**, tức là bạn đã deploy **nginx** thành công.

***

## 5. Expose Nginx Service ra Internet

Chạy lệnh sau để **expose** service ra internet:

```
kubectl expose deployment nginx-app --type=NodePort --port=30080 --target-port=80
```

Nếu kết quả hiển thị service với **NodePort**, tức là bạn đã expose thành công.

### 5.1. Truy cập ứng dụng

Truy cập ứng dụng theo địa chỉ:

```
http://<node_ip>:<node_port>/
```

* **node\_ip**: Địa chỉ **External IP** của bất kỳ **node** nào trong cluster.
* **node\_port**: Cổng được hiển thị trong danh sách service.

Bạn có thể lấy **External IP** của node tại giao diện **vServer**: [vServer Console](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server).

Ví dụ, nếu **node\_ip** là `61.28.231.65` và **node\_port** là `31007`, bạn có thể truy cập ứng dụng bằng đường dẫn:

```
http://61.28.231.65:31007/
```

Nếu bạn muốn expose service này thông qua **vLB Layer4** hoặc **vLB Layer7**, vui lòng tham khảo hướng dẫn:

* **Expose một service thông qua vLB Layer4**
* **Expose một service thông qua vLB Layer7**
