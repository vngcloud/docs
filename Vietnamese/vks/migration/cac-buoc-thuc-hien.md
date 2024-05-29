# Các bước thực hiện

Bên dưới là các bước chung mà bạn cần thực hiện để migrate workload từ một Cluster sang một Cluster khác. Với mỗi trường hợp, có thể có thêm một vài bước. Chúng tôi đã liệt kê các trường hợp phổ biến nhất như sau, bạn có thể tham khảo và làm theo hướng dẫn tại:

* [Migrate Cluster from VKS to VKS](usecase/migrate-cluster-from-vks-to-vks.md)
* [Migrate Cluster from vContainer to VKS](usecase/migration-cluster-from-vcontainer-to-vks.md)
* [Migrate Cluster from another platform to VKS](usecase/migrate-cluster-from-other-to-vks.md)

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

## \[Optional] Migrate resources private outside cluster

Migrating resources private outside cluster (di chuyển tài nguyên riêng tư bên ngoài cụm) là quá trình di chuyển tài nguyên riêng tư nằm ngoài Cluster nguồn sang một nơi mà Cluster đích có thể sử dụng. Ví dụ, bạn có thể có những tài nguyên riêng tư như image, database,... Lúc này, trước khi bắt đầu migrate, bạn cần tự thực hiện việc migrate các tài nguyên này. Ví dụ, nếu bạn cần:

* Migrating Container Images: vui lòng tham khảo thêm tại [đây](../../vcontainer-registry/) để thực hiện migrate image giữa 2 Cluster.
* Migrating Databases and Storage (On-Demand): Bạn có thể sử dụng Relational **Database Service (RDS)** và **Object Storage Service (OBS)** tùy theo nhu cầu sử dụng của bạn. Sau khi việc migration hoàn tất, hãy nhớ config lại database và storage cho applications của bạn trên VKS Cluster.

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
    --bucket my-bucket \
    --backup-location-config region=hcm03,s3ForcePathStyle="true",s3Url=https://hcm03.vstorage.vngcloud.vn
```

## Sao lưu (Backup)

### Ingress và Service LoadBalancer

* Ingress controller
  * Nếu cụm source đã sử dụng `vngcloud-ingress-controller`: thêm annotation `vks.vngcloud.vn/ignore: true` cho tất cả Ingress resource. Sau khi hoàn thành restore thì xóa annotation này đi.
  * Những ingress contoller khác sẽ không bị ảnh hưởng, ngoại trừ `nginx-ingress-controller` của vContainer (tạo lại khi qua cụm mới).
* Cloud controller manager: Chỉ duy nhất 1 CCM có thể chạy trên 1 cụm.
  * Nếu có ý định sử dụng `vngcloud-controller-manager` trong cụm đích: thêm annotation `vks.vngcloud.vn/ignore: true` cho tất cả Service type LoadBalancer. Sau khi hoàn thành restore thì xóa annotation này đi.
  * Nếu không, đảm bảo `vngcloud-controller-manager` đã được gỡ bỏ trên cụm VKS.

### Mark volume to backup and resource unnnecessary

Link to helper file: [helper.sh](https://raw.githubusercontent.com/anngdinh/vcontainer-helm-infra-documentation/main/src/helm-charts/migrate/helper.sh). Create a file named `helper.sh` and grant execute permission.

#### 1. Chuyển hostPath volume thành Persistent Volume để có thể backup

Vì velero không hỗ trợ sao lưu hostPath volume, cần phải chuyển thành Persistent Volume. [Link](https://anngdinh.github.io/vcontainer-helm-infra-documentation/helm-charts/migrate/more-usage/troubleshooting.html)

Để list các hostPath đang sử dụng:

```bash
./helper.sh check_hostPath
```

#### 2. Mark Persistent Volume to include in backup

Tất cả data Persistent Volumes được lưu trữ trên vStorage. Cần thêm annotation cho tất cả pod dùng PV với volume name: `backup.velero.io/backup-volumes=volume1,volume2`

Hoặc có thể tự động tìm các volume bằng cách:

```bash
./helper.sh mark_volume
```

#### 3. Mark resource in exclude in backup

Vì VKS là fully managed cluster, nên không cần backup các resource như: `calico`, `kube-dns`, `kube-scheduler`, `kube-apiserver`,... Ngoài ra, các resource của vContainer như là: `magnum-auto-healer`, `cluster-autoscaler`, `csi-cinder`,... cũng sẽ bỏ qua.

```bash
./helper.sh mark_exclude
```

#### 4. Check label and taint of node

Có thể tài nguyên trong cụm nguồn sử dụng label và taint. Đảm bảo rằng các nhãn và taint quan trọng này tồn tại trong cụm taget.

```bash
./helper.sh check_node_label
./helper.sh check_node_taint
```

#### 6. Mapping Storage Class

Cần chuyển Storage Class trong cụm nguồn tới cụm đích. Giả sử có 2 SC bên dưới:

```bash
@ kubectl get sc
NAME                            PROVISIONER       RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
sc-iops-200-retain (default)    csi.vngcloud.vn   Retain          Immediate           true                   81s
sc-ssd-10000-delete (default)   csi.vngcloud.vn   Delete          Immediate           true                   14d
```

Và bạn muốn chuyển đổi sang 2 Storage Class `ssd-200`, `ssd-10000` trong target cluster theo thứ tự thì bạn phải áp dụng yaml này trong **target cluster**:

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

#### 7. Tạo backup

```bash
velero backup create wordpress-backup --exclude-namespaces velero \
    --include-cluster-resources=true \
    --wait

velero backup describe wordpress-backup --details
```

* Kết quả trả về như sau là việc backup đã thành công:

```bash
velero backup get
NAME               STATUS      ERRORS   WARNINGS   CREATED                         EXPIRES   STORAGE LOCATION   SELECTOR
wordpress-backup   Completed   0        0          2021-10-14 15:32:07 +0800 CST   29d       default            <none>
```

## Khôi phục (Restore)

Trong quá trình khôi phục tại cluster đích, Velero sẽ thực hiện tải dữ liệu sao lưu xuống cụm mới và triển khai lại tài nguyên dựa trên tệp JSON.

Get backup:

```bash
velero backup get
```

Create restore from backup:

```bash
velero restore create --from-backup wordpress-backup
```

## Sau khi khôi phục thành công

Cần xóa các annotation đã gắn của Ingress và Service type LoadBalancer.
