# Physical Infrastructure Monitoring

### Overview <a href="#tong-quan" id="tong-quan"></a>

vCloudstack service is a service that deploys infrastructure and runs VNG Cloud services on-site, so monitoring the operating status of the entire physical infrastructure is considered important. vCloudStack allows users to experience controlling the operating status of the system in the Portal Admin Site interface. All information will be transparent and clear, helping administrators easily grasp the status of all physical devices so that they can propose a plan to upgrade or maintain the system in a timely manner.

You can refer to the infrastructure control information described below.

***

### Compute Information <a href="#thong-tin-compute" id="thong-tin-compute"></a>

The Compute interface allows administrators to monitor parameters about RAM and CPU usage of the virtualized infrastructure.

To access the Compute screen, go to vCloudStack Admin Site and select Compute in the control bar to be navigated to the Compute screen.

Detailed parameters displayed in the interface screen include:

* **Host:** Host Name;
* **Status:** Host status;
* **vCPUs:** Number of virtualized CPUs;
* **Ratio:** Virtualization ratio;
* **Running VMs:** number of running VMs;
* **vCPUs Used :** Number of CPUs used to allocate for VM use;
* **CPU Usage:** Highest CPU index in the last 30 minutes;
* **Free RAM (MB):** Free RAM capacity (not in use)
* **Memory Usage:** Amount of RAM used
* **Host IP:** Host IP address
* **Processor Version:** CPU version
* **Aggegate name:** Host attribute group name

***

### Storage Information <a href="#thong-tin-storage" id="thong-tin-storage"></a>

The screen displays Storage information, allowing administrators to monitor the usage status of all Clusters that are storing data.

To access the Storage screen, go to vCloudStack Admin Site and select Storage in the control bar to be navigated to the Storage screen.

The information displayed for tracking includes:

* **Cluster:** Name of the Cluster;
* **Pool:** Pool Name;
* **Images:** Total number of Images;
* **Total Cloud:** Total storage capacity on Cloud;
* **Used Cloud:** Used storage capacity in units of capacity;
* **Used Cloud (%):** Used storage capacity in %;
* **Avg volume size:** Average Volume size;
* **Free Cloud** : Free Cloud storage capacity calculated by capacity unit;
* **Free Cloud (%):** Free Cloud storage capacity in %;
* **Last report:** Last update;
* **Site name:** Site name;
* **Site code:** This site's identifier;
* **Location:** Location of this Cluster
* **Data center:** Name of the data center of this Cluster.

***

### Backup information <a href="#thong-tin-backup" id="thong-tin-backup"></a>

The screen displays Data Backup information, allowing administrators to monitor the backup status of users who have performed backups stored on vStorage.

To access the Backup screen, go to vCloudStack Admin Site and select Backup in the control bar to be directed to the Backup screen.

Backup information on vStorage displayed for monitoring includes:

* **General information:**
  * **Users:** Number of Users holding the backup;
  * **Total Backup Size:** Total size of backups (volumes in the server);
  * **Server Backups:** Total Server Backups;
  * **Volume Backups:** Total Volume Backups
* **Special information:**
  * **Total Project:** Total number of projects backed up in vStorage;
  * **Total Project Size:** Total backup size across all projects;
  * **Protected Volume:** Number of volumes being backed up according to policy;
  * **Protected Server:** Number of Servers being backed up according to policy;

### Network Information <a href="#thong-tin-network" id="thong-tin-network"></a>

The Network interface allows administrators to keep track of the Networks that have been created and who is using them when creating virtual servers.

To access the Network screen, go to vCloudStack Admin Site and select Network in the control bar to be navigated to the Network screen.

Detailed parameters displayed in the interface screen include:

* **Name** : The name of the network to identify when using
* **Status** : Network information status is ready for user use
* **ID:** Network Identifier
* **Network type:** Subnet IP address and gateway IP address allocation (eg: vlan, vxlan…);
* **Segment ID** : ID code based on the type of network configured;
* **Physical Network:** Physical Network information (eg: br0, vlan1, external\_network);
* **Share type/Owner:** Share information for all users (All) or only for Owner use (Private); Displays the email of the network's Owner user.

To initialize Network, you can refer to [Network Configuration](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcloudstack/bat-dau-voi-vcloudstack/cau-hinh-network) section .
