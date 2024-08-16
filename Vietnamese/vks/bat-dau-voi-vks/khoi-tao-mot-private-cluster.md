# Khởi tạo một Private Cluster

Các private cluster không sử dụng địa chỉ External IP cho các node. Điều này có nghĩa là người dùng từ internet không thể trực tiếp kết nối với các node trong cluster. Private Cluster là lựa chọn lý tưởng cho các dịch vụ yêu cầu kiểm soát truy cập chặt chẽ, đảm bảo tuân thủ các quy định về bảo mật và quyền riêng tư dữ liệu.

### Model <a href="#khoitaomotpublicclustervoiprivatenodegroup-dieukiencan" id="khoitaomotpublicclustervoiprivatenodegroup-dieukiencan"></a>

<figure><img src="../../.gitbook/assets/image (691).png" alt=""><figcaption></figcaption></figure>

**Thành phần**        &#x20;

* **Control plane**: Được quản lý bởi VNG Cloud, chịu trách nhiệm điều phối và quản lý toàn bộ cluster.
* **Nodes**: Các Node trong Cluster khi được tạo ra sẽ chỉ có internal IP và không thể đi ra public internet. Nếu muốn node truy cập được internet, bạn cần sử dụng NAT Gateway. Chi tiết tham khảo thêm tại [đây](khoi-tao-mot-public-cluster-voi-private-node-group/pfsense-as-a-nat-gateway.md).
* **Private Load Balancer**: Được quản lý bởi VNG Cloud, giúp phân phối traffic truy cập từ VKS đến các dịch vụ khác trên VNG Cloud như IAM, vMonitor Platform, vServer, vStorage.
* **Private Service Endpoint**: Khi bạn tạo một private cluster, hệ thống tự động tạo 4 endpoints giúp kết nối với các dịch vụ khác trên VNG Cloud bao gồm:
  * **Endpoint** để kết nối tới dịch vụ **IAM** (Endpoint Name: vks-iam-endpoint-...)
  * **Endpoint** để kết nối tới dịch vụ **vMonitor Platform** (Endpoint Name: vks-vmonitor-endpoint-...)
  * **Endpoint** để kết nối tới dịch vụ **vServer** (Endpoint Name: vks-vserver-endpoint-...)
  * **Endpoint** để kết nối tới dịch vụ **vStorage** (Endpoint Name: vks-vstorage-endpoint-...)

{% hint style="info" %}
**Warning:**

* <mark style="color:red;background-color:red;">**Không xóa Service Endpoint**</mark>: Để đảm bảo hoạt động ổn định của cluster, bạn không nên xóa 4 service endpoint đã được tạo sẵn. Nếu vô tình xóa hoặc chỉnh sửa 4 endpoint này, trong vòng tối đa 5 phút, hệ thống sẽ tự động tạo lại nhưng có thể gây gián đoạn đến các dịch vụ đang chạy. Lúc này, do service endpoint tạo lại có thể đã thay đổi Endpoint IP so với ban đầu nên để cluster hoạt động được, bạn cần thực hiện thêm Endpoint IP một cách thủ công cho những server đang chạy trước đó.
* <mark style="color:red;background-color:red;">**Tái sử dụng Service Endpoint:**</mark> Các service endpoint có thể được nhiều private cluster cùng sử dụng. Khi các private cluster chung VPC thì chúng tôi sẽ tái sử dụng chúng cho các cluster này.&#x20;
* <mark style="color:red;background-color:red;">**Xóa Service Endpoint tự động:**</mark> Khi bạn xóa cluster, nếu không còn cluster nào tái sử dụng các service endpoint này, hệ thống sẽ tự động xóa chúng.
{% endhint %}

***

### Điều kiện cần <a href="#khoitaomotpublicclustervoiprivatenodegroup-dieukiencan" id="khoitaomotpublicclustervoiprivatenodegroup-dieukiencan"></a>

Để có thể khởi tạo một **Cluster** và **Deploy** một **Workload**, bạn cần:

* Có ít nhất 1 **VPC** và 1 **Subnet** đang ở trạng thái **ACTIVE**. Nếu bạn chưa có VPC, Subnet nào, vui lòng khởi tạo VPC, Subnet theo hướng dẫn tại [đây.](../../vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc.md)&#x20;
* Có ít nhất 1 **SSH** key đang ở trạng thái **ACTIVE**. Nếu bạn chưa có SSH key nào, vui lòng khởi tạo SSH key theo hướng dẫn tại [đây.](../../vserver/compute-hcm03-1a/security/ssh-key-bo-khoa.md)
* Đã cài đặt và cấu hình **kubectl** trên thiết bị của bạn. vui lòng tham khảo tại [đây](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) nếu bạn chưa rõ cách cài đặt và sử dụng kuberctl. Ngoài ra, bạn không nên sử dụng phiên bản kubectl quá cũ, chúng tôi khuyến cáo bạn nên sử dụng phiên bản kubectl sai lệch không quá một phiên bản với version của cluster.

***

