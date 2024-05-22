# Các bước thực hiện



### Chuẩn bị cluster đích (Prepard target resource)

Trên hệ thống VKS, bạn cần thực hiện khởi tạo một Cluster theo hướng dẫn tại [đây](../clusters/). Đảm bảo rằng cấu hình của cluster đích giống với cấu hình của cluster nguồn.

***

### Migrate resources private outside cluster



***

### Cài đặt Velero trên cả 2 cluster nguồn và cluster đích(Install Velero tool)

Sau khi bạn đã thực hiện migrate các tài nguyên private ngoài cluster, bạn có thể sử dụng công cụ migration để sao lưu (backup) và khôi phục (restore) application trên cluster nguồn và cluster đích.&#x20;

* Tạo một vStorage Project làm nơi nhận dữ liệu backup của cụm theo hướng dẫn tại [đây](../../vstorage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-project/khoi-tao-project.md).
* Khởi tạo S3 key tương ứng với vStorage Project này theo hướng dẫn tại [đây](../../vstorage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials/khoi-tao-s3-key.md).
* Tạo file credentials-velero với nội dung sau:

```
[default]
aws_access_key_id=<AWS_ACCESS_KEY_ID>
aws_secret_access_key=<AWS_SECRET_ACCESS_KEY>
```

* Cài đặt Velero CLI theo câu lệnh:&#x20;

```
curl -OL https://github.com/vmware-tanzu/velero/releases/download/v1.13.2/velero-v1.13.2-linux-amd64.tar.gz
tar -xvf velero-v1.13.2-linux-amd64.tar.gz
cp velero-v1.13.2-linux-amd64/velero /usr/local/bin
```

* Cài đặt Velero trên cluster của bạn

```
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

* Chạy lệnh dưới để backup dữ liệu cluster của bạn&#x20;

```
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

### Khôi phục (Restore)

Trong quá trình khôi phục tại cluster đích, Velero sẽ thực hiện tải dữ liệu sao lưu xuống cụm mới và triển khai lại tài nguyên dựa trên tệp JSON.

### Update resource config

&#x20;Sau khi tài nguyên của cluster đích được triển khai đúng cách, bạn có thể thực hiện switch traffic cho dịch vụ của bạn. Sau khi xác nhận rằng tất cả các dịch vụ đều chạy bình thường, bạn có thể thực hiện xóa cluster nguồn.

