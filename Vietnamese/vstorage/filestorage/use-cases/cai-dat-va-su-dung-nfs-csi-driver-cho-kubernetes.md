# Cài đặt và sử dụng NFS CSI Driver (cho Kubernetes)

## Điều kiên cần

* **Đã có Cluster với ít nhất 1 Node Group có 1 node trên VKS:**
  * Bạn phải khởi tạo thành công một cluster trên nền tảng VKS.
  * Kubernetes version của cluster phải từ 1.21 trở lên.
  * Cluster phải có ít nhất một Node Group đang hoạt động.&#x20;
  * _Nếu chưa có, bạn cần tham khảo và thực hiện theo tài liệu hướng dẫn tại_ [_đây_](../../../vks/bat-dau-voi-vks/khoi-tao-mot-public-cluster/)_._
* **Đã có File Storage (NFS):**
  * Bạn phải khởi tạo một File Storage theo giao thức NFS. Dịch vụ này có thể là Public File Storage hoặc Private File Storage.
  * Nếu bạn tạo Private File Storage thì file này phải được tạo trong cùng một VPC với VKS cluster của bạn để đảm bảo kết nối mạng. Chúng có thể nằm trong cùng hoặc khác subnet, miễn là trong cùng một VPC.
  * _Nếu chưa có, bạn cần tham khảo và thực hiện theo tài liệu hướng dẫn tại_ [_đây_](../cac-tinh-nang-cua-filestorage/khoi-tao-tai-nguyen/khoi-tao-file-storage-nfs.md)_._

***

## Cài đặt NFS CSI Driver

### **Bước 1: Kết nối đến Cluster**

* Đầu tiên, bạn cần tải file cấu hình: Trên giao diện VKS Portal, chọn **Download Config File** và tải về file `kubeconfig`. File này chứa thông tin xác thực để kết nối đến cluster.

<figure><img src="../../../.gitbook/assets/image (1118).png" alt=""><figcaption></figcaption></figure>

* Kiểm tra kết nối: Mở terminal cuar bạn và chạy lệnh sau để xác minh rằng bạn đã kết nối thành công đến cluster:

```
kubectl get nodes
```

* Ví dụ với Cluster bên dưới, tôi đã khởi tạo với 2 nodes:

```
# kubectl get nodes
NAME                                   STATUS   ROLES    AGE   VERSION
vks-demo-cluster-nodegroup-001-4ba81   Ready    <none>   6d    v1.29.13
vks-demo-cluster-nodegroup-001-bccb4   Ready    <none>   6d    v1.29.13
```

### Bước 2: Cài đặt NFS CSI Driver

* Chạy lệnh bên dưới để tải về và cài đặt NFS CSI Driver:

```bash
curl -skSL https://raw.githubusercontent.com/kubernetes-csi/csi-driver-nfs/v4.5.0/deploy/install-driver.sh | bash -s v4.5.0 --
```

* Sau khi cài đặt, kiểm tra trạng thái các pod qua lệnh:

```bash
kubectl -n kube-system get pod -o wide -l app=csi-nfs-controller
kubectl -n kube-system get pod -o wide -l app=csi-nfs-node
```

* Kết quả mong đợi:

```bash
csi-nfs-controller-6866b7dfbf-xfd56   4/4     Running
csi-nfs-node-dc4km                    3/3     Running
csi-nfs-node-dq5fd                    3/3     Running
```

Kết quả như này tức là NFS CSI đã cài đặt thành công và 3 pods cần thiết cho NFS CSI đã hoạt động.

***

## Tạo StorageClass

Storage Class (hay còn được gọi tắt là SC) là **một mẫu** để tạo ổ đĩa (PersistentVolume) tự động theo nhu cầu.

* Đầu tiên, bạn cần lấy thông tin mount của File Storage NFS: Trên giao diện File Storage Portal, chọn **Mount guide** và lưu các thông tin IP cũng như folder thực hiện mount.

<figure><img src="../../../.gitbook/assets/image (1119).png" alt=""><figcaption></figcaption></figure>

* Bây giờ, bạn hãy tạo Storage Class bằng cách tạo file `nfs-sc.yaml` với nội dung:

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs-csi       # Tên Storage Class
provisioner: nfs.csi.k8s.io
parameters:
  server: 10.7.9.5    # IP của filestorage (lấy từ thông tin mount guide trên File Storage Portal)
  share: /demo-nfs    # mountpoint (lấy từ thông tin mount guide trên File Storage Portal)
reclaimPolicy: Delete
volumeBindingMode: Immediate
mountOptions:
  - nfsvers=4
  - hard
  - timeo=600
  - retrans=3
  - rsize=1048576
  - wsize=1048576
  - resvport
  - async
