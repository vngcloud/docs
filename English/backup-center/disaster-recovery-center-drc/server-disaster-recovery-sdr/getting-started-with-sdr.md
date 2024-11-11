# Getting Started with SDR

Server Disaster Recovery (SDR) is an important solution to ensure the continuity of your business in case of unexpected incidents. Below is a detailed guide to get you started using the Server DR feature on VNG Cloud, going through the main features and how they work.

## **1. Access VNG Cloud Console:** <a href="#id-1.-truy-cap-vng-cloud-console" id="id-1.-truy-cap-vng-cloud-console"></a>

* Access the Server Disaster Recovery dashboard here:
* You will be redirected to the VNG Cloud account login page. See detailed instructions [on how to log in to VNG Cloud](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/identity-and-access-management-iam/cac-loai-dinh-danh-iam/tai-khoan-user-accounts/cach-dang-nhap-vao-vng-cloud) with IAM User account and Root User account

## **2. Enable Snapshot service** <a href="#id-2.-kich-hoat-dich-vu-snapshot" id="id-2.-kich-hoat-dich-vu-snapshot"></a>

To use the Server Disaster Recovery (SDR) service effectively, users need to enable the Snapshot service in the Regions where the primary and backup servers are located. Snapshot is an important feature that allows creating quick backups of data on disk, helping to ensure data recovery in case of an incident.

**Auto-Activate:**

If you have not enabled the Snapshot service, SDR will automatically enable it for you to ensure you have full access to the DR service features. This simplifies the installation and configuration process, while ensuring the continuity and security of your data.

**Note:** You can check the activation status of the Snapshot service in the Snapshot service management section of the vServer interface.

## **3. Add Server:** <a href="#id-3.-them-may-chu-attach-server" id="id-3.-them-may-chu-attach-server"></a>

* In the Server Recovery Center console, click the **"Attach a Server"** button .
* Select the Main Server you want to protect from the list of available servers.
* Configure information for the Shadow Server:
  * **Region:** Select the geographic region where you want the backup server to be located. It is best to select a different region than the primary server to increase availability in case of regional failure.
  * **VPC (Virtual Private Cloud):** Select the VPC you want the backup server to belong to.
  * **Subnet:** Select the specific subnet in the selected VPC to place the backup server.
* Click the "Attach" button to complete the server addition process.

## **4. Start Replication:** <a href="#id-4.-bat-dau-sao-chep-start-replication" id="id-4.-bat-dau-sao-chep-start-replication"></a>

* After successfully adding the server, select it from the list.
* Click the **"Start Replication"** button to start the process of copying data from the primary server to the backup server.
* Configure copy parameters:
  * **Shadow Server Name:** Set an easily recognizable name for the shadow server.
  * **Region:** If you want to change the region where the backup server is located, you can select it again here.
  * **Interval:** Select the frequency of data replication. You can choose from 1 hour to 12 hours, depending on the importance and frequency of data changes on the primary server.
  * **Network Settings:** Configure VPC, Subnet and IP address (optional) for the backup server.
* Click the **"Start Replication"** button to begin the data replication process.

## **5. Monitoring and Management:** <a href="#id-5.-giam-sat-va-quan-ly" id="id-5.-giam-sat-va-quan-ly"></a>

* Once replication begins, you can monitor the replication status and related information on the Server Disaster Recovery dashboard.
* You can also do other things like:
  * **Stop Replication:** Pause the data replication process.
  * **Restart Replication:** Restart the replication process from the beginning.
  * **Resume Replication:** Resume the replication process after stopping it.
  * **Test Failover:** Simulates the failover to a backup server to test system availability.
  * **Failover:** Perform a failover to a backup server in case the primary server fails.

## **6. Take Advantage of Advanced Features:** <a href="#id-6.-tan-dung-cac-tinh-nang-nang-cao" id="id-6.-tan-dung-cac-tinh-nang-nang-cao"></a>

* **Cross-region DR:** If you want to increase resilience against large-scale incidents, consider using cross-region DR to back up and restore data across different regions.
* **Planned DR Actions:** Plan and automate DR actions to ensure recovery happens quickly and accurately when needed.
* **Recovery Priority:** Ensure the most critical systems are restored first by customizing the priority order for primary servers.

**Note:**

* Please make sure you have read and understood VNG Cloud's Disaster Recovery service policies and terms of use.
* During use, if you have any questions or need support, you can contact VNG Cloud's technical support team.

Refer to more detailed instructions on Server Disaster Recovery features at:

* [Management (SDR)](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/backup-center/disaster-recovery-center-drc/server-disaster-recovery-sdr/quan-ly-sdr)
* [Pricing](../../cloud-backup/pricing.md)
