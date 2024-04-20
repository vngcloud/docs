# Integrate with Container Storage Interface (CSI)

Để integrate CSI với Kubernetes cluser, hãy làm theo các bước sau đây:

### Chuẩn bị <a href="#integratewithcontainerstorageinterface-csi-chuanbi" id="integratewithcontainerstorageinterface-csi-chuanbi"></a>

* Tạo một Kubernetes cluster trên VNGCloud, hoặc sử dụng một cluster đã có. Lưu ý: đảm bảo bạn đã tải xuống cluster configuration file sau khi cluster được khởi tạo thành công và truy cập vào cluster của bạn.

{% hint style="info" %}
**Chú ý:**&#x20;

Khi bạn thực hiện khởi tạo Cluster theo hướng dẫn bên trên, nếu bạn chưa **bật option** ![](<../../../../../.gitbook/assets/image (16).png>) **, mặc định chúng tôi sẽ không cài sẵn plugin này vào Cluster của bạn. Bạn cần tự thực hiện Khởi tạo Service Account và cài đặt VNGCloud BlockStorage CSI Driver** theo hướng dẫn bên dưới. Nếu bạn đã bật option ![](<../../../../../.gitbook/assets/image (17).png>), thì chúng tôi đã cài sẵn plugin này vào Cluster của bạn, hãy bỏ qua bước Khởi tạo Service Account, cài đặt **VNGCloud BlockStorage CSI Driver** và tiếp tục thực hiện theo hướng dẫn kể từ Deploy một Workload.
{% endhint %}

<details>

<summary>Khởi tạo Service Account và cài đặt <strong>VNGCloud BlockStorage CSI Driver</strong></summary>

### Khởi tạo Service Account