```

* Tiếp theo, chạy câu lệnh sau đây để triển khai tạo storage class và kiểm tra thông tin:

```bash
kubectl apply -f nfs-sc.yaml
kubectl get storageclasses
kubectl describe storageclass nfs-csi
```

* Kết quả mong muốn:&#x20;

```bash
# kubectl apply -f nfs-sc.yaml
# kubectl get storageclasses
# kubectl describe storageclass nfs-csi
storageclass.storage.k8s.io/nfs-csi created
NAME                                  PROVISIONER          RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
nfs-csi                               nfs.csi.k8s.io       Delete          Immediate              false                  0s
vngcloud-nvme-5000-delete (default)   bs.csi.vngcloud.vn   Delete          WaitForFirstConsumer   true                   6d
vngcloud-ssd-3000-delete              bs.csi.vngcloud.vn   Delete          WaitForFirstConsumer   true                   6d
Name:            nfs-csi
IsDefaultClass:  No
Annotations:     kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"storage.k8s.io/v1","kind":"StorageClass","metadata":{"annotations":{},"name":"nfs-csi"},"mountOptions":["nfsvers=4","hard","timeo=600","retrans=3","rsize=1048576","wsize=1048576","resvport","async"],"parameters":{"server":"10.7.9.5","share":"/demo-nfs"},"provisioner":"nfs.csi.k8s.io","reclaimPolicy":"Delete","volumeBindingMode":"Immediate"}

Provisioner:           nfs.csi.k8s.io
Parameters:            server=10.7.9.5,share=/demo-nfs
AllowVolumeExpansion:  <unset>
MountOptions:
  nfsvers=4
  hard
  timeo=600
  retrans=3
  rsize=1048576
  wsize=1048576
  resvport
  async
ReclaimPolicy:      Delete
VolumeBindingMode:  Immediate
Events:             <none>
```

## Tạo và sử dụng PVC

PersistentVolumeClaim (hay còn gọi là PVC) là **yêu cầu người dùng gửi ra** để xin một ổ đĩa lưu trữ có kích thước cụ thể. Khi bạn tạo một PVC, Kubernetes sẽ dùng SC để tạo hoặc chọn một ổ đĩa phù hợp.

* Tạo file `nfs-pvc.yaml`với nội dung sau:    &#x20;

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  annotations:
    volume.beta.kubernetes.io/storage-provisioner: nfs.csi.k8s.io
    volume.kubernetes.io/storage-provisioner: nfs.csi.k8s.io
  name: pvc-nfs-dynamic        # Tên PVC
  namespace: default
spec:
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 3Gi            # Kích thước mong muốn cho PVC
  storageClassName: nfs-csi   # Tên Storage Class, tên này phải khớp với Storage Class Name đã tạo bên trên
  volumeMode: Filesystem
```

* Chạy câu lệnh sau đây để triển khai tạo pvc và kiểm tra việc cài đặt:

```bash
kubectl apply -f nfs-pvc.yaml
kubectl get pvc
kubectl describe pvc pvc-nfs-dynamic
```

* Kết quả mong muốn:&#x20;

```bash
# kubectl apply -f nfs-pvc.yaml
# kubectl get pvc
# kubectl describe pvc pvc-nfs-dynamic
persistentvolumeclaim/pvc-nfs-dynamic created
NAME              STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
pvc-nfs-dynamic   Pending                                      nfs-csi        <unset>                 0s
Name:          pvc-nfs-dynamic
Namespace:     default
StorageClass:  nfs-csi
Status:        Bound
Volume:        pvc-6ed4097b-d8fb-41c8-ba9c-7147a652ff83
Labels:        <none>
Annotations:   pv.kubernetes.io/bind-completed: yes
               pv.kubernetes.io/bound-by-controller: yes
               volume.beta.kubernetes.io/storage-provisioner: nfs.csi.k8s.io
               volume.kubernetes.io/storage-provisioner: nfs.csi.k8s.io
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:      3Gi
Access Modes:  RWX
VolumeMode:    Filesystem
Used By:       <none>
Events:
  Type    Reason                 Age   From                                                                                      Message
  ----    ------                 ----  ----                                                                                      -------
  Normal  ExternalProvisioning   0s    persistentvolume-controller                                                               Waiting for a volume to be created either by the external provisioner 'nfs.csi.k8s.io' or manually by the system administrator. If volume creation is delayed, please verify that the provisioner is running and correctly registered.
  Normal  Provisioning           0s    nfs.csi.k8s.io_vks-demo-cluster-nodegroup-001-4ba81_d071c067-6d99-4d90-87cf-01f89c32a2c4  External provisioner is provisioning volume for claim "default/pvc-nfs-dynamic"
  Normal  ProvisioningSucceeded  0s    nfs.csi.k8s.io_vks-demo-cluster-nodegroup-001-4ba81_d071c067-6d99-4d90-87cf-01f89c32a2c4  Successfully provisioned volume pvc-6ed4097b-d8fb-41c8-ba9c-7147a652ff83
```

