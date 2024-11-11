# Start Replication

To start the replication process, you need to add the primary server to be replicated to SDR. See instructions for adding the primary server to SDR [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/backup-center/disaster-recovery-center-drc/server-disaster-recovery-sdr/quan-ly-sdr/them-may-chu-attach-a-server) .

After successfully adding the server, follow the instructions below to start the data replication process.

## Start Replication <a href="#start-replication" id="start-replication"></a>

1. Select the previously added primary server from the list here:
2. Click the **"Start Replication"** button to start configuring the backup server parameters, an interface window will appear allowing you to configure the following information:
   1. **Basic Information**
      * **Shadow Server Name:** Set an easily recognizable name for the shadow server.
      * **Region:** If you want to change the region where the backup server is located, you can select it again here.
      * **Interval:** Select the frequency of data replication. You can choose from 1 hour to 12 hours, depending on the importance and frequency of data changes on the primary server.
   2. **Network Settings**
      * Configure **VPC** , **Subnet and specify private IP** address and Floating IP (optional) for backup server.
      * **Select Security Group** configuration for the backup server: This Security group must be in the list of server groups in the Region selected in the Basic Information section.
   3. **Volume Setting**
      * **Default:** The system will automatically upload the same number of volumes in terms of drive type (SSD/NVMe), IOPS (Input/Output Operations Per Second), and capacity as the primary server. This helps ensure that the backup server has the same data processing capabilities as the primary server.
      * **Customization:** You are allowed to change the drive type and IOPS to suit your needs. For example, if you need higher performance for your backup server, you can choose the NVMe drive type or increase the IOPS.
        * **Shadow Server volume type:** Select the disk type for the backup server (SSD or NVMe).
        * **Shadow Server IOPS:** Select the IOPS level for the backup server. The higher the IOPS, the faster the disk read/write performance.
        * **Note:** If the region where the standby server is located does not support the same disk type and IOPS configuration as the region where the primary server is located, the system will automatically adjust and load the default information for that region. This ensures that you can still create a standby server, although there may be performance differences compared to the primary server.
   4. **Instance Type Configuration:** You need to choose a flavor (server type) that suits the needs of the backup server. This includes considering factors such as the number of CPUs, RAM capacity, and storage capacity. You can completely **change the flavor** of the backup server after it has been successfully initialized. This allows you to flexibly adjust the server configuration to better meet actual usage needs, or optimize costs.
   5. **Other Setting** :
      * You can optionally configure a placement group for the backup server. Placement group is a feature that allows you to group servers together to ensure they are located on the same physical infrastructure, helping to reduce network latency and increase data transfer performance between servers.
      * **Note:** This group must be in the same region as the backup server. This ensures that the servers in the placement group are physically close to each other, optimizing data transfer performance.
3. Click the **"Start Replication"** button to begin the data replication process.

**Notes when creating backup servers**

* **Default state:** The backup server is created in **shutdown** state by default . This is for data replication purposes and to help you save costs. In shutdown state, you will **not be charged** for using the backup server.
* **Charged on startup:** However, if you **start** the backup server, you will start being charged for server usage according to the selected configuration.
* **Impact on replication:** Note that when you start the backup server, the data replication process on that server will **fail** . This is because the backup server needs to be in a powered off state so that the system can perform replication safely and efficiently.

## Full Replication <a href="#full-replication" id="full-replication"></a>

After clicking " **Start Replication** " the system will perform the following processes:

1. **Initialize backup server:** The system will initialize the backup server based on the configuration you selected to start the replication process.
2. **Start Full Replication:** The system will start the process of copying all data (Full Replication) from the primary server to the backup server.
3. **Costs:** During this process, you will start to incur costs for:
   * **Backup Server:** Includes the cost of the server and the volumes attached to it.
   * **Snapshot storage:** The cost of storing snapshot copies of data to serve the replication process.
   * See more about fee calculation [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/backup-center/disaster-recovery-center-drc/server-disaster-recovery-sdr/cach-tinh-phi)
4. **Pairing Status:**
   * **Replicating:** If the data replication process is successful, the pairing status will change to "Replicating". At this point, you can view the recovery point that was just created.
   * **Error:** If the status is "Error", it means that the "Start Replication" process has not started or has encountered an error. You can:
     * **View error details:** Access the server details to see what the specific error is. From there, you can try to troubleshoot the issue yourself based on the error information.
     * **Contact Support:** If you cannot resolve the issue yourself, please contact our support team for assistance via the following channels:
       * Email [**support@vngcloud.vn**](mailto:support@vngcloud.vn) or hotline **19001549 – Ext 3.**
       * Open ticket: [https://vngcloud.vn/en/web/guest/contact](https://apc01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fu12870758.ct.sendgrid.net%2Fls%2Fclick%3Fupn%3D6Th82stgZiRII4JWBZ2k-2F8jp0RwIXS6fxA7KQMXjUq8DSCsrmL59yXstoJFgaU1dGY-2FSWg-2FK9UdGxb9Lh9dNFA-3D-3DpvNZ\_Ym-2Fxt4z9Amb7foJoUGq7k-2FFaxzUNhQVDcUTybZdrS2NXAbbCaEQkSCrQOhYjTHUSbv6080NfkWdCEMWKJJF2zpfOBUaPuOIa3OzTC0yp1D9JlA3uof8O-2BtBLR8V2gs8RQIrzb7xDzuI-2FW-2BVnmHahaTWks-2FX1rqpdHNVHwVyZ6vhj-2BZLRAIyEc2XrBxbfG0QrF7-2FsBJLgoViI1e7tTyjc8Q-3D-3D\&data=05%7C01%7Ctult4%40vng.com.vn%7C7e33555fd46c4091057908db827ef130%7C7c112a6e10e24e09afc42e37bc60d821%7C0%7C0%7C638247253964298461%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C3000%7C%7C%7C\&sdata=VmVhSabKwqQW2lPslozGS3cQzp0jF4ShJuofnhGp%2Fzs%3D\&reserved=0)

**Important Note:**

* **Costs:** Make sure you understand the costs associated with using backup servers and storing snapshots before you begin the replication process.
* **Status monitoring:** Regularly check the replication status to ensure the process is running smoothly. If there is an error, handle it promptly to avoid affecting the system's recovery ability.
