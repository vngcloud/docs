# Các bước thực hiện

Bên dưới là các bước chung mà bạn cần thực hiện để migrate workload từ một Cluster sang một Cluster khác. Với mỗi trường hợp, có thể có thêm một vài bước. Chúng tôi đã liệt kê các trường hợp phổ biến nhất như sau, bạn có thể tham khảo và làm theo hướng dẫn tại:

* [Migrate Cluster from VKS to VKS](usecase/migrate-cluster-from-vks-to-vks.md)
* [Migrate Cluster from vContainer to VKS](usecase/migration-cluster-from-vcontainer-to-vks.md)
* [Migrate Cluster from another platform to VKS](usecase/migrate-cluster-from-other-to-vks.md)

***

## Chuẩn bị cluster đích (Prepare target resource)

Trên hệ thống VKS, bạn cần thực hiện khởi tạo một Cluster theo hướng dẫn tại [đây](../clusters/). Đảm bảo rằng cấu hình của cluster đích giống với cấu hình của cluster nguồn.

{% hint style="info" %}
**Chú ý:**

Để việc migrate thành công, trên Cluster đích, bạn cần đảm bảo các yêu cầu sau:

* Lượng resource cần thiết như số lượng node, cấu hình instance của node,...
* Boot volume > persistent volume size. (có thể down size sau khi restore thành công)
* Node labels và node taints giống cluster cũ.
* Storage Class tương ứng hoặc thay thế.
{% endhint %}

***

***

## \[Optional] Migrate resources private outside cluster

Migrating resources private outside cluster (di chuyển tài nguyên riêng tư bên ngoài cụm) là quá trình di chuyển tài nguyên riêng tư nằm ngoài Cluster nguồn sang một nơi mà Cluster đích có thể sử dụng. Ví dụ, bạn có thể có những tài nguyên riêng tư như image, database,... Lúc này, trước khi bắt đầu migrate, bạn cần tự thực hiện việc migrate các tài nguyên này. Ví dụ, nếu bạn cần:

* Migrate Container Images: bạn có thể migrate image tới VNGCloud Container Registry thông qua hướng dẫn tại [đây](../../vcontainer-registry/).
* Migrate Databases: bạn có thể sử dụng **Relational Database Service (RDS)** và **Object Storage Service (OBS)** tùy theo nhu cầu sử dụng của bạn. Sau khi việc migration hoàn tất, hãy nhớ config lại database cho applications của bạn trên VKS Cluster.
* Migrate Storage: bạn có thể sử dụng **NFS Server** của vServer.

{% hint style="info" %}
**Chú ý:**

* Sau khi bạn thực hiện migrate các resource ngoài Cluster, bạn cần đảm bảo Cluster đích kết nối được tới các resource đã migrate này.&#x20;
{% endhint %}

***

## Cài đặt Velero trên cả 2 cluster nguồn và cluster đích (Install Velero tool)

Sau khi bạn đã thực hiện migrate các tài nguyên private ngoài cluster, bạn có thể sử dụng công cụ migration để sao lưu (backup) và khôi phục (restore) application trên cluster nguồn và cluster đích.

* Tạo một vStorage Project , Container làm nơi nhận dữ liệu backup của cụm theo hướng dẫn tại [đây](../../vstorage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-project/khoi-tao-project.md).
* Khởi tạo S3 key tương ứng với vStorage Project này theo hướng dẫn tại [đây](../../vstorage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials/khoi-tao-s3-key.md).

