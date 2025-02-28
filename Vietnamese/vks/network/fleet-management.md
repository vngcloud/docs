# Fleet Management

## Tổng quan

Fleet Management là tính năng giúp gom nhóm các Kubernetes cluster trên nhiều **zone/region**, cho phép quản lý traffic linh hoạt giữa các cluster. Khi sử dụng **Global Load Balancer (GLB)**, có hai cơ chế phân phối traffic chính:

1. **North-South Traffic Management với GLB**
   * **Cách hoạt động**: Một **GLB** duy nhất sẽ **route traffic đến các cụm cluster** theo vùng địa lý (VD: HAN, HCM...), giúp tối ưu hóa hiệu suất và giảm chi phí so với việc sử dụng nhiều Load Balancer riêng lẻ.
   * **Hỗ trợ cho cluster có Network Type:**\
     ✅ Calico Overlay\
     ✅ Cilium Overlay\
     ✅ Cilium VPC Native
2. **East-West Traffic Management với GLB**
   * **Cách hoạt động**: Nếu một backend service trong một cluster gặp sự cố, traffic sẽ **failover** sang backend của các cluster khác trong **fleet**, đảm bảo **không bị downtime**.
   * **Chỉ hỗ trợ cho cluster có Network Type**:\
     ✅ Cilium VPC Native

***

## Tạo fleet

Thực hiện theo hướng dẫn sau đây để tạo một Fleet và quản lý phân phối traffic với GLB:

**Bước 1:** Đăng nhập vào **VKS Portal** tại link: [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Bước 2:** Chọn mục **Fleet Management**

**Bước 3:** Chọn **Create a fleet**

<figure><img src="../../.gitbook/assets/image (932).png" alt=""><figcaption></figcaption></figure>

**Bước 4:** Nhập tên gợi nhớ cho fleet ở mục **Fleet Name**. Tên **Fleet** phải có độ dài từ 5 tới 50 ký tự, bao gồm các ký tự a-z, 0-9, '-'

**Bước 5:** Chọn **Region** chứa **Cluster** của bạn

**Bước 6:** Chọn danh sách cluster bạn muốn thêm vào fleet và chọn **Register**.&#x20;

**Bước 7:** Tại danh sách **Cluster** đã được thêm, bạn cần chỉ định một **cluster** làm **host**. Các **Cluster** còn lại sẽ là **member**. Ví dụ trong hình, tôi chỉ định cluster có tên demo-fleet-03 làm host và cluster có tên demo-cluster-04 làm member.

**Bước 8:** Chọn loại **Traffic flow** mà bạn mong muốn, tùy thuộc vào loại **Network type** của các **cluster** bạn đã chọn mà loại **Traffic flow** bạn có thể chọn sẽ hiển thị tương ứng.&#x20;

**Bước 9:** Chọn **Create**

<figure><img src="../../.gitbook/assets/image (933).png" alt=""><figcaption></figcaption></figure>

**Bước 10:** Thực hiện triển khai một service trên host cluster. Đầu tiên, bạn cần tải **KubeConfig** của **Host Cluster** về và thực hiện kết nối tới host cluster này. Sau khi tải xuống file **KubeConfig** và cập nhật thành file **config** trong thư mục `~/.kube`, bạn có thể kiểm tra kết nối tới cluster bằng lệnh:

```bash
kubectl get nodes
```

Tiếp theo, hãy thực hiện triển khai một service, trong đó:

* Với Traffic Flow: **East West Traffic Management with Multi Cluster Service**: bạn có thể tạo service type **LoadBalancer, NodePort hoặc ClusterIP.**
* Với Traffic Flow: **North South Trafic Management with GLB**: bạn có thể tạo service type **LoadBalance hoặc NodePort**.

Ví dụ bên dưới, tôi tạo một file `nginx.yaml` chứa service nginx loại LoadBalancer tại namespace `default`:

```yaml
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

```bash
kubectl apply -f nginx.yaml
```

**Bước 11:** Thực hiện tạo file `glb-nginx.yaml` chứa service GLB thông qua YAML mẫu sau:

```yaml
apiVersion: vks.vngcloud.vn/v1alpha1
kind: VngcloudGlobalLoadBalancer
metadata:
  name: nginx-service
  namespace: default
```

Lúc này, hệ thống sẽ tạo mới một vGLB trên hệ thống vGLB, bạn có thể kiểm tra vGLB được tạo tai [đây](https://glb.console.vngcloud.vn/glb/list).&#x20;

<figure><img src="../../.gitbook/assets/image (944).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Chú ý:**

* Một **vGLB** chỉ có thể được sử dụng cho **một Fleet duy nhất**.
* Tuy nhiên, nếu bạn có một vGLB **chưa được sử dụng trong bất kỳ Fleet nào**, bạn có thể **tái sử dụng** nó bằng cách **thêm annotation vào file YAML** khi tạo vGLB.
{% endhint %}

**Bước 12:** Áp dụng cấu hình GLB bằng lệnh:

```bash
kubectl apply -f glb-nginx.yaml
```

Thay `glb-nginx.yaml` bằng tên file YAML của bạn.

**Bước 13:** Kiểm tra trạng thái của GLB bằng lệnh:

```bash
kubectl get vngcloudgloballoadbalancer -n default
```

Bạn sẽ thấy danh sách các GLB đã tạo cùng với trạng thái của chúng.

Ví dụ:&#x20;

```bash
NAME            FLEET ID                                  GLB ID                                     ADDRESS
                                                   AGE
nginx-service   fl-cadc9e8c-0930-44aa-a37f-cb330a8c4af9   glb-09108dcc-5d3d-4067-8700-02941acd7d68   vks-fl-cadc9e8-default-nginx-serv-33be0-53461-2354c.glb.vngcloud.vn   4h30m
```

**Bước 14:** Lấy địa chỉ IP hoặc hostname của GLB để truy cập service bằng lệnh:

<figure><img src="../../.gitbook/assets/image (945).png" alt=""><figcaption></figcaption></figure>

**Bước 15:** Kiểm tra khả năng hoạt động của Fleet bằng cách gửi request đến GLB:

```sh
curl http://<GLB_Endpoint>
```

Thay `<GLB_Endpoint>` bằng địa chỉ IP hoặc hostname lấy được từ bước trên.

Ví dụ:&#x20;

```bash
curl http://vks-fl-25757a5-default-nginx-serv-33a00-53461-38e3a.glb.vngcloud.vn
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
                    Date: Fri, 28 Feb 2025 08:48:50 GMT
                    ETag: "5e9efe7d-264"
                    Last-Modified: Tue, 21 Apr 2020 ...
Forms             : {}
Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 612], [Content-Type, text/html]...}
Images            : {}
InputFields       : {}
Links             : {@{innerHTML=nginx.org; innerText=nginx.org; outerHTML=<A href="http://nginx.org/">nginx.org</A>; outerText=nginx.org; tagName=A; href=http://nginx.org/}, @{innerHTML=nginx.com;    
                    innerText=nginx.com; outerHTML=<A href="http://nginx.com/">nginx.com</A>; outerText=nginx.com; tagName=A; href=http://nginx.com/}}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 612
```

Hoặc truy cập trực tiếp như ảnh:&#x20;

<figure><img src="../../.gitbook/assets/image (946).png" alt=""><figcaption></figcaption></figure>

**Bước 16:** Thử nghiệm failover bằng cách tắt backend service trong một cluster và quan sát cách traffic được phân phối sang cluster khác trong Fleet:

**Test Traffic Flow MCS (East-West):**

```bash
kubectl scale deployment nginx-app --replicas=0 -n default
```

* Sau đó, kiểm tra truy cập lại GLB để xác nhận rằng traffic đã được chuyển đến cluster khác.
* Coming soon

**Test North-South Traffic với GLB:**

* Coming soon

Sau khi hoàn thành các bước trên, bạn đã thiết lập thành công Fleet Management trên VKS với Global Load Balancer để quản lý traffic giữa các cluster hiệu quả.

***

## Đăng ký và hủy đăng ký một cluster vào fleet

Sau khi tạo một Fleet, bạn có thể thêm các cluster Kubernetes hiện có vào Fleet qua 2 cách:

* **Cách 1:** Tại mục **Fleet Management**, chọn **Chỉnh sửa Fleet** sau đó chọn một cluster từ danh sách có sẵn và nhấn **"Register"** để thêm vào Fleet.

<figure><img src="../../.gitbook/assets/image (936).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (937).png" alt=""><figcaption></figcaption></figure>

* **Cách 2:** Đăng ký trực tiếp cluster vào Fleet ngay trong quá trình tạo cluster.

<figure><img src="../../.gitbook/assets/image (938).png" alt=""><figcaption></figcaption></figure>

Nếu không cần sử dụng một cluster trong Fleet nữa, bạn có thể **hủy đăng ký (Unregister)** bằng cách:

**Bước 1:** Truy cập vào phần **Fleet Management**.

**Bước 2:** Chọn cluster cần loại bỏ.

**Bước 3:** Nhấn **"Remove"** hoặc **"Unregister"** (chỉ xóa cluster khỏi Fleet, không xóa cluster khỏi hệ thống VKS).

<figure><img src="../../.gitbook/assets/image (939).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (940).png" alt=""><figcaption></figcaption></figure>

***

## Thay đổi host cluster trong một fleet

Sau khi tạo Fleet, bạn có thể chỉnh sửa cấu hình của nó:

* **Thay đổi Host Cluster** trong Fleet hiện có.
* **Thêm hoặc loại bỏ các member cluster** khi cần, nhưng luôn đảm bảo Fleet có ít nhất một host cluster.

<figure><img src="../../.gitbook/assets/image (941).png" alt=""><figcaption></figcaption></figure>

***

## Xóa một fleet

Khi không còn cần sử dụng Fleet, bạn có thể xóa nó bằng cách:

**Bước 1:** Truy cập vào **Fleet Management**.

**Bước 2:** Chọn **Fleet** cần xóa.

**Bước 3:** Nhấn **"Delete"** và xác nhận.

<figure><img src="../../.gitbook/assets/image (943).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Chú ý:**

* Mỗi Fleet cần có ít nhất **một host cluster**, các cluster còn lại sẽ đóng vai trò là **member cluster**. Sau khi Fleet được tạo, bạn có thể **thêm/bớt member cluster** hoặc **thay đổi host cluster**.
* Một cluster không thể đăng ký vào **nhiều Fleet cùng lúc**. Nếu muốn đổi Fleet, bạn cần **gỡ đăng ký (Unregister) khỏi Fleet cũ** trước khi thêm vào Fleet mới.
* Không thể xóa một cluster nếu nó đang là host cluster trong một Fleet. Nếu bạn muốn xóa một cluster đang là **host**, bạn cần **chuyển vai trò host sang cluster khác** trước khi xóa cluster đó. Nếu không có host cluster, Fleet sẽ không hoạt động đúng cách.
* Nếu bạn muốn sử dụng Private cluster cho Fleet, bạn **bắt buộc phải thiết lập NAT** để giao tiếp với GLB do hiện tại chúng tôi chưa hỗ trợ Private Service Endpoint tới GLB.
* Khi xóa một Fleet, **các cluster bên trong Fleet vẫn tồn tại** và có thể được sử dụng độc lập hoặc thêm vào Fleet khác.
{% endhint %}