### Khởi tạo Cluster <a href="#khoitaomotpublicclustervoiprivatenodegroup-khoitaocluster" id="khoitaomotpublicclustervoiprivatenodegroup-khoitaocluster"></a>

**Cluster trong Kubernetes** là một tập hợp gồm một hoặc nhiều máy ảo (VM) được kết nối lại với nhau để chạy các ứng dụng được đóng gói dạng container. Cluster cung cấp một môi trường thống nhất để triển khai, quản lý và vận hành các container trên quy mô lớn.

Để khởi tạo một Cluster, hãy làm theo các bước bên dưới:

**Bước 1:** Truy cập vào [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Bước 2:** Tại màn hình **Overview**, chọn **Activate.**

**Bước 3:** Chờ đợi tới khi chúng tôi khởi tạo thành công tài khoản VKS của bạn. Sau khi Activate thành công, bạn hãy chọn **Create a Cluster**

**Bước 4:** Tại màn hình khởi tạo Cluster, chúng tôi đã thiết lập thông tin cho Cluster và một **Default Node Group** cho bạn, bạn có thể giữ các giá trị mặc định này hoặc điều chỉnh các thông số mong muốn cho Cluster và Node Group của bạn tại Cluster Configuration, Default Node Group Configuration, Plugin. <mark style="color:red;">**Mặc định chúng tôi sẽ khởi tạo cho bạn một Public Cluster. Bạn cần thay đổi lựa chọn của bạn thành Private Cluster.**</mark>

**Bước 5:** Chọn **Create Kubernetes cluster.** Hãy chờ vài phút để chúng tôi khởi tạo Cluster của bạn, trạng thái của Cluster lúc này là **Creating**.

**Bước 6:** Khi trạng thái **Cluster** là **Active**, bạn có thể xem thông tin Cluster, thông tin Node Group bằng cách chọn vào Cluster Name tại cột **Name**.

***

### Kết nối và kiểm tra thông tin Cluster vừa tạo <a href="#khoitaomotpublicclustervoiprivatenodegroup-ketnoivakiemtrathongtinclustervuatao" id="khoitaomotpublicclustervoiprivatenodegroup-ketnoivakiemtrathongtinclustervuatao"></a>

Sau khi Cluster được khởi tạo thành công, bạn có thể thực hiện kết nối và kiểm tra thông tin Cluster vừa tạo theo các bước:&#x20;

**Bước 1:** Truy cập vào [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Bước 2:** Danh sách Cluster được hiển thị, chọn biểu tượng **Download** và chọn **Download config file** để thực hiện tải xuống file kubeconfig. File này sẽ giúp bạn có toàn quyền truy cập vào Cluster của bạn.

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

### Deploy một Workload <a href="#khoitaomotpublicclustervoiprivatenodegroup-deploymotworkload" id="khoitaomotpublicclustervoiprivatenodegroup-deploymotworkload"></a>

Sau đây là hướng dẫn để bạn deploy service nginx trên Kubernetes.

**Bước 1**: **Tạo Deployment cho Nginx app.**

*   Tạo file **nginx-service-lb4.yaml** với nội dung sau:

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
      type: LoadBalancer 
      ports:
        - protocol: TCP
          port: 80
          targetPort: 80
    ```

    * Deploy Deployment này bằng lệch:&#x20;

    ```
    kubectl apply -f nginx-service-lb4.yaml
    ```

    ***

    **Bước 2: Kiểm tra thông tin Deployment, Service trước khi expose ra Internet.**

    * Chạy câu lệnh sau đây để kiểm tra **Deployment**

    ```
    kubectl get svc,deploy,pod -owide
    ```

    * Nếu kết quả trả về như bên dưới tức là bạn đã deploy service nginx thành công.

    ```
    NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)           AGE     SELECTOR
    service/kubernetes      ClusterIP      10.96.0.1       <none>        443/TCP           2d4h    <none>
    service/nginx-app       NodePort       10.96.215.192   <none>        30080:31289/TCP   8m12s   app=nginx
    service/nginx-service   LoadBalancer   10.96.179.221   <pending>     80:32624/TCP      2m16s   app=nginx

    NAME                        READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
    deployment.apps/nginx-app   1/1     1            1           2m16s   nginx        nginx:1.19.1   app=nginx

    NAME                             READY   STATUS    RESTARTS   AGE     IP              NODE                                            NOMINATED NODE   READINESS GATES
    pod/nginx-app-7f45b65946-t7d7k   1/1     Running   0          2m16s   172.16.24.202   ng-3f06013a-f6a5-47ba-a51f-bc5e9c2b10a7-ecea1   <none>           <none
    ```

***

**Bước 3: Để truy cập vào app nginx vừa export, bạn có thể sử dụng URL với định dạng:**

```
http://Endpoint/
```

Bạn có thể lấy thông tin Public Endpoint của Load Balancer tại giao diện vLB. Cụ thể truy cập tại [https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb/](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb/detail/lb-927c0b5f-5bcf-4ee1-b645-41d6a0caeecb)

Ví dụ, bên dưới tôi đã truy cập thành công vào app nginx với địa chỉ : [http://180.93.181.20/](http://180.93.181.20/)