Ví dụ, tôi đã khởi tạo một vStorage Project, Container có thông tin sau: Region: HCM03, Container: mycontainer, Endpoint: [https://hcm03.vstorage.vngcloud.vn](https://hcm03.vstorage.vngcloud.vn).

* Tạo file credentials-velero với nội dung sau:

```yaml
[default]
aws_access_key_id=________CLIENT_ID____________
aws_secret_access_key=________CLIENT_SECRET____________
```

* Cài đặt Velero CLI theo câu lệnh:

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
    --bucket mycontainer \
    --backup-location-config region=hcm03,s3ForcePathStyle="true",s3Url=https://hcm03.vstorage.vngcloud.vn
```

***

## Sao lưu (Backup)

Trước khi thực hiện sao lưu, tùy theo nhu cầu migrate của bạn mà sẽ có thêm một vài bước như sau:&#x20;

### Đối với VNGCloud Ingress Controller

* Nếu Cluster nguồn của bạn đang sử dụng plugin `vngcloud-ingress-controller`: bạn cần thêm annotation `vks.vngcloud.vn/ignore: true` cho tất cả **Ingress resource**. Sau khi hoàn thành restore ở bước cuối cùng thì bạn cần thực hiện xóa annotation này đi.
* Ngoài `vngcloud-ingress-controller,`những Ingress controller khác như `nginx-ingress-controller` sẽ không cần thêm annotation `vks.vngcloud.vn/ignore` và sẽ được migrate bình thường mà không bị ảnh hưởng.

### Đối với VNGCloud Controller Manager

* Nếu Cluster nguồn của bạn đang sử dụng plugin `vngcloud-controller-manager:` bạn cần thêm annotation `vks.vngcloud.vn/ignore: true` cho tất cả **Service Type LoadBalancer**. Sau khi hoàn thành restore ở bước cuối cùng thì bạn cần thực hiện xóa annotation này đi.
* Nếu không, đảm bảo `vngcloud-controller-manager` đã được gỡ bỏ trên Cluster đích.

### Đánh dấu các Volume bạn muốn backup và các resource không cần thiết

Để đánh dấu các Volume bạn muốn backup và các resource không cần thiết, đầu tiên bạn cần tài xuống đoạn helper bash script được chung tôi cung cấp sẵn và thực hiện grand execute permission. Chi tiết file mấu bạn có thể xem tại: [velero\_helper.sh](https://raw.githubusercontent.com/vngcloud/velero/main/velero\_helper.sh)

#### 1. Chuyển hostPath Volume thành Persistent Volume để có thể thực hiện backup

Do Velero không hỗ trợ sao lưu hostPath Volume, bạn cần phải chuyển hostPath Volume thành Persistent Volume theo hướng dẫn sau đây:&#x20;

* Để list các hostPath Volume đang sử dụng:

```bash
./helper.sh check_hostPath
```

#### 2. Mark Persistent Volume to include in backup

Tất cả data Persistent Volumes được lưu trữ trên vStorage. Cần thêm annotation cho tất cả pod dùng PV với volume name: `backup.velero.io/backup-volumes=volume1,volume2`

* Hoặc có thể tự động tìm các volume bằng cách:

```bash
./helper.sh mark_volume
```

#### 3. Mark resource in exclude in backup

Do VKS hoạt động theo cơ chế Fully Managed Control Plane, nên bạn không cần backup các resource như: `calico`, `kube-dns`, `kube-scheduler`, `kube-apiserver`,... Ngoài ra, các resource của vContainer như là: `magnum-auto-healer`, `cluster-autoscaler`, `csi-cinder`,... cũng sẽ được bỏ qua.

* Đánh dầu resource không cần backup thông qua lệnh:

```bash
./helper.sh mark_exclude
```

#### 4. Check label and taint of node

Khi thực hiện migrate, có thể tài nguyên trong Cluster nguồn đang sử dụng label và taint. Bạn cần đảm bảo các label và taint quan trọng này tồn tại trong Cluster đích.

* Kiểm tra lable và taint thông qua lệnh:

```bash
./helper.sh check_node_label
./helper.sh check_node_taint
```

#### 6. Mapping Storage Class

* Nếu Storage Class của bạn khác nhau giữa Cluster nguồn và Cluster đích, bạn cần chuyển Storage Class giữa 2 cụm. Ví dụ:
  * Tại Cluster nguồn, bạn đang có 2 Storage Class sau:

```bash
@ kubectl get sc
NAME                            PROVISIONER       RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
sc-iops-200-retain (default)    csi.vngcloud.vn   Retain          Immediate           true                   81s
sc-ssd-10000-delete (default)   csi.vngcloud.vn   Delete          Immediate           true                   14d
```

* Bạn có thể tạo file mapping chưa nội dung như ví dụ bên dưới để thực hiện chuyển đổi 2 storage class từ Cluster nguồn thành 2 storage class tại Cluster đích. File này phải được apply tại Cluster đích trước khi bạn chạy lệnh backup:

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
  sc-iops-200-retain: ssd-200
  sc-ssd-10000-delete: ssd-10000
```

### Tạo backup

* Thực hiện chạy lệnh bên dưới để thực hiện backup:

```bash
velero backup create <backup_name> --exclude-namespaces velero \
    --include-cluster-resources=true \
    --wait

velero backup describe <backup_name> --details
```

* Kết quả trả về như sau là việc backup đã thành công:

```bash
velero backup get
NAME               STATUS      ERRORS   WARNINGS   CREATED                         EXPIRES   STORAGE LOCATION   SELECTOR
wordpress-backup   Completed   0        0          2021-10-14 15:32:07 +0800 CST   29d       default            <none>
```

***

## Khôi phục (Restore)

Trong quá trình khôi phục tại cluster đích, Velero sẽ thực hiện tải dữ liệu sao lưu xuống cụm mới và triển khai lại tài nguyên dựa trên tệp JSON.

* Lấy danh sách tất cả các bản backup đã tạo theo lệnh:&#x20;

```bash
velero backup get
```

* Thực hiện restore từ một bản backup theo lệnh:&#x20;

```bash
velero restore create --from-backup <backup_name>
```

***

## Update resource config

* Nếu bạn thêm các annotation theo hướng dẫn bên trên thì lúc này, bạn cần xóa các annotation đã gắn trên **Ingress Resource** và **Service type LoadBalancer.**
* Sau khi tài nguyên của cluster đích được triển khai đúng cách, bạn có thể thực hiện **switch traffic** cho dịch vụ của bạn. Sau khi xác nhận rằng tất cả các dịch vụ đều chạy bình thường, bạn có thể thực hiện xóa cluster nguồn.
