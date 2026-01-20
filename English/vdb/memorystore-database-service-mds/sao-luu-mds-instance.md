# Backup MDS Instance

The Backup management interface provides an overview of all existing backups and detailed information for each one. You can access the Backup management interface here: https://vdb.console.vngcloud.vn/memorystore/backup. You can create new Manual Backups, Restore (restore a new DB Instance based on a backup), or Delete (delete a backup). Refer to the following instructions for backup management features:

**A. On-Demand Backup (Manual Backup)**

When you need to create a backup, access the GreenNode service and go to the backup management screen. This screen will list all backups (manual & automatic) of all DB Instances in your account.

**Method 1:** Click the "Create Backup" button. On the Create Backup screen, select the following information:

* **Backup Name:** Set a name for this backup.
* **Database Instance Name:** Choose the DB Instance you want to back up.
* **Backup Type:** For MemoryStore, you have the option to perform a Full Backup.

After ensuring all information is correct, click "Create."

If the system successfully receives the request, a backup will appear with the status "NEW." When created successfully, the backup will change to the status "COMPLETED."

**Method 2:** In addition to the Backup management screen, you can also create a Manual Backup directly from the Database management screen.

1. Click on a DB Instance you want to back up, and you will be taken to the DB Instance details page.
2. Go to the "Backup" tab and scroll down to the "Backup list." This will list all backups (manual & automatic) corresponding to this DB Instance. You can click "Create Backup" to create a Manual Backup right here.
3. The next steps are the same as the instructions in Method 1.

**B. Automatic Daily Backup**

vDBaaS supports automatic daily backups at a time you specify.

To check if a DB Instance has this feature configured, do the following:

1. Click on a DB Instance you want to check, and you will be taken to the DB Instance details page.
2. Then, select the "Backup" tab and find the "Backup Information" section. If "Automatic backup" is "Enabled," it means you have configured automatic daily backups for this DB Instance at the "Backup Time" specified.

To configure this feature, you have two options:

**Method 1:** Configure it during DB Instance creation. For this option, please refer to the instructions on Creating a DB Instance in the MDS Instance Creation Guide.

**Method 2:** Change it in the Database management interface.

1.  Go to the Database management screen, click on the DB Instance you want to configure.&#x20;

    <figure><img src="../../.gitbook/assets/image (242).png" alt=""><figcaption></figcaption></figure>
2. Then, click "Edit DB Setting."
3. Scroll down to the "Backup settings" section, and you can configure the following information:
   * **Automatic daily backup:** Enable/disable the automatic daily backup feature.
   * **Backup retention period:** Determine the storage time for automatic backups. To help you save storage space, automatic backups exceeding this period will be deleted.
   * **Backup time:** The time when the automatic backup process takes place. GreenNode recommends choosing this time during the lowest traffic period for your system.

After ensuring that the information is correct, click the "Save" button in the upper right corner and wait for the changes to be applied.

**C. Restore MDS Instance from Backup**

vDB MemoryStore supports restoring a new MDS Instance from a previous backup. This restoration process does not depend on how the backup was created (Manual Backup or Automatic Daily Backup).

To perform the restoration process, go to the Backup management screen and follow these instructions:

1.  Click on the backup you want to restore and choose "Action" -> "Restore." The Restore process is similar to creating a new MDS Instance.&#x20;

    <figure><img src="../../.gitbook/assets/image (241).png" alt=""><figcaption></figcaption></figure>
2. On the MDS Instance restoration screen, you can also choose information about the new MDS Instance configuration in the Instance flavor, DB instance setting, Network & Security, DB Option, and Backup setting sections.
3. After ensuring the information is correct, click the "Restore" button in the upper right corner.
4. Then, return to the Database management screen, and you will see a new MDS Instance being created. The status of this new MDS Instance will also change from "Building/Build" to "Active" if successful.

**D. Delete Backup**
