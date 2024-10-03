# Migration Cluster from vContainer to VKS

**Tools used: Velero + vStorage (s3)**

## 1. Process <a href="#id-1.-quy-trinh" id="id-1.-quy-trinh"></a>

<figure><img src="../../.gitbook/assets/image (293).png" alt=""><figcaption></figcaption></figure>

**Process of migrating from vContainer to vKS (Customer + VNG Cloud)**

**Step 1:** Evaluate the current version of the vContainer cluster and the corresponding vKS cluster to migrate. At this point, there will be 2 cases (step 2 and step 3)

**Step 2:** If the vContainer version is lower than the versions currently supported by vKS, then the Custom Resources (CRDs) need to be reviewed for compatibility with the new kubernetes versions.

* If compatible with the new vKS version, continue with step 3.
* If not compatible, need to manually update and reconfigure CRD as well as related Applications.

**Step 3:** If the vContainer version is supported by vKS (1.27, 1.28 and 1.29), then you need to check the resources on vContainer before backing up. You need to pay attention to the following types of resources:

* **PV/PVC:** Velero does not support backup with hostPath type, only Local type is supported.
* **Ingress resources** : Ingress resources managed by **container-ingress-nginx-controller** will not work after migration.
* **Label and Taint nodes** : Velero does not re-attach Labels and Taints to nodes in the vKS

**Step 4** : Backup resources on vContainer cluster

**Step 5** : Restore resources on vKS cluster

**Step 6** : Perform testing and adjustments

## 2. Important Note: <a href="#id-2.-luu-y-quan-trong" id="id-2.-luu-y-quan-trong"></a>

### <mark style="color:red;">1. Mapping StorageClass on vKS cluster</mark> <a href="#id-1.-mapping-storageclass-tren-vks-cluster" id="id-1.-mapping-storageclass-tren-vks-cluster"></a>

Check the existing StorageClasses on vContainer and create corresponding StorageClasses on vKS. Then perform 1:1 mapping of StorageClasses between vContainer and vKS cluster.

Example ConfigMap file in **Step 3.**

### <mark style="color:red;">2. Use PersistentVolume as hostPath</mark> <a href="#id-2.-su-dung-persistentvolume-dang-hostpath" id="id-2.-su-dung-persistentvolume-dang-hostpath"></a>

**Velero does not support hostPath volume backup, only local.**

For clusters using PV type hostPath, it is necessary to convert to local type as follows:

**Note: Need to delete and redeploy the Application using PV type hostPath**

**Case 1:** Type Local supports hostPath path

For example, PV hostPath is configured to mount at the /opt/data folder, convert to Local type and mount back to Pods, according to the following form:

```bash
apiVersion: storage.k8s.io/v1 

kind: StorageClass 

metadata: 

  name: manual 

provisioner: kubernetes.io/no-provisioner 

volumeBindingMode: WaitForFirstConsumer 

--- 

apiVersion: v1 

kind: PersistentVolume 

metadata: 

  name: pv-volume 

  labels: 

    type: local 

spec: 

  storageClassName: manual 

  capacity: 

    storage: 1Gi 

  accessModes: 

    - ReadWriteOnce 

  local: 

    path: "/opt/data" 

  nodeAffinity: 

    required: 

      nodeSelectorTerms: 

      - matchExpressions: 

        - key: kubernetes.io/hostname 

          operator: Exists 

--- 

apiVersion: v1 

kind: PersistentVolumeClaim 

metadata: 

  name: pv-claim 

spec: 

  storageClassName: manual 

  accessModes: 

    - ReadWriteOnce 

  resources: 

    requests: 

      storage: 1Gi 
```

**Case 2:** Type Local does not support the original hostPath path

When creating PV/PVC according to Case 1, Pod cannot mount PVC and an error appears

**MountVolume.NewMounter initialization failed for volume "pvc" : path "/mnt/data" does not exist**

Copy the data to a new folder (eg /var, /opt, /tmp, ...) and repeat Case 1, then mount the PVC into the Pod as usual:

```bash
cp -R /mnt/data /var 
```

## 3. Detailed implementation steps <a href="#id-3.-cac-buoc-thuc-hien-chi-tiet" id="id-3.-cac-buoc-thuc-hien-chi-tiet"></a>

### Step 1: Install Velero on both clusters (vContainer and vKS) <a href="#buoc-1-cai-dat-velero-tren-ca-2-cluster-vcontainer-va-vks" id="buoc-1-cai-dat-velero-tren-ca-2-cluster-vcontainer-va-vks"></a>

Create a vStorage project, Container and corresponding S3 key to store backup data

On both clusters:

* Create a **credentials-velero** file with the following content:

```bash
[default] 
aws_access_key_id=________________________ # <= Adjust here 
aws_secret_access_key=________________________ # <= Adjust here 
```

* Install Velero CLI

```bash
curl -OL  https://github.com/vmware-tanzu/velero/releases/download/v1.14.1/velero-v1.14.1-linux-amd64.tar.gz 

tar -xvf velero-v1.14.1-linux-amd64.tar.gz 
cp velero-v1.14.1 -linux-amd64/velero /usr/local/bin 
```

* Install Velero on 2 kubernetes clusters

