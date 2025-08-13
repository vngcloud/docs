# Cài đặt và sử dụng NFS CSI Driver (cho Kubernetes)

## Điều kiên cần

* Kubernetes cluster version 1.21+
* Linux-based NFS server

## Cài đặt NFS CSI Driver

```bash
curl -skSL https://raw.githubusercontent.com/kubernetes-csi/csi-driver-nfs/v4.5.0/deploy/install-driver.sh | bash -s v4.5.0 --
```

* Sau khi cài đặt, kiểm tra trạng thái các pod:

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

## Tạo StorageClass

Tạo file `nfs-sc.yaml` với nội dung:

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs-csi
provisioner: nfs.csi.k8s.io
parameters:
  server: 10.7.9.5      # NFS server IP
  share: /demo-nfs      # NFS export path
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

Áp dụng và kiểm tra:

```bash
kubectl apply -f nfs-sc.yaml
kubectl get storageclasses
kubectl describe storageclass nfs-csi
```

## Tạo và sử dụng PVC

Tạo file `nfs-pvc.yaml`:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-nfs-dynamic
spec:
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 3Gi
  storageClassName: nfs-csi
```

Áp dụng và kiểm tra:

```bash
kubectl apply -f nfs-pvc.yaml
kubectl get pvc
kubectl describe pvc pvc-nfs-dynamic
```

## Deploy ứng dụng sử dụng PVC

Tạo file `nginx-deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-nfs
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
          claimName: pvc-nfs-dynamic

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

Áp dụng deployment:

```bash
kubectl apply -f nginx-deployment.yaml
```

### Advanced Options

1. **Retain Policy**:

```yaml
reclaimPolicy: Retain  # Giữ lại data khi PVC bị xóa
```

2. **Delayed Binding**:

```yaml
volumeBindingMode: WaitForFirstConsumer  # Chờ đến khi có Pod sử dụng mới provisioning
```

### Ghi chú quan trọng

* Xóa Pod không xóa PVC
* Với `reclaimPolicy: Delete`, xóa PVC sẽ xóa data trên NFS server
* Với `reclaimPolicy: Retain`, cần manual cleanup data sau khi xóa PVC
