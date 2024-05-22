# Migrate Cluster from another platform to VKS

Để migrate một Cluster từ hệ thống Cloud Provider hoặc On-premise tới hệ thống VKS, hãy thực hiện theo các bước bên dưới:&#x20;

## Trên cả 2 Cluster (source and target)

* Tạo một vStorage Project, Container làm nơi nhận dữ liệu backup của cụm theo hướng dẫn tại [đây](../../../vstorage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-project/khoi-tao-project.md).
* Khởi tạo S3 key tương ứng với vStorage Project này theo hướng dẫn tại đây.&#x20;
* Tạo file credentials-velero với nội dung sau:

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
velero install \
    --provider aws \
    --plugins velero/velero-plugin-for-aws:v1.9.0 \
    --use-node-agent \
    --use-volume-snapshots=false \
    --secret-file ./credentials-velero \
    --bucket mybucket \
    --backup-location-config region=hcm03,s3ForcePathStyle="true",s3Url=https://hcm03.vstorage.vngcloud.vn
```

## Tại Cluster nguồn

* Bạn có thể triển khai service nginx theo mẫu

```yaml
---
apiVersion: v1
kind: Namespace
metadata:
  name: mynamespace
---
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
      storageClassName: standard-rwo
      resources:
        requests:
          storage: 20Gi

```

```bash
kubectl exec -n mynamespace -it web-0 bash
cd /usr/share/nginx/html
echo -e "<html>\n<head>\n  <title>MyVNGCloud</title>\n</head>\n<body>\n  <h1>Hello, MyVNGCloud</h1>\n</body>\n</html>" > index.html
```

* Lúc này, khi bạn truy cập vào Public IP của Node, bạn sẽ thấy "Hello, MyVNGCloud".
* Đánh dấu Volume bạn muốn backup thông qua lệnh:

```bash
kubectl -n mynamespace annotate pod/web-0 backup.velero.io/backup-volumes=disk-ssd
```

* Thực hiện backup theo cú pháp:

```bash
velero backup create mybackup --include-cluster-scoped-resources="" \
    --include-namespace-scoped-resources="*" \
    --include-namespaces mynamespace \
    --parallel-files-upload 20 --wait

velero backup describe mybackup --details
```

## Tại Cluster đích

* Tạo file mapping Storage Class giữa Cluster nguồn và đích:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: change-storage-class-config
  namespace: velero
  labels:
    velero.io/plugin-config: ""
    velero.io/change-storage-class: RestoreItemAction
data:
  standard-rwo: sc-iops-200-retain
```

* Thực hiện restore theo lệnh:

```bash
velero restore create --from-backup mybackup
```

{% hint style="info" %}
**Chú ý:**

* Google Kubernetes Engine (GKE) không cho phép triển khai daemonset trên tất cả các node. Tuy nhiên, Velero chỉ cần triển khai daemonset trên node có mount PV. Giải pháp cho vấn đề này là bạn có thể điều chỉnh taint và toleration của daemonset để chỉ triển khai nó trên node có mount PV.
* Bạn có thể thay đổi yêu cầu tài nguyên mặc định `cpu:500m` và `mem:512M` trong bước cài đặt hoặc điều chỉnh khi triển khai yaml.
{% endhint %}
