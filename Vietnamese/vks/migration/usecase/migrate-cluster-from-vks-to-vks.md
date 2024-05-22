# Migrate Cluster from VKS to VKS

Để migrate một Cluster từ hệ thống VKS tới hệ thống VKS, hãy thực hiện theo các bước theo tài liệu này. Giả sử, tại Cluster nguồn, tôi đã triển khai một service nginx như sau:&#x20;

* File triển khai:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
  namespace: mynamespace
  labels:
    app: nginx
spec:
  ports:
  - port: 80
    name: web
  selector:
    app: nginx
  type: NodePort
---
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
  namespace: mynamespace
spec:
  selector:
    matchLabels:
      app: nginx
  serviceName: "nginx"
  replicas: 1
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
          name: web
        volumeMounts:
        - name: disk-ssd
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: disk-ssd
      namespace: mynamespace
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: ssd-3000
      resources:
        requests:
          storage: 40Gi
```

```bash
kubectl exec -n mynamespace -it web-0 bash
cd /usr/share/nginx/html
echo -e "<html>\n<head>\n  <title>MyVNGCloud</title>\n</head>\n<body>\n  <h1>Hello, MyVNGCloud</h1>\n</body>\n</html>" > index.html
```

* Lúc này, khi bạn truy cập vào Public IP của Node, bạn sẽ thấy "Hello, MyVNGCloud".

***

## Trên cả 2 Cluster (source and target)

* Tạo một **vStorage Project, Container** làm nơi nhận dữ liệu backup của cụm theo hướng dẫn tại [đây](../../../vstorage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-project/khoi-tao-project.md).
* Khởi tạo **S3 key** tương ứng với vStorage Project này theo hướng dẫn tại [đây](../../../vstorage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials/khoi-tao-s3-key.md).
* Tạo file **credentials-velero** với nội dung sau:

```yaml
[default]
aws_access_key_id=<AWS_ACCESS_KEY_ID>
aws_secret_access_key=<AWS_SECRET_ACCESS_KEY>
```

* Cài đặt Velero CLI:

```bash
curl -OL https://github.com/vmware-tanzu/velero/releases/download/v1.13.2/velero-v1.13.2-linux-amd64.tar.gz
tar -xvf velero-v1.13.2-linux-amd64.tar.gz
cp velero-v1.13.2-linux-amd64/velero /usr/local/bin
```

* Cài đặt Velero trên 2 cụm của bạn theo lệnh:

```bash
velero install --provider aws \
  --plugins velero/velero-plugin-for-aws:v1.9.0,velero/velero-plugin-for-csi:v0.7.0 \
  --secret-file ./credentials-velero \
  --bucket mycontainer \
  --backup-location-config region=hcm03,s3ForcePathStyle="true",s3Url=https://hcm03.vstorage.vngcloud.vn \
  --use-node-agent \
  --features=EnableCSI

# Enable CSI client:
velero client config set features=EnableCSI
```

{% hint style="info" %}
**Chú ý:**

* Khi bạn thực hiện migrate cluster từ VKS tới VKS, chúng tôi khuyến cáo bạn sử dụng **Snapshot** để migrate Volume của bạn từ cluster nguồn qua cluster đích.
{% endhint %}

* Cài đặt plugin **VNGCloud Snapshot Controller** trên 2 cluster theo lệnh:

```bash
helm repo add vks-helm-charts https://vngcloud.github.io/vks-helm-charts
helm repo update
helm install vngcloud-snapshot-controller vks-helm-charts/vngcloud-snapshot-controller \
  --replace --namespace kube-system
```

* Tạo một Storage Class

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name:  ssd-3000                           # [1] The StorageClass name, CAN be changed
provisioner: bs.csi.vngcloud.vn                     # The CSI driver name, MUST set this value
parameters:
  type: vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018  # Change it to your volume type UUID from portal
  ispoc: "true"
allowVolumeExpansion: true
```

***

## Tại Cluster nguồn

* Thực hiện apply file bên dưới để tạo default Volume Snapshot cho mọi PVC

```yaml
apiVersion: snapshot.storage.k8s.io/v1
kind: VolumeSnapshotClass
metadata:
  name: vngcloud-vsclass
  labels:
    velero.io/csi-volumesnapshot-class: "true"
driver: bs.csi.vngcloud.vn
deletionPolicy: Delete

# user can choose the VolumeSnapshotClass by setting annotation velero.io/csi-volumesnapshot-class_disk.csi.cloud.com: "test-snapclass" on backup resource.
# user can choose the VolumeSnapshotClass by setting annotation velero.io/csi-volumesnapshot-class: "test-snapclass" on PersistentVolumeClaim resource.
```

* Thực hiện backup theo cú pháp:

```bash
velero backup create mybackup --include-cluster-scoped-resources="" \
    --include-namespace-scoped-resources="*" \
    --include-namespaces mynamespace \
    --wait

# velero backup create mybackup \
#   --exclude-namespaces kube-system,kube-public,kube-node-lease,velero,default \
#   --wait

# --snapshot-move-data is Specify whether snapshot data should be moved

velero backup describe mybackup --details
```

## Tại Cluster đích

* Thực hiện restore theo lệnh:

```bash
velero restore create --from-backup mybackup
```