Khởi tạo hoặc sử dụng một **service account** đã tạo trên IAM và gắn policy: **vServerFullAccess**. Để tạo service account bạn truy cập tại [đây](https://hcm-3.console.vngcloud.vn/iam/service-accounts) và thực hiện theo các bước sau:

* Chọn "**Create a Service Account**", điền tên cho Service Account và nhấn **Next Step** để gắn quyền cho Service Account
* Tìm và chọn **Policy:** **vLBFullAccess và Policy:** **vServerFullAccess**, sau đó nhấn "**Create a Service Account**" để tạo Service Account, Policy: vLBFullAccess vàPolicy: vServerFullAccess do VNG Cloud tạo ra, bạn không thể xóa các policy này.
* Sau khi tạo thành công bạn cần phải lưu lại **Client\_ID** và **Secret\_Key** của Service Account để thực hiện bước tiếp theo.



### Cài đặt Helm <a href="#integratewithcontainerstorageinterface-csi-caidathelm" id="integratewithcontainerstorageinterface-csi-caidathelm"></a>

* Cài đặt Helm phiên bản từ 3.0 trở lên. Tham khảo tại [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/) để biết cách cài đặt.

***

### Cài đặt vngcloud-blockstorage-csi-driver <a href="#integratewithcontainerstorageinterface-csi-caidatvngcloud-blockstorage-csi-driver" id="integratewithcontainerstorageinterface-csi-caidatvngcloud-blockstorage-csi-driver"></a>

* Đầu tiên, thêm repo này vào cluster của bạn:

```
helm repo add vks-helm-charts https://vngcloud.github.io/vks-helm-charts
helm repo update
```

* Thay thế thông tin ClientID, Client Secret và tiếp tục chạy:

```
VNGCLOUD_CLIENT_ID=<put-your-client-id>
VNGCLOUD_CLIENT_SECRET=<put-your-client-secret>
VNGCLOUD_VKS_CLUSTER_ID=<put-your-vks-cluster-id>  # Optional

helm install vngcloud-blockstorage-csi-driver vks-helm-charts/vngcloud-blockstorage-csi-driver \
  --replace --namespace kube-system \
  --set vngcloudAccessSecret.keyId=${VNGCLOUD_CLIENT_ID} \
  --set vngcloudAccessSecret.accessKey=${VNGCLOUD_CLIENT_SECRET} \
  --set vngcloudAccessSecret.vksClusterId=${VNGCLOUD_VKS_CLUSTER_ID}  # Optional
```

* Sau khi việc cài đặt plugin hoàn tất, thực hiện kiểm tra trạng thái của vngcloud-blockstorage-csi-driver pods:

```
kubectl get pods -n kube-system | grep vngcloud-blockstorage-csi-driver
```

* Ngoài ra, chúng tôi sẽ có các bản cập nhật cho plugin này. Bạn có thể cập nhật chúng lên phiên bản mới nhất mà chúng tôi cung cấp bằng cách:

```
helm upgrade vngcloud-blockstorage-csi-driver vks-helm-charts/vngcloud-blockstorage-csi-driver -n kube-system
```

</details>

***

### Tạo Persistent Volume <a href="#integratewithcontainerstorageinterface-csi-taostorageclass" id="integratewithcontainerstorageinterface-csi-taostorageclass"></a>

* Bây giờ, bạn cần tạo tệp tin Yaml chứa các nội dung theo mẫu bên dưới. Ví dụ bạn có thể tạo tệp tin **persistent-volume.yaml** như bên dưới:&#x20;

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: my-expansion-storage-class                    # [1] The StorageClass name, CAN be changed
provisioner: bs.csi.vngcloud.vn                       # The VNG-CLOUD CSI driver name
parameters:
  type: vtype-bacd68a4-8758-4fb6-a739-b047665e05d5    # The volume type UUID
  isPOC: "true"
allowVolumeExpansion: true                            # MUST set this value to turn on volume expansion feature
---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-expansion-pvc                           # [2] The PVC name, CAN be changed
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 20Gi                                # [3] The PVC size, CAN be changed, this value MUST be in the valid range of the proper volume type
  storageClassName: my-expansion-storage-class     # [4] The StorageClass name, MUST be the same as [1]
---

apiVersion: v1
kind: Pod
metadata:
  name: nginx                                      # [5] The Pod name, CAN be changed
spec:
  containers:
    - image: nginx
      imagePullPolicy: IfNotPresent
      name: nginx
      ports:
        - containerPort: 80
          protocol: TCP
      volumeMounts:
        - mountPath: /var/lib/www/html
          name: my-volume-name                     # MUST be the same as [6]
  volumes:
    - name: my-volume-name                         # [6] The volume name, CAN be changed
      persistentVolumeClaim:
        claimName: my-expansion-pvc                # MUST be the same as [2]
        readOnly: false
```

Trong đó, bạn cần nhập name và nhập Volume type mà bạn mong muốn sử dụng. Danh sách các Volume Type mà vServer đang cung cấp tham khảo tại [Volume Types](../../../volume/volume-types.md).

* Tiếp theo, thực hiện triển khai tệp tin này vào cluster của bạn:

```
kubectl apply -f persistent-volume.yaml
```

* Sau khi apply tập tin thành công, bạn có thể kiểm tra danh sách service, pvc thông qua:&#x20;

```
kubectl get sc,pvc,pod -owide
```

```
NAME                                                       PROVISIONER          RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
storageclass.storage.k8s.io/my-expansion-storage-class     bs.csi.vngcloud.vn   Delete          Immediate           true                   2m8s
storageclass.storage.k8s.io/sc-iops-200-retain (default)   bs.csi.vngcloud.vn   Retain          Immediate           false                  130m

NAME                                     STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                 AGE    VOLUMEMODE
persistentvolumeclaim/my-expansion-pvc   Bound    pvc-ac19cd50-ef4f-447f-83fa-8f6caf6598bb   20Gi       RWO            my-expansion-storage-class   2m8s   Filesystem

NAME        READY   STATUS    RESTARTS   AGE    IP             NODE                                            NOMINATED NODE   READINESS GATES
pod/nginx   1/1     Running   0          2m8s   172.16.209.8   ng-e7df8b95-a6ed-4afd-8ac7-be4ad01301d2-588a6   <none>           <none>
```

***

### Tạo Snapshot <a href="#integratewithcontainerstorageinterface-csi-sudungcsitrongpod" id="integratewithcontainerstorageinterface-csi-sudungcsitrongpod"></a>

* Tạo tệp tin Yaml chứa các nội dung theo mẫu bên dưới. Dưới đây là tập tin YAML mẫu để tạo một volume thuộc my-storage-class. Volume này sử dụng ổ đĩa SSD và có kích thước 20GB.

volume.yaml

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: my-storage-class                            # [1] The StorageClass name, CAN be changed
provisioner: csi.vngcloud.vn                        # The CSI driver name
parameters:
  type: vtype-6790f903-38d2-454d-919e-5b49184b5927  # Change it to your volume type UUID from portal
---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc                                      # [2] The PVC name, CAN be changed
spec:
  accessModes:
  - ReadWriteOnce                                   # MUST set this value, currently only support RWO
  resources:
    requests:
      storage: 20Gi                                 # [3] The PVC size, CAN be changed, this value MUST be in the valid range of the proper volume type
  storageClassName: my-storage-class                # MUST be same value with [1], not set this value will use default StorageClass
---

apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - image: nginx
    imagePullPolicy: Always
    name: nginx
    ports:
    - containerPort: 80
      protocol: TCP
    volumeMounts:
      - mountPath: /var/lib/www/html                # The mount path in container, CAN be changed
        name: my-volume-name                        # MUST be same value with [4]
  volumes:
  - name: my-volume-name                            # [4] The volume mount name, CAN be changed
    persistentVolumeClaim:
      claimName: my-pvc                             # MUST be same value with [2]
      readOnly: false
```

Trong đó,&#x20;

* Thay đổi type trong StorageClass cho phù hợp với loại volume bạn muốn sử dụng.
* Thay đổi claimName trong Pod spec cho phù hợp với tên PersistentVolumeClaim bạn muốn sử dụng.
* Triển khai tệp tin vào cluster của bạn

volume.yaml

```
kubectl apply -f block-volume.yaml
```

* Sau khi apply tập tin thành công, bạn có thể kiểm tra danh sách service thông qua:&#x20;

```
kubectl get sc,pvc,pod -owide
```

<figure><img src="https://docs-admin.vngcloud.vn/download/attachments/73761117/image2024-3-17_22-50-12.png?version=1&#x26;modificationDate=1710690613000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

### Chỉnh sửa kích cỡ volume <a href="#integratewithcontainerstorageinterface-csi-chinhsuakichcovolume" id="integratewithcontainerstorageinterface-csi-chinhsuakichcovolume"></a>

* Để thực hiện chỉnh sửa kích cỡ volume, khi triển khai tệp tin yaml, bạn cần thiết lập allowVolumeExpansion: **true**. Ví dụ:&#x20;

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: my-expansion-storage-class                 # [1] The StorageClass name, CAN be changed
provisioner: csi.vngcloud.vn                       # The VNG-CLOUD CSI driver name
parameters:
  type: vtype-93a22a9f-1ec0-4e61-84fb-75ac181c13dc # The volume type UUID
allowVolumeExpansion: true                         # MUST set this value to turn on volume expansion feature
---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-expansion-pvc                           # [2] The PVC name, CAN be changed
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 20Gi                                # [3] The PVC size, CAN be changed, this value MUST be in the valid range of the proper volume type
  storageClassName: my-expansion-storage-class     # [4] The StorageClass name, MUST be the same as [1]
---

apiVersion: v1
kind: Pod
metadata:
  name: nginx                                      # [5] The Pod name, CAN be changed
spec:
  containers:
    - image: nginx
      imagePullPolicy: IfNotPresent
      name: nginx
      ports:
        - containerPort: 80
          protocol: TCP
      volumeMounts:
        - mountPath: /var/lib/www/html
          name: my-volume-name                     # MUST be the same as [6]
  volumes:
    - name: my-volume-name                         # [6] The volume name, CAN be changed
      persistentVolumeClaim:
        claimName: my-expansion-pvc                # MUST be the same as [2]
        readOnly: false
```

* Triển khai tệp tin lên cluster của bạn:

```
kubectl apply -f volume-resizing.yaml
```

* Lúc này, bạn có thể thực hiện resizing volume bằng cách:&#x20;

```
kubectl patch pvc my-expansion-pvc -p '{"spec":{"resources":{"requests":{"storage":"30Gi"}}}}'
kubectl get pvc my-expansion-pvc -o yaml  # Verify the PVC size
```

* Sau đó, bạn có thể thực hiện verify kích thước mới của volume theo lệnh:

```
kubectl exec -it nginx -- bash

# inside the nginx pod
lsblk
```
