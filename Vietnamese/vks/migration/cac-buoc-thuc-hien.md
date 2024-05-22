# Các bước thực hiện



### Chuẩn bị cluster đích (Prepard target resource)

Trên hệ thống VKS, bạn cần thực hiện khởi tạo một Cluster theo hướng dẫn tại [đây](../clusters/). Đảm bảo rằng cấu hình của cluster đích giống với cấu hình của cluster nguồn.

***

### Migrate resources private outside cluster

Migrating resources private outside cluster (di chuyển tài nguyên riêng tư bên ngoài cụm) là quá trình di chuyển tài nguyên riêng tư nằm trên Cluster nguồn sang một Cluster đích. Ví dụ, bạn có thể có những tài nguyên riêng tư như image, database,... Lúc này, trước khi bắt đầu migrate, bạn cần tự thực hiện việc migrate các tài nguyên này.

#### Migrating Container Images

Tham khảo thêm tại [đây](../../vcontainer-registry/) để thực hiện migrate image giữa 2 Cluster.

#### Migrating Databases and Storage (On-Demand) <a href="#migrating-databases-and-storage-on-demand" id="migrating-databases-and-storage-on-demand"></a>

Bạn có thể sử dụng  Relational **Database Service (RDS)** và **Object Storage Service (OBS)** tùy theo nhu cầu sử dụng của bạn. Sau khi việc migration hoàn tất, hãy nhớ config lại database và storage cho applications của bạn trên VKS Cluster.

***

### Cài đặt Velero trên cả 2 cluster nguồn và cluster đích(Install Velero tool)

Sau khi bạn đã thực hiện migrate các tài nguyên private ngoài cluster, bạn có thể sử dụng công cụ migration để sao lưu (backup) và khôi phục (restore) application trên cluster nguồn và cluster đích.&#x20;

* Tạo một vStorage Project , Container làm nơi nhận dữ liệu backup của cụm theo hướng dẫn tại [đây](../../vstorage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-project/khoi-tao-project.md).
* Khởi tạo S3 key tương ứng với vStorage Project này theo hướng dẫn tại [đây](../../vstorage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials/khoi-tao-s3-key.md).

Ví dụ, tôi đã khởi tạo một vStorage Project, Container có thông tin sau: Region: HCM03, Container: my-container, Endpoint: [https://hcm03.vstorage.vngcloud.vn](https://hcm03.vstorage.vngcloud.vn).

* Tạo file credentials-velero với nội dung sau:

```yaml
[default]
aws_access_key_id=<AWS_ACCESS_KEY_ID>
aws_secret_access_key=<AWS_SECRET_ACCESS_KEY>
```

* Cài đặt Velero CLI theo câu lệnh:&#x20;

```yaml
curl -OL https://github.com/vmware-tanzu/velero/releases/download/v1.13.2/velero-v1.13.2-linux-amd64.tar.gz
tar -xvf velero-v1.13.2-linux-amd64.tar.gz
cp velero-v1.13.2-linux-amd64/velero /usr/local/bin
```

* Cài đặt Velero trên cluster của bạn

```yaml
velero install \
    --provider aws \
    --plugins velero/velero-plugin-for-aws:v1.9.0 \
    --use-node-agent \
    --use-volume-snapshots=false \
    --secret-file ./credentials-velero \
    --bucket my-bucket \
    --backup-location-config region=hcm03,s3ForcePathStyle="true",s3Url=https://hcm03.vstorage.vngcloud.vn \

# flag `--default-volumes-to-fs-backup` will backup all persistent volume as file system volume
```

***

### Sao lưu (Backup)

Để sao lưu tài nguyên, hãy sử dụng công cụ Velero để tạo đối tượng sao lưu trong cluster nguồn. Velero sẽ thực hiện truy vấn, đóng gói dữ liệu và tải chúng lên một S3 Compatible Object Storage.&#x20;

* \[Optional] Để sao lưu dữ liệu của storage volume được chỉ định trong pod, hãy thêm annotation vào pod. Ví dụ:

```yaml
kubectl -n <namespace> annotate pod/<pod_name> backup.velero.io/backup-volumes=<volume_name_1>,<volume_name_2>,...
# Eg: kubectl annotate pod/wordpress-758fbf6fc7-s7fsr backup.velero.io/backup-volumes=wp-storage
# Eg: kubectl annotate pod/mysql-5ffdfbc498-c45lh backup.velero.io/backup-volumes=mysql-storage
```

* Chạy lệnh dưới để backup dữ liệu cluster của bạn:

Bạn có thể tạo bản sao lưu mặc định với tất cả tài nguyên hoặc tài nguyên cụ thể hơn bằng cách thêm các cờ này. Chi tiết tham khảo thêm tại [Resource filtering](https://velero.io/docs/v1.13/resource-filtering/).

```yaml
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

Trong đó:&#x20;

* `--include-namespaces`: chỉ định namespace bạn muốn backup

```yaml
velero backup create <backup-name> --include-namespaces <namespace>
```

* `--include-resources`: chỉ định resource cụ thể bạn muốn backup

```yaml
velero backup create <backup-name> --include-resources deployments
```

* `--selector`: backup resource match với điều kiện chỉ định trước

```yaml
velero backup create <backup-name> --selector <key>=<value>
```

* Kiểm tra trạng thái backup thông qua cú pháp

```
$ velero backup get
```

* Kết quả trả về như sau là việc backup đã thành công:

```
NAME               STATUS      ERRORS   WARNINGS   CREATED                         EXPIRES   STORAGE LOCATION   SELECTOR
wordpress-backup   Completed   0        0          2021-10-14 15:32:07 +0800 CST   29d       default            <none>
```

***

### Khôi phục (Restore)

Trong quá trình khôi phục tại cluster đích, Velero sẽ thực hiện tải dữ liệu sao lưu xuống cụm mới và triển khai lại tài nguyên dựa trên tệp JSON.

* \[Optional] Velero có thể thay đổi PV/PVC Storage Classes của Persistent Volumes and Persistent Volume Claims trong giai đoạn restore Cluster. Để thiết lập mapping Storage Class, hãy tạo file mapping với namespace: velero theo mẫu:

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
  <old-storage-class>: <new-storage-class>
  <old-storage-class>: <new-storage-class>
```

* \[Optional] Thay đổi Pod/ Deployment/ StatefulSet/ DaemonSet/ ReplicaSet/ ReplicationController/ Job/ CronJob Image Repositories theo hướng dẫn tại [đây](https://velero.io/docs/v1.13/restore-reference/).

***

### Update resource config

&#x20;Sau khi tài nguyên của cluster đích được triển khai đúng cách, bạn có thể thực hiện switch traffic cho dịch vụ của bạn. Sau khi xác nhận rằng tất cả các dịch vụ đều chạy bình thường, bạn có thể thực hiện xóa cluster nguồn.

