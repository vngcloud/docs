# Create a Cluster via POC

POC resources are designed to help users experience GreenNode services in the best way possible.

Conditions for using POC resources:

* **Target**: Prepaid users who have been granted a POC wallet
* **Funding source:** [**POC Wallet**](https://docs.vngcloud.vn/vng-cloud-document/vn/quan-ly-hoa-don-chi-phi-and-tai-nguyen-tren-vng-cloud/trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/thanh-toan/thanh-toan-tai-nguyen-poc)
* **Resources:** All resources eligible for POC
* **Usage period:** Depends on the duration of the granted POC wallet.

***

### Prerequisites <a href="#khoitaomotpublicclustervoipublicnodegroup-dieukiencan" id="khoitaomotpublicclustervoipublicnodegroup-dieukiencan"></a>

To initialize a **Cluster** and **Deploy** a **Workload**, you need:

* At least 1 **VPC** and 1 **Subnet** in **ACTIVE** state. If you do not have a VPC or Subnet yet, please create one following the instructions [here.](../../vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc/)
* At least 1 **SSH** key in **ACTIVE** state. If you do not have any SSH key, please create one following the instructions [here.](../../vserver/compute-hcm03-1a/security/ssh-key-bo-khoa.md)
* Installed and configured **kubectl** on your device. Please refer [here](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/) if you are not sure how to install and use kubectl. Additionally, you should not use a kubectl version that is too old; we recommend using a kubectl version that differs by no more than one version from the cluster version.

***

### Create Cluster <a href="#khoitaomotpublicclustervoipublicnodegroup-khoitaocluster" id="khoitaomotpublicclustervoipublicnodegroup-khoitaocluster"></a>

A **Cluster in Kubernetes** is a collection of one or more virtual machines (VMs) connected together to run containerized applications. A Cluster provides a unified environment for deploying, managing, and operating containers at scale.

To create a Cluster, follow the steps below:

**Step 1:** Go to [https://vks.console.vngcloud.vn/overview](https://vks.console.vngcloud.vn/overview)

**Step 2:** On the **Overview** screen, select **Activate.**

**Step 3:** Wait until we successfully initialize your VKS account. After successful activation, select **Create a Cluster**

**Step 4:** On the Cluster creation screen, we have pre-configured information for the Cluster and a **Default Node Group**. You can keep these default values or adjust the desired parameters for your Cluster and Node Group at Cluster Configuration, Default Node Group Configuration, Plugin. **By default, we will create a Public Cluster with Public Node Group for you.**

**Step 5:** Select **POC** and then select **Create Kubernetes cluster.** Please wait a few minutes for us to create your Cluster. The Cluster status at this point will be **Creating**.

**Step 6:** When the **Cluster** status is **Active**, you can view Cluster information and Node Group information by selecting the Cluster Name in the **Name** column.

{% hint style="info" %}
**Note:**

* When you create a Cluster and choose to use the POC wallet, we automatically create the Control Plane, Node, Volume, and Private Service Endpoint (if you choose to use it) through the POC wallet. For other resources such as:
  * **PVC:** when creating via yaml, please add the parameter `isPOC: "true"` to the yaml file. See the example below.
  * **LoadBalancer:** when creating via yaml, please add the annotation `vks.vngcloud.vn/is-poc: "true"` to the yaml file. See the example below.
* Since **Load Balancer** and **PVC** resources are managed through YAML, after Stop POC, if your YAML file still has the parameter `isPOC : true or is-poc : true`, in case you delete the Load Balancer from vLB Portal and remove the `load-balancer-id` parameter in yaml, the system will automatically recreate these resources through the POC wallet. To create Load Balancer and PVC with real money, please change the isPOC parameter to false. (`isPOC : false or is-poc : false`). We recommend that you adjust this parameter before performing Stop POC for your Cluster.
{% endhint %}

***

### Connect and check Cluster information <a href="#khoitaomotpublicclustervoipublicnodegroup-ketnoivakiemtrathongtinclustervuatao" id="khoitaomotpublicclustervoipublicnodegroup-ketnoivakiemtrathongtinclustervuatao"></a>

After the Cluster is successfully created, you can connect and check the Cluster information by following these steps:

**Step 1:** Go to [https://vks.console.vngcloud.vn/k8s-cluster](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** The Cluster list is displayed, select the **Download** icon and select **Download Config File** to download the kubeconfig file. This file will give you full access to your Cluster.

**Step 3**: Rename this file to config and save it to the **\~/.kube/config** folder

**Step 4:** Check the Cluster by running:

* Run the following command to check **node**

```bash
kubectl get nodes
```

* If the result returns as below, your Cluster was successfully created with 3 nodes.

```bash
NAME                                            STATUS     ROLES    AGE   VERSION
ng-0e10592c-e70e-404d-a4e8-5e3b80f805e4-834b7   Ready      <none>   50m   v1.28.8
ng-0e10592c-e70e-404d-a4e8-5e3b80f805e4-cf652   Ready      <none>   23m   v1.28.8
ng-0f4ed631-1252-49f7-8dfc-386fa0b2d29b-a8ef0   Ready      <none>   28m   v1.28.8
```

***

### Deploy Workload and expose service through vLB Layer 4 or vLB Layer 7 <a href="#exposemotservicethongquavlblayer4-deploymotworkload" id="exposemotservicethongquavlblayer4-deploymotworkload"></a>

Below are instructions for deploying 2 workloads and exposing them through Load Balancer Layer 4 and Load Balancer Layer 7 on Kubernetes.

**Step 1**: **Create Deployment, Service for Nginx app.**

* Create file **nginx-service.yaml** with the following content:

<pre class="language-bash"><code class="lang-bash">apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: default
spec:
  replicas: 2
  selector:
    matchLabels:
      unique-label: app1
  template:
    metadata:
      labels:
        unique-label: app1
        same-label: vngcloud
    spec:
      containers:
        - name: nginx-deployment
          image: nginx
          ports:
            - containerPort: 80
              name: http
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: python-http-server
spec:
  replicas: 2
  selector:
    matchLabels:
      app: python-http-server
  template:
    metadata:
      labels:
        app: python-http-server
        same-label: vngcloud
    spec:
      containers:
      - name: python-http-server
        image: python:3.9-slim
        command: ["python", "-m", "http.server", "8080"]
        ports:
        - containerPort: 8080
          name: http
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: default
  annotations:
<strong>    vks.vngcloud.vn/is-poc: "true"      # Parameter specifying that the Load Balancer will be created using the POC wallet
</strong>spec:
  ports:
    - port: 80
      targetPort: http
      protocol: TCP
      name: http-server
  selector:
    same-label: vngcloud
  type: LoadBalancer

---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: webapp-02
  namespace: default
  annotations:
    vks.vngcloud.vn/is-poc: "true"      # Parameter specifying that the Load Balancer will be created using the POC wallet
spec:
  ingressClassName: vngcloud
  defaultBackend:
    service:
      name: nginx-service
      port:
        name: http-server
</code></pre>

* Deploy this Service by running:

```bash
kubectl apply -f nginx-service.yaml
```

* Next, you can check the Deployment by running:

```bash
kubectl get svc,deploy,pod -owide
```

***

### **Create Persistent Volume**

* Create file **persistent-volume.yaml** with the following content:

```bash
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: my-expansion-storage-class                    # [1] The StorageClass name, CAN be changed
provisioner: bs.csi.vngcloud.vn                       # The VNG-CLOUD CSI driver name
parameters:
  type: vtype-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx    # The volume type UUID
  isPOC: "true"                                       # Parameter specifying that the Volume will be created using the POC wallet
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

* Run the following command to deploy:

```bash
kubectl apply -f persistent-volume.yaml
```

***

### **Create Snapshot**

For **Snapshot** resources, you cannot specify snapshot to use the POC wallet from VKS. To create a Snapshot via the POC wallet, on **vServer Portal**, please select **Activate Snapshot**, then on the **Checkout** screen, please select the **POC** wallet. At this point, **all your snapshot resources will be created via the POC wallet**. Therefore, stopping POC needs to be done through **vConsole** or **vServer Portal**. See the image below for reference.

<figure><img src="../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

**Install GreenNode Snapshot Controller**

* Install Helm version 3.0 or higher. Refer to [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/) for installation instructions.
* Add this repo to your cluster via:

```bash
helm repo add vks-helm-charts https://vngcloud.github.io/vks-helm-charts
helm repo update
```

* Then run:

```bash
helm install vngcloud-snapshot-controller vks-helm-charts/vngcloud-snapshot-controller \
  --replace --namespace kube-system
```

* After the installation is complete, check the status of vngcloud-blockstorage-csi-driver pods:

```bash
kubectl get pods -n kube-system
```

For example, the output below means you have successfully installed the snapshot-controller:

```bash
NAME                                           READY   STATUS              RESTARTS       AGE

snapshot-controller-7fdd984f89-745tg           0/1     ContainerCreating   0              3s
snapshot-controller-7fdd984f89-k94wq           0/1     ContainerCreating   0              3s
```

**Create file snapshot.yaml with the following content:**

```bash
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

* Run the following command to deploy:

```bash
kubectl apply -f snapshot.yaml
```

***

### **Check PVC and Snapshot**

* After successfully applying the files, you can check the list of services and PVC via:

```bash
kubectl get sc,pvc,pod -owide
```

```bash
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

### Change IOPS of a Persistent Volume

To change the IOPS of a Persistent Volume, follow these steps:

**Step 1:** Run the command below to list PVCs in your Cluster

```bash
kubectl get persistentvolumes
```

**Step 2:** Edit the PVC YAML file

```bash
kubectl edit pvc my-expansion-pvc
```

* If you have not changed the IOPS of the Persistent Volume before, add the annotation `bs.csi.vngcloud.vn/volume-type: "volume-type-id"`. For example: below I am changing the IOPS from 200 (Volume type id = vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018) to 1000 (Volume type id = vtype-85b39362-a360-4bbb-9afa-a36a40cea748)

```bash
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

* If you have previously changed the IOPS, the yaml file will already have the annotation `bs.csi.vngcloud.vn/volume-type: "volume-type-id"`. In this case, edit the annotation to the Volume type ID with the desired IOPS.

### Change Disk Volume of a Persistent Volume

To change the Disk Volume size, run the following command:

For example: initially the PVC was created with 20 Gi, now I will increase it to 30Gi

```bash
kubectl patch pvc my-expansion-pvc -p '{"spec":{"resources":{"requests":{"storage":"30Gi"}}}}'
```

{% hint style="info" %}
**Note:**

* You can only increase the Disk Volume size. You cannot decrease it.
{% endhint %}

### Restore Persistent Volume from Snapshot

To restore a Persistent Volume from a Snapshot, follow these steps:

* Create file **restore-volume.yaml** with the following content:

```bash
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

After experiencing VKS, if you want to convert these POC resources to real resources, please follow the instructions [here](https://docs.vngcloud.vn/vng-cloud-document/vn/vks/clusters/stop-poc).
