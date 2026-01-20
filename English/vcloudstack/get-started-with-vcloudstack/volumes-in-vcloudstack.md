# Volumes in vCloudStack

### Overview <a href="#tong-quan" id="tong-quan"></a>

Volume is an object in a virtual environment that is responsible for providing block storage to servers with high availability and performance. You can use Volume to store data and applications, or you can attach one or more Volumes to a server while creating the server or later while the server is running, and you can also remove it from the server and attach it to another server.

#### **Basic information** <a href="#volume-thongtincoban" id="volume-thongtincoban"></a>

When using volume, the following information should be noted:

* Maximum capacity for a volume is 1TB
* A volume without the multi-attach attribute can only be attached to one virtual machine at any given time. A volume with the multi-attach attribute can be attached to multiple virtual machines simultaneously. The multi-attach attribute can be selected at volume creation time.
* Boot volume cannot be removed from virtual server
* Data volumes can be attached to or removed from different virtual servers.
* You can select the QoS level for the volume according to the Volume Type information to limit bandwidth and IOPS.
* You can choose the encryption function when creating a volume to protect data. GreenNode supports aes-xts-plan64 encryption (128 bits)

***

### Create Volume <a href="#tao-volume" id="tao-volume"></a>

There are two types of volumes: boot volumes and data volumes. Boot volumes can be created simultaneously during virtual machine creation. Data volumes can be created during server creation or as a separate operation from the volume management page.

**Step 1:** Access the vServer interface with Region as vCloudstack, go to the Volume page.

**Step 2:** Create a data volume, providing necessary information such as name, size, IOPS, multi-attach options and encryption.

**Step 3:** You can check the parameters on the right, then press **Create Volume.**

***

### Attach Volume to VM Instance <a href="#volume-ganvolumevaovminstance" id="volume-ganvolumevaovminstance"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack, go to the Volume page.

**Step 2** : Select the data volume to attach, go to the action menu on the right, select **Attach.**

**Step 3:** Select the virtual server to mount the volume, after mounting you need to operate from within the virtual server such as creating partition, formatting and mounting.

***

### Unmount volume from VM Instance <a href="#volume-thaogovolumekhoivminstance" id="volume-thaogovolumekhoivminstance"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack, go to the Volume page.

**Step 2:** Select the data volume to remove, go to the action menu on the right, select **Detach.**

**Step 3** : Select the virtual server to remove the volume.

***

### Delete volume <a href="#volume-xoavolume" id="volume-xoavolume"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack, go to the Volume page.

**Step 2:** Select the data volume to delete, go to the action menu on the right, select **Delete**

{% hint style="info" %}
**Note:** Only volumes in Available status can be deleted.
{% endhint %}
