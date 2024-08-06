# Migration Cluster from vContainer to VKS

To migrate a Cluster from vContainer system to VKS system, follow the steps in this document.

### Prerequisites <a href="#dieu-kien-can" id="dieu-kien-can"></a>

* <mark style="color:red;">**Perform download helper bash script and grand execute permission for this file**</mark> ([ velero\_helper.sh](https://raw.githubusercontent.com/vngcloud/velero/main/velero\_helper.sh) )
* (Optional) Deploy some services to check the correctness of the migration. Suppose, at the source Cluster, I have deployed an nginx service as follows:
  * Deployment files:

```
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
      storageClassName: csi-sc-cinderplugin-nvme-5000
      resources:
        requests:
          storage: 40Gi
```



```
kubectl exec -n mynamespace -it web-0 bash
cd /usr/share/nginx/html
echo -e "<html>\n<head>\n  <title>MyVNGCloud</title>\n</head>\n<body>\n  <h1>Hello, MyVNGCloud</h1>\n</body>\n</html>" > index.html
```

* Now, when you access Node's Public IP, you will see "Hello, MyVNGCloud".

***

### Prepare target cluster (Prepare target resource) <a href="#chuan-bi-cluster-dich-prepare-target-resource" id="chuan-bi-cluster-dich-prepare-target-resource"></a>

On the VKS system, you need to initialize a Cluster according to the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/clusters) . Make sure that the destination cluster's configuration is the same as the source cluster's configuration.

{% hint style="info" %}
**Attention:**

For the migration to be successful, on the target Cluster, you need to ensure the following requirements:

* The amount of resources needed such as number of nodes, node instance configuration,...
* Node labels and node taints are the same as the old cluster.
* Corresponding or alternative Storage Class.
{% endhint %}

***

### \[Optional] Migrate private resources outside cluster <a href="#optional-migrate-resources-private-outside-cluster" id="optional-migrate-resources-private-outside-cluster"></a>

Migrating private resources outside cluster (moving private resources outside the cluster) is the process of moving private resources outside the source Cluster to a place that the destination Cluster can use. For example, you may have private resources such as images, databases, etc. Now, before starting to migrate, you need to migrate these resources yourself. For example, if you need:

* Migrate Container Images: you can migrate images to VNGCloud Container Registry through instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vcontainer-registry) .
* Migrate Databases: you can use **Relational Database Service (RDS)** and **Object Storage Service (OBS)** depending on your needs. After the migration is complete, remember to reconfigure the database for your applications on VKS Cluster.
* Migrate Storage: you can use vServer's **NFS Server** .

{% hint style="info" %}
**Attention:**

* After you migrate resources outside the Cluster, you need to ensure the target Cluster can connect to these migrated resources.
{% endhint %}

***

### Install Velero on both source and destination clusters (Install Velero tool) <a href="#cai-dat-velero-tren-ca-2-cluster-nguon-va-cluster-dich-install-velero-tool" id="cai-dat-velero-tren-ca-2-cluster-nguon-va-cluster-dich-install-velero-tool"></a>

After you have migrated private resources outside the cluster, you can use the migration tool to backup and restore the application on the source cluster and target cluster.

* Create a **vStorage Project, Container** to receive the cluster's backup data according to instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vstorage/object-storage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-project/khoi-tao-project) .
* Create an S3 key corresponding to this vStorage Project according to the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials/khoi-tao-s3-key) .

For example, I have initialized a vStorage Project, Container with the following information: Region: HCM03, Container: mycontainer, Endpoint: [https://hcm03.vstorage.vngcloud.vn](https://hcm03.vstorage.vngcloud.vn/) .

#### On both Clusters (source and target) <a href="#tren-ca-2-cluster-source-and-target" id="tren-ca-2-cluster-source-and-target"></a>

*   Create file **credentials-velero** with the following content:



    ```
    [default]
    aws_access_key_id=________________________
    aws_secret_access_key=________________________
    ```
*   Install Velero CLI:



    ```
    curl -OL https://github.com/vmware-tanzu/velero/releases/download/v1.13.2/velero-v1.13.2-linux-amd64.tar.gz
    tar -xvf velero-v1.13.2-linux-amd64.tar.gz
    cp velero-v1.13.2-linux-amd64/velero /usr/local/bin
    ```
*   Install Velero on your 2 clusters with the command:



    ```
    velero install \
        --provider aws \
        --plugins velero/velero-plugin-for-aws:v1.9.0 \
        --use-node-agent \
        --use-volume-snapshots=false \
        --secret-file ./credentials-velero \
        --bucket ________________________ \
        --backup-location-config region=hcm03,s3ForcePathStyle="true",s3Url=https://hcm03.vstorage.vngcloud.vn
    ```

***

### At the source Cluster <a href="#tai-cluster-nguon" id="tai-cluster-nguon"></a>

*   Annotate the Persistent Volumes that need to be backed up. By default, Velero will not backup volume. You can run the command below to annotate backup of all volumes.



    ```
    ./velero_helper.sh mark_volume --confirm
    ```
*   Additionally, you can mark not to backup system resources with the following command:



    ```
    ./velero_helper.sh mark_exclude --confirm
    ```

    For details, please refer [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vks/migration/gioi-han-va-han-che) .
*   You need to create 2 backups for cluster resource and namespace resource to avoid possible errors. Create backup according to the syntax:



    ```
    velero backup create vcontainer-cluster --include-namespaces "" \
      --include-cluster-resources=true \
      --wait
    ```



    ```
    velero backup create vcontainer-namespace --exclude-namespaces velero \
        --wait
    ```

***

### At the destination Cluster <a href="#tai-cluster-dich" id="tai-cluster-dich"></a>

*   Create a Storage Class mapping file between source and destination Cluster, apply this file on your destination Cluster:



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
      _______old_storage_class_______: _______new_storage_class_______  # <= Adjust here
      _______old_storage_class_______: _______new_storage_class_______  # <= Adjust here
    ```
*   Perform restore in order:



    ```
    velero restore create --item-operation-timeout 1m --from-backup vcontainer-cluster \
        --exclude-resources="MutatingWebhookConfiguration,ValidatingWebhookConfiguration"
    ```



    ```
    velero restore create --item-operation-timeout 1m --from-backup vcontainer-namespace
    ```



    ```
    velero restore create --item-operation-timeout 1m --from-backup vcontainer-cluster
    ```

***

### Update resource config <a href="#update-resource-config" id="update-resource-config"></a>

*   For vContainer clusters that use nginx-ingress-controller with Network Load Balancer attached, when migrating the cluster via VKS, you need to change Service Nginx from type Node Port to type Load Balancer via the command:

    Copy

    ```
    kubectl patch service -n kube-system vcontainer-ingress-nginx-controller \
          -p '{"spec": {"type": "LoadBalancer"}}'
    ```