```bash
velero install \ 
    --provider aws \ 
    --plugins velero/velero-plugin-for-aws:v1.9.0 \ 
    --use-node-agent \ 
    --use-volume-snapshots=false \ 
    --secret-file ./credentials-velero \ 
    --bucket __________\                    # <= Adjust here 
    --backup-location-config region=hcm03,s3ForcePathStyle="true",s3Url=https://hcm03.vstorage.vngcloud.vn 
```

### Step 2: Perform backup on vContainer Cluster <a href="#buoc-2-thuc-hien-backup-tren-cluster-vcontainer" id="buoc-2-thuc-hien-backup-tren-cluster-vcontainer"></a>

* Annotate the Persistent Volumes to be backed up

```bash
./velero_helper.sh mark_volume --confirm 
```

* Annotate non-backup resources of kube-system

```bash
./velero_helper.sh mark_exclude --confirm 
```

* Annotate other resources (not marked in the velero\_helper.sh file), such as CSI, Ingress Controller, or other resources that you do not want to migrate (note that you need to label all resources of objects that do not need to be backed up).
  * For example, an application includes DaemonSet, Deployment, Pod, ... then it is necessary to mark labels for all those resources.

```bash
# Thêm label velero.io/exclude-from-backup=true cho từng resources 

 

## Với Cinder CSI 

kubectl -n kube-system label StatefulSet/csi-cinder-controllerplugin velero.io/exclude-from-backup=true 

kubec kubectl -n kube-system label DaemonSet/csi-cinder-nodeplugin velero.io/exclude-from-backup=true  

 

## Với vcontainer-ingress-nginx-controller 

kubectl -n kube-system label Deployment/ vcontainer-ingress-nginx-controller velero.io/exclude-from-backup=true 

kubectl -n kube-system label Deployment/ vcontainer-ingress-nginx-default-backend velero.io/exclude-from-backup=true 
```

* Perform check and attach Labels and Taints on vContainer nodes to vKS nodes before restore

```bash
# Kiểm tra các Label nodes 
./velero_helper.sh check_node_label 
# Kiểm tra các Taint nodes 
./velero_helper.sh check_node_taint 
```

* Create 2 backups for Cluster resources and Namespace resources according to the syntax

```bash
# Tạo cluster resource backup 
velero backup create vcontainer-cluster --include-namespaces ""  --include-cluster-resources=true --wait 

 

# Tạo cluster namespace backup 

velero backup create vcontainer-namespace --exclude-namespaces velero --wait 

 

# Xóa các bản backup (nếu cần) 

velero backup delete vcontainer-namespace vcontainer-cluster --confirm 
```

* View created backups and details of backed up resources (note **the STATUS** of the backup)

```bash
# List các bản backup được tạo 
velero get backup 

# Chi tiết của một bản backup 

velero backup describe <bk-name> --details 

# Xem logs quá trình backup 

velero backup logs <bk-name> 
```

### Step 3: Perform Restore on VKS Cluster <a href="#buoc-3-thuc-hien-restore-tren-cluster-vks" id="buoc-3-thuc-hien-restore-tren-cluster-vks"></a>

* If in the vContainer cluster using CSI is **cinder.csi.openstack.org** , need to perform StorageClass mapping between 2 clusters vContainer and vKS
  * Mapping **csi-sc-cinderplugin-nvme-5000** (vContainer) and **vngcloud-nvme-5000-delete** (vKS), similarly for other StorageClasses
  * In vKS, it is necessary to create corresponding StorageClasses.

Create **sc-mapping.yaml** file and apply on VKS cluster

```bash
apiVersion: v1 

kind: ConfigMap 

metadata: 

  name: change-storage-class-config 

  namespace: velero 

  labels: 

    velero.io/plugin-config: "" 

    velero.io/change-storage-class: RestoreItemAction 

data: 

  csi-sc-cinderplugin-nvme-5000: vngcloud-nvme-5000-delete 

  #_______old_storage_class_______: _______new_storage_class_______ # <= Add here 
```

* Add permissions for Velero to restore data PersistentVolume

Create **add-permission.yaml** file and apply on VKS cluster

```bash
apiVersion: v1 

kind: ConfigMap 

metadata: 

  name: fs-restore-action-config 

  namespace: velero 

  labels: 

    velero.io/plugin-config: "" 

    velero.io/pod-volume-restore: RestoreItemAction 

data: 

  secCtx: | 

    capabilities: 

      drop: [] 

      add: [] 

    allowPrivilegeEscalation: false 

    readOnlyRootFilesystem: true 

    runAsUser: 0 

    runAsGroup: 0 
```

* Perform restore in order
  * Note, for each restore, you need to check whether the restore process was successful or not before continuing to execute other commands.

```bash
# Kiểm tra restore 

velero get restore 

velero describe restore <restore-name> --details 
```

```bash
velero restore create --item-operation-timeout 1m --from-backup vcontainer-cluster --exclude-resources="MutatingWebhookConfiguration,ValidatingWebhookConfiguration" 
```

```bash
velero restore create --item-operation-timeout 1m --from-backup vcontainer-namespace 
```

```bash
velero restore create --item-operation-timeout 1m --from-backup vcontainer-cluster 
```

* In case of migrating to VKS and still using vcontainer-nginx-ingress-controller, it is necessary to change the Service type to LoadBalancer

```bash
kubectl patch service -n kube-system vcontainer-ingress-nginx-controller -p '{"spec": {"typ
```
