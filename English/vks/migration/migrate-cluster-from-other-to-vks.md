# Migrate Cluster from another platform to VKS

Để migrate một Cluster từ hệ thống Cloud Provider hoặc On-premise tới hệ thống VKS, hãy thực hiện theo các bước theo tài liệu này.

## Pre-required

* Do download helper bash script and grand execute permission for this file ([velero\_helper.sh](https://raw.githubusercontent.com/vngcloud/velero/main/velero\_helper.sh))
* (Optional) Deploy some services to test the correctness of the migration. Suppose, in the source Cluster, I have deployed an nginx service as follows:
*   ```yaml
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
              storage: 40Gi
    ```

    ```bash
    kubectl exec -n mynamespace -it web-0 bash
    cd /usr/share/nginx/html
    echo -e "<html>\n<head>\n  <title>MyVNGCloud</title>\n</head>\n<body>\n  <h1>Hello, MyVNGCloud</h1>\n</body>\n</html>" > index.html
    ```
* Lúc này, khi bạn truy cập vào Public IP của Node, bạn sẽ thấy "Hello, MyVNGCloud".

***

## Prepare target resource

On the VKS system, you need to initialize a Cluster according to the instructions here. Make sure that the configuration of the destination cluster is the same as the configuration of the source cluster.

{% hint style="info" %}
**Note:**

For successful migration, on the destination Cluster, you need to ensure the following requirements:&#x20;

* Necessary resources such as number of nodes, node instance configuration,...&#x20;
* Node labels and node taints are the same as the old cluster.&#x20;
* Corresponding or replaced Storage Class.
{% endhint %}

***

## \[Optional] Migrate resources private outside cluster

Migrating private resources outside cluster is the process of moving private resources outside the source cluster to a place where the destination cluster can use them. For example, you may have private resources such as images, databases, etc. Now, before starting the migration, you need to migrate these resources yourself. For example, if you need to:

* Migrate Container Images: you can migrate images to VNGCloud Container Registry via the instructions here.&#x20;
* Migrate Databases: you can use Relational Database Service (RDS) and Object Storage Service (OBS) depending on your usage needs. After the migration is complete, remember to reconfigure the database for your applications on VKS Cluster.&#x20;
* Migrate Storage: you can use NFS Server of vServer.

{% hint style="info" %}
**Note:**

* After you migrate resources outside the Cluster, you need to make sure the destination Cluster can connect to these migrated resources.
{% endhint %}

***

## Install Velero tool

For example, I have created a vStorage Project with the following Container information:

* **Region:** HCM03
* **Container:** mycontainer
* **Endpoint:** https://hcm03.vstorage.vngcloud.vn

Initialize the corresponding S3 key for this vStorage Project as instructed [here](https://hcm03.vstorage.vngcloud.vn).

Create a **vStorage Project, Container** as the destination for backup data of the cluster as instructed [here](https://hcm03.vstorage.vngcloud.vn).

After migrating private resources outside the cluster, you can use migration tools to back up and restore applications on both the source and destination clusters.

### Trên cả 2 Cluster (source and target)

*   Tạo file **credentials-velero** với nội dung sau:

    ```yaml
    [default]
    aws_access_key_id=________________________
    aws_secret_access_key=________________________
    ```
*   Cài đặt Velero CLI:

    ```bash
    curl -OL https://github.com/vmware-tanzu/velero/releases/download/v1.13.2/velero-v1.13.2-linux-amd64.tar.gz
    tar -xvf velero-v1.13.2-linux-amd64.tar.gz
    cp velero-v1.13.2-linux-amd64/velero /usr/local/bin
    ```
*   Cài đặt Velero trên 2 cụm của bạn theo lệnh:

    ```bash
    velero install \
        --provider aws \
        --plugins velero/velero-plugin-for-aws:v1.9.0 \
        --use-node-agent \
        --use-volume-snapshots=false \
        --secret-file ./credentials-velero \
        --bucket ______________________________ \
        --backup-location-config region=hcm03,s3ForcePathStyle="true",s3Url=https://hcm03.vstorage.vngcloud.vn
    ```

***

## Cluster on Amazon Elastic Kubernetes Service (EKS)

### On Source Cluster

*   Annotate các Persistent Volume cần backup. Mặc định velero sẽ không backup volume. Bạn có thể chạy lệnh dưới để annotate backup tất cả volume.

    ```yaml
    ./velero_helper.sh mark_volume -c
    ```
*   Ngoài ra, bạn có thể đánh dấu không backup các resource của system bằng lệnh sau:

    ```yaml
    ./velero_helper.sh mark_exclude -c
    ```
*   Thực hiện backup theo cú pháp:

    ```bash
    velero backup create eks-cluster --include-namespaces "" \
      --include-cluster-resources=true \
      --wait
    ```

    ```bash
    velero backup create eks-namespace --exclude-namespaces velero \
        --wait
    ```

{% hint style="info" %}
**Note:**

* Bạn phải tạo 2 phiên bản backup cho Cluster Resource và Namespace Resource.
{% endhint %}

***

### On Destination Cluster

*   Tạo file mapping Storage Class giữa Cluster nguồn và đích:

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
      _______old_storage_class_______: _______new_storage_class_______  # <= Adjust here
      _______old_storage_class_______: _______new_storage_class_______  # <= Adjust here
    ```
*   Thực hiện restore theo lệnh:

    ```bash
    velero restore create --item-operation-timeout 1m --from-backup eks-cluster \
        --exclude-resources="MutatingWebhookConfiguration,ValidatingWebhookConfiguration"
    ```

    ```bash
    velero restore create --item-operation-timeout 1m --from-backup eks-namespace
    ```

    ```bash
    velero restore create --item-operation-timeout 1m --from-backup eks-cluster
    ```

***

## Cluster on Google Kubernetes Engine (GKE)

### On Source Cluster

*   Annotate các Persistent Volume và lable resource cần loại trừ khỏi bản backup

    ```yaml
    ./velero_helper.sh mark_volume -c
    ```
*   Ngoài ra, bạn có thể đánh dấu không backup các resource của system bằng lệnh sau:

    ```yaml
    ./velero_helper.sh mark_exclude -c
    ```
*   Thực hiện backup theo cú pháp:

    ```bash
    velero backup create gke-cluster --include-namespaces "" \
      --include-cluster-resources=true \
      --wait
    ```

    ```bash
    velero backup create gke-namespace --exclude-namespaces velero \
        --wait
    ```

{% hint style="info" %}
**Chú ý:**

* Bạn phải tạo 2 phiên bản backup cho Cluster Resource và Namespace Resource.
{% endhint %}

***

### On Destination Cluster

*   Tạo file mapping Storage Class giữa Cluster nguồn và đích:

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
      _______old_storage_class_______: _______new_storage_class_______  # <= Adjust here
      _______old_storage_class_______: _______new_storage_class_______  # <= Adjust here
    ```
*   Thực hiện restore theo lệnh:

    ```bash
    velero restore create --item-operation-timeout 1m --from-backup gke-cluster \
        --exclude-resources="MutatingWebhookConfiguration,ValidatingWebhookConfiguration"
    ```

    ```bash
    velero restore create --item-operation-timeout 1m --from-backup gke-namespace
    ```

    ```bash
    velero restore create --item-operation-timeout 1m --from-backup gke-cluster
    ```

{% hint style="info" %}
**Note:**

* Google Kubernetes Engine (GKE) does not allow deploying daemonset on all nodes. However, Velero only needs to deploy daemonset on PV-mounted nodes. The solution to this problem is that you can adjust the taint and toleration of daemonset to deploy it only on PV-mounted nodes.&#x20;
* You can change the default resource requirements cpu:500m and mem:512M during the installation step or adjust it when deploying yaml.
{% endhint %}
