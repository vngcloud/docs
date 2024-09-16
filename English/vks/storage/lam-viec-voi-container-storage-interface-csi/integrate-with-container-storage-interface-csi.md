# Integrate with Container Storage Interface (CSI)

To integrate CSI with Kubernetes cluster, follow these steps:

## Prepare <a href="#integratewithcontainerstorageinterface-csi-chuanbi" id="integratewithcontainerstorageinterface-csi-chuanbi"></a>

* Create a Kubernetes cluster on VNGCloud, or use an existing cluster. Note: make sure you have downloaded the cluster configuration file once the cluster has been successfully initialized and accessed your cluster.

## Create Service Account and install VNGCloud BlockStorage CSI Driver <a href="#exposemotservicethongquavlblayer7-khoitaoserviceaccountvacaidatvngcloudingresscontroller" id="exposemotservicethongquavlblayer7-khoitaoserviceaccountvacaidatvngcloudingresscontroller"></a>

{% hint style="info" %}
**Attention:**

* When you initialize the Cluster according to the instructions above, if you have not enabled the **Enable BlockStore Persistent Disk CSI Driver** option , by default we will not pre-install this plugin into your Cluster. You need to manually create Service Account and install VNGCloud BlockStorage CSI Driver according to the instructions below. If you have enabled the **Enable BlockStore Persistent Disk CSI Driver** option , we have pre-installed this plugin into your Cluster, skip the Service Account Initialization step, install VNGCloud BlockStorage CSI Driver and continue following the instructions from now on. Deploy a Workload.
* <mark style="color:red;">**VNGCloud BlockStorage CSI Driver**</mark> <mark style="color:red;"></mark><mark style="color:red;">only supports attaching volumes to a single node (VM) throughout the life of that volume. If you have a need for ReadWriteMany, you may consider using the NFS CSI Driver, as it allows multiple nodes to Read and Write on the same volume at the same time. This is very useful for applications that need to share data between multiple pods or services in Kubernetes.</mark>
{% endhint %}

<details>

<summary>Create Service Account and install VNGCloud BlockStorage CSI Driver</summary>

**Initialize Service Account**

