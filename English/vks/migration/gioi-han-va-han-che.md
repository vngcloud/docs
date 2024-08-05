# Migrate Limitation

When using Velero to migrate Cluster to Cluster, you can add the following options.

### Mark the Volumes you want to backup and unnecessary resources <a href="#danh-dau-cac-volume-ban-muon-backup-va-cac-resource-khong-can-thiet" id="danh-dau-cac-volume-ban-muon-backup-va-cac-resource-khong-can-thiet"></a>

To mark the Volumes you want to backup and unnecessary resources, first you need to download the bash helper script we provide and perform grand execute permission. You can see details of the tab file at: [velero\_helper.sh](https://raw.githubusercontent.com/vngcloud/velero/main/velero\_helper.sh)

#### 1. Convert hostPath Volume to Persistent Volume to be able to perform backup <a href="#id-1.-chuyen-hostpath-volume-thanh-persistent-volume-de-co-the-thuc-hien-backup" id="id-1.-chuyen-hostpath-volume-thanh-persistent-volume-de-co-the-thuc-hien-backup"></a>

Since Velero does not support backing up hostPath Volume, you need to convert hostPath Volume to Persistent Volume according to the following instructions:

*   To list hostPath Volumes in use:

    Copy

    ```
    ./helper.sh check_hostPath
    ```

#### 2. Mark Persistent Volume to include in backup <a href="#id-2.-mark-persistent-volume-to-include-in-backup" id="id-2.-mark-persistent-volume-to-include-in-backup"></a>

All data Persistent Volumes are stored on vStorage. Need to add annotation for all pods using PV with volume name:`backup.velero.io/backup-volumes=volume1,volume2`

*   Or you can automatically find volumes by:

    Copy

    ```
    ./helper.sh mark_volume
    ```

#### 3. Mark resources in exclude in backup <a href="#id-3.-mark-resource-in-exclude-in-backup" id="id-3.-mark-resource-in-exclude-in-backup"></a>

Because VKS operates under the Fully Managed Control Plane mechanism, you do not need to backup resources such as: `calico`, `kube-dns`, `kube-scheduler`, `kube-apiserver`,... In addition, vContainer resources such as: `magnum-auto-healer`, `cluster-autoscaler`, `csi-cinder`,... will also be ignored.

*   Identify resources that do not need backup via the command:

    Copy

    ```
    ./helper.sh mark_exclude
    ```

#### 4. Check label and taint of node <a href="#id-4.-check-label-and-taint-of-node" id="id-4.-check-label-and-taint-of-node"></a>

When performing a migration, it is possible that the resources in the source Cluster are using labels and taints. You need to ensure these important labels and taints exist in the target Cluster.

*   Check lable and taint via command:

    Copy

    ```
    ./helper.sh check_node_label
    ./helper.sh check_node_taint
    ```

#### 5. Mapping Storage Class <a href="#id-5.-mapping-storage-class" id="id-5.-mapping-storage-class"></a>

* If your Storage Class is different between the source Cluster and the destination Cluster, you need to transfer the Storage Class between the two clusters. For example:
  *   At the source Cluster, you have the following 2 Storage Classes:

      Copy

      ```
      @ kubectl get sc
      NAME                            PROVISIONER       RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
      sc-iops-200-retain (default)    csi.vngcloud.vn   Retain          Immediate           true                   81s
      sc-ssd-10000-delete (default)   csi.vngcloud.vn   Delete          Immediate           true                   14d
      ```
*   You can create a mapping file with content like the example below to convert 2 storage classes from the source Cluster into 2 storage classes at the destination Cluster. This file must be applied at the target Cluster before you run the backup command:

    Copy

    ```
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