## Deploy ứng dụng sử dụng PVC

Bên dưới là hướng dẫn tạo deployment nginx sử dụng PVC mà bạn vừa tạo bên trên:

* Tạo file `nginx-deployment.yaml`với nội dung sau:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-nfs                                  # Tên pod
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-nfs
  template:
    metadata:
      labels:
        app: nginx-nfs
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        volumeMounts:
        - name: nfs-storage    
          mountPath: /usr/share/nginx/html
      volumes:
      - name: nfs-storage
        persistentVolumeClaim:
          claimName: pvc-nfs-dynamic                # Tên PVC

---
apiVersion: v1
kind: Service
metadata:
  name: nginx-nfs-service
spec:
  selector:
    app: nginx-nfs
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

* Chạy câu lệnh sau đây để triển khai tạo service và deployment:

```bash
kubectl apply -f nginx-deployment.yaml
```

* Kết quả mong muốn:&#x20;

```bash
# kubectl apply -f nginx-deployment.yaml
deployment.apps/nginx-nfs created
service/nginx-nfs-service created
```

***

## Kiểm tra NFS File Storage sau khi triển khai

* Đầu tiên, bạn có thể kiểm tra PVC đã bound chưa qua lệnh:&#x20;

```bash
kubectl get pvc pvc-nfs-dynamic
```

* Kết quả mong đợi:

```bash
# kubectl get pvc pvc-nfs-dynamic
NAME              STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
pvc-nfs-dynamic   Bound    pvc-6ed4097b-d8fb-41c8-ba9c-7147a652ff83   3Gi        RWX            nfs-csi        <unset>                 109s
```

* Bây giờ, bạn có thể Deploy Pod test để ghi dữ liệu bằng cách tạo file `test-pod.yaml` theo mầu:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-nfs-writer
spec:
  containers:
  - name: busybox
    image: busybox
    command: ["/bin/sh", "-c", "while true; do echo $(date) >> /mnt/data/testfile; sleep 5; done"]
    volumeMounts:
    - name: nfs-storage
      mountPath: /mnt/data
  volumes:
  - name: nfs-storage
    persistentVolumeClaim:
      claimName: pvc-nfs-dynamic
```

* Chạy câu lệnh sau đây để triển khai tạo pod và kiểm tra:

```bash
kubectl apply -f test-pod.yaml
kubectl get pods -w
```

* Kết quả mong muốn:

<pre class="language-bash"><code class="lang-bash"># kubectl apply -f test-pod.yaml
<strong># kubectl get pods -w
</strong>pod/test-nfs-writer configured
NAME                         READY   STATUS    RESTARTS   AGE
nginx-nfs-6df57b7f6b-gptfj   1/1     Running   0          3m25s
nginx-nfs-6df57b7f6b-mbxx8   1/1     Running   0          3m25s
nginx-nfs-6df57b7f6b-sgcxh   1/1     Running   0          3m25s
nsenter-2fzs6c               1/1     Running   0          21h
test-nfs-writer              1/1     Running   0          2m3s
</code></pre>

* Bạn cũng có thể kiểm tra dữ liệu đã ghi qua lệnh:

```bash
kubectl exec -it test-nfs-writer -- ls -lh /mnt/data
kubectl exec -it test-nfs-writer -- du -sh /mnt/data
```

* Kết quả mong muốn:

<pre><code># kubectl exec -it test-nfs-writer -- ls -lh /mnt/data
<strong># kubectl exec -it test-nfs-writer -- du -sh /mnt/data
</strong>total 1K
-rw-r--r--    1 nobody   nobody       841 Aug 13 04:04 testfile
1.5K    /mnt/data
</code></pre>

* Và cuối cùng, bạn có thể kiểm tra usage của File storage thông qua portal.

***

### Advanced Options

Một số option nâng cao bạn có thể sử dụng khi tạo Storage Class:&#x20;

* **Retain Policy**:

```yaml
reclaimPolicy: Retain  # Giữ lại data khi PVC bị xóa
```

* **Delayed Binding**:

```yaml
volumeBindingMode: WaitForFirstConsumer  # Chờ đến khi có Pod sử dụng mới provisioning
```