* Create or use a **service account** created on IAM and attach policy: **vServerFullAccess** . To create a service account, go here [and](https://hcm-3.console.vngcloud.vn/iam/service-accounts) follow these steps:
  * Select " **Create a Service Account** ", enter a name for the Service Account and click **Next Step** to assign permissions to the Service Account
  * Find and select **Policy: vServerFullAccess** , then click " **Create a Service Account** " to create a Service Account, Policy: vLBFullAccess and Policy: vServerFullAccess are created by VNG Cloud, you cannot delete these policies.
  * After successful creation, you need to save **the Client\_ID** and **Secret\_Key** of the Service Account to perform the next step.

**Install VNGCloud BlockStorage CSI Driver**

* Install Helm version 3.0 or higher. Refer to [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/) for instructions on how to install.
*   Add this repo to your cluster via the command:

    ```
    helm repo add vks-helm-charts https://vngcloud.github.io/vks-helm-charts
    helm repo update
    ```
*   Replace your K8S cluster's ClientID, Client Secret, and ClusterID information and continue running:

    Copy

    ```
    helm install vngcloud-blockstorage-csi-driver vks-helm-charts/vngcloud-blockstorage-csi-driver \
      --replace --namespace kube-system \
      --set vngcloudAccessSecret.keyId=${VNGCLOUD_CLIENT_ID} \
      --set vngcloudAccessSecret.accessKey=${VNGCLOUD_CLIENT_SECRET} \
      --set vngcloudAccessSecret.vksClusterId=${VNGCLOUD_VKS_CLUSTER_ID}  # Optional
    ```
*   After the installation is complete, check the status of vngcloud-blockstorage-csi-driver pods:

    ```
    kubectl get pods -n kube-system | grep vngcloud-csi-
    ```
*   For example, in the image below you have successfully installed vngcloud-blockstorage-csi-driver:

    ```
    NAME                                           READY   STATUS    RESTARTS       AGE
    vngcloud-csi-controller-56bd7b85f-ctpns        7/7     Running   6 (2d4h ago)   2d4h
    vngcloud-csi-controller-56bd7b85f-npp9n        7/7     Running   2 (2d4h ago)   2d4h
    vngcloud-csi-node-c8r2w                        3/3     Running   0              2d4h
    ```

</details>

***

## Deploy a Workload <a href="#exposemotservicethongquavlblayer7-deploymotworkload" id="exposemotservicethongquavlblayer7-deploymotworkload"></a>

The following is a guide for you to deploy the nginx service on Kubernetes.

### **Step 1** : **Create Deployment for Nginx app.**

*   Create **nginx-service.yaml** file with the following content:

    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-app
    spec:
      selector:
        matchLabels:
          app: nginx
      replicas: 1
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
          - name: nginx
            image: nginx:1.19.1
            ports:
            - containerPort: 80
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: nginx-service
    spec:
      selector:
        app: nginx 
      ports:
        - protocol: TCP
          port: 80
          targetPort: 80
    ```
*   Deploy This deployment equals:

    ```
    kubectl apply -f nginx-service.yaml
    ```

***

### **Step 2: Check the Deployment and Service information just deployed**

*   Run the following command to test **Deployment**

    ```
    kubectl get svc,deploy,pod -owide
    ```
*   If the results are returned as below, it means you have deployed Deployment successfully.

    ```
    NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)           AGE     SELECTOR
    service/kubernetes      ClusterIP      10.96.0.1       <none>        443/TCP           2d4h    <none>
    service/nginx-app       NodePort       10.96.215.192   <none>        30080:31289/TCP   6m12s   app=nginx
    service/nginx-service   LoadBalancer   10.96.179.221   <pending>     80:32624/TCP      16s     app=nginx

    NAME                        READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
    deployment.apps/nginx-app   1/1     1            1           16s   nginx        nginx:1.19.1   app=nginx

    NAME                             READY   STATUS    RESTARTS   AGE   IP              NODE                                            NOMINATED NODE   READINESS GATES
    pod/nginx-app-7f45b65946-t7d7k   1/1     Running   0          16s   172.16.24.202   ng-3f06013a-f6a5-47ba-a51f-bc5e9c2b10a7-ecea1   <none>           <none>
    ```

***

### **Create Persistent Volume** <a href="#tao-persistent-volume" id="tao-persistent-volume"></a>

*   Create a **persistent-volume.yaml** file with the following content:

    Copy

    ```
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: my-expansion-storage-class                    # [1] The StorageClass name, CAN be changed
    provisioner: bs.csi.vngcloud.vn                       # The VNG-CLOUD CSI driver name
    parameters:
      type: vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018    # The volume type UUID
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
*   Run the following command to deploy a Pod using a Persistent Volume

    Copy

    ```
    kubectl apply -f persistent-volume.yaml
    ```

At this time, the vServer system will automatically create a Volume corresponding to the yaml file above, for example:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F8svzf7rbhsyezgepb2x1%252Fimage.png%3Falt%3Dmedia%26token%3Dbdb7092a-4130-48a2-a86b-879b7a2f53e2&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=2952fe1e&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

### **Create Snapshots** <a href="#tao-snapshot" id="tao-snapshot"></a>

Snapshot is a low-cost, convenient and effective data backup method and can be used to create images, restore data and distribute copies of data. If you are a new user who has never used the Snapshot service, you will need to Activate Snapshot Service before you can create a Snapshot for your Persistent Volume.

#### **Activate Snapshot Service**

To be able to create Snapshots, you need to perform Activate Snapshot Service. You will not be charged for activating the snapshot service. After you create snapshots, costs will be calculated based on the storage capacity and storage time of these snapshots. Follow these steps to enable the Snapshot service:

**Step 1:** Visit [https://hcm-3.console.vngcloud.vn/vserver/block-store/snapshot/overview](https://hcm-3.console.vngcloud.vn/vserver/block-store/snapshot/overview)

**Step 2:** Select **Activate Snapshot Service** .

For example:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FicsrvGVI2RNcZHyA3r8e%252Fimage.png%3Falt%3Dmedia%26token%3D7a126a23-ea0e-451b-82f3-b601ba34b652&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b652b4a3&#x26;sv=1" alt=""><figcaption></figcaption></figure>

#### **Install VNGCloud Snapshot Controller**

* Install Helm version 3.0 or higher. Refer to [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/) for instructions on how to install.
*   Add this repo to your cluster via the command:

    ```
    helm repo add vks-helm-charts https://vngcloud.github.io/vks-helm-charts
    helm repo update
    ```
*   Continue running:

    ```
    helm install vngcloud-snapshot-controller vks-helm-charts/vngcloud-snapshot-controller \
      --replace --namespace kube-system
    ```
*   After the installation is complete, check the status of vngcloud-blockstorage-csi-driver pods:

    ```
    kubectl get pods -n kube-system | grep snapshot-controller
    ```

For example, in the image below you have successfully installed vngcloud-snapshot-controller:

```
NAME                                           READY   STATUS              RESTARTS       AGE
snapshot-controller-7fdd984f89-745tg           0/1     ContainerCreating   0              3s
snapshot-controller-7fdd984f89-k94wq           0/1     ContainerCreating   0              3s
```

#### **Create a snapshot.yaml file with the following content**

```
apiVersion: snapshot.storage.k8s.io/v1
kind: VolumeSnapshotClass
metadata:
  name: my-snapshot-storage-class  # [2] The name of the volume snapshot class, CAN be changed
driver: bs.csi.vngcloud.vn
deletionPolicy: Delete
parameters:
  force-create: "false"
---

apiVersion: snapshot.storage.k8s.io/v1
kind: VolumeSnapshot
metadata:
  name: my-snapshot-pvc  # [4] The name of the snapshot, CAN be changed
spec:
  volumeSnapshotClassName: my-snapshot-storage-class  # MUST match with [2]
  source:
    persistentVolumeClaimName: my-expansion-pvc  # MUST match with [3]
```

* Run the following command to deploy Volume Snapshot

```
kubectl apply -f snapshot.yaml
```

***

### **Check the newly created PVC and Snapshot** <a href="#kiem-tra-pvc-va-snapshot-vua-tao" id="kiem-tra-pvc-va-snapshot-vua-tao"></a>

*   After applying the file successfully, you can check the service and pvc list via:

    ```
    kubectl get sc,pvc,pod -owide
    ```



    ```
    NAME                                                       PROVISIONER          RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
    storageclass.storage.k8s.io/my-expansion-storage-class     bs.csi.vngcloud.vn   Delete          Immediate           true                   10m
    storageclass.storage.k8s.io/sc-iops-200-retain (default)   bs.csi.vngcloud.vn   Retain          Immediate           false                  2d4h

    NAME                                     STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                 AGE   VOLUMEMODE
    persistentvolumeclaim/my-expansion-pvc   Bound    pvc-14456f4a-ee9e-435d-a94f-5a2e820954e9   20Gi       RWO            my-expansion-storage-class   10m   Filesystem

    NAME                             READY   STATUS    RESTARTS   AGE   IP              NODE                                            NOMINATED NODE   READINESS GATES
    pod/nginx                        1/1     Running   0          10m   172.16.24.203   ng-3f06013a-f6a5-47ba-a51f-bc5e9c2b10a7-ecea1   <none>           <none>
    pod/nginx-app-7f45b65946-t7d7k   1/1     Running   0          94m   172.16.24.202   ng-3f06013a-f6a5-47ba-a51f-bc5e9c2b10a7-ecea1   <none>           <none>
    ```

***

### Change the IOPS parameters of the newly created Persistent Volume <a href="#thay-doi-thong-so-iops-cua-persistent-volume-vua-tao" id="thay-doi-thong-so-iops-cua-persistent-volume-vua-tao"></a>

To change the IOPS parameters of the newly created Persistent Volume, follow these steps:

**Step 1:** Run the command below to list the PVCs in your Cluster

```
kubectl get persistentvolumes
```

**Step 2:** Edit the PVC YAML file according to the command

```
kubectl edit pvc my-expansion-pvc
```

*   If you have not edited the IOPS of the Persistent Volume before, when you run the above command, add an annotation bs.csi.vngcloud.vn/volume-type: "volume-type-id" . For example, below I am changing the Persistent Volume IOPS from 200 (Volume type id = vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018) to 1000 (Volume type id = vtype-85b39362-a360-4bbb-9afa-a36a40cea748 )

    Copy

    ```
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      annotations:
        bs.csi.vngcloud.vn/volume-type: "vtype-85b39362-a360-4bbb-9afa-a36a40cea748"
        kubectl.kubernetes.io/last-applied-configuration: |
          {"apiVersion":"v1","kind":"PersistentVolumeClaim","metadata":{"annotations":{},"name":"my-expansion-pvc","namespace":"default"},"spec":{"accessModes":["ReadWriteOnce"],"resources":{"requests":{"storage":"20Gi"}},"storageClassName":"my-expansion-storage-class"}}
        pv.kubernetes.io/bind-completed: "yes"
        pv.kubernetes.io/bound-by-controller: "yes"
        volume.beta.kubernetes.io/storage-provisioner: bs.csi.vngcloud.vn
        volume.kubernetes.io/storage-provisioner: bs.csi.vngcloud.vn
      creationTimestamp: "2024-04-21T14:16:53Z"
      finalizers:
      - kubernetes.io/pvc-protection
      name: my-expansion-pvc
      namespace: default
      resourceVersion: "11041591"
      uid: 14456f4a-ee9e-435d-a94f-5a2e820954e9
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 20Gi
      storageClassName: my-expansion-storage-class
      volumeMode: Filesystem
      volumeName: pvc-14456f4a-ee9e-435d-a94f-5a2e820954e9
    status:
      accessModes:
      - ReadWriteOnce
      capacity:
        storage: 20Gi
      phase: Bound
    ```
* If you have edited the IOPS of the Persistent Volume before, when you run the above command, your yaml file will already have the annotation bs.csi.vngcloud.vn/volume-type: "volume-type-id" . Now, edit this annotation to the Volume type id with the IOPS you desire.

### Change the Disk Volume of the newly created Persistent Volume <a href="#thay-doi-disk-volume-cua-persistent-volume-vua-tao" id="thay-doi-disk-volume-cua-persistent-volume-vua-tao"></a>

To change the Disk Volume of the newly created Persistent Volume, run the following command:

For example, initially the PVC created was 20 Gi in size, now I will increase it to 30 Gi

```
kubectl patch pvc my-expansion-pvc -p '{"spec":{"resources":{"requests":{"storage":"30Gi"}}}}'
```

{% hint style="info" %}
**Attention**:

* You can only increase Disk Volume but cannot reduce Disk Volume size.
{% endhint %}

### Restore Persistent Volume from Snapshot <a href="#restore-persistent-volume-tu-snapshot" id="restore-persistent-volume-tu-snapshot"></a>

To restore Persistent Volume from Snapshot, follow these steps:

*   Create file **restore-volume.yaml** with the following content:

    Copy

    ```
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: my-restore-pvc  # The name of the PVC, CAN be changed
    spec:
      storageClassName: my-expansion-storage-class  
      dataSource:
        name: my-snapshot-pvc # MUST match with [4] from the section 5.2
        kind: VolumeSnapshot
        apiGroup: snapshot.storage.k8s.io
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 20Gi
    ```
