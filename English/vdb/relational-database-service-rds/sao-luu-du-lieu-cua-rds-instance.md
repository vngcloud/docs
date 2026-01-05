# Backing Up RDS Instance

#### Backing Up RDS Instance&#x20;

GreenNode vDB supports two methods for data backup: on-demand (manual) and daily automatic backups at a scheduled time.

***

### **A. On-demand Backup (Manual Backup)**

When you need to create a backup, go to the backup management screen for the vDB Relational service [here](https://vdb.console.vngcloud.vn/relational/backup). This screen will list all backups (manual & auto) for all RDS Instances in your account.

#### Steps to create a backup:

1.  Click on the **Create Backup** button. In the **Create Backup** screen, provide the following information:

    * **Backup Name**: Give a name to this backup.
    * **Database Instance Name**: Choose the RDS Instance you want to back up.
    * **Backup Type**: You have two options:
      * **Full Backup**: vDB will back up all your data.
      * **Incremental Backup**: vDB will only back up the changes in your database. The size of an Incremental Backup is much smaller than a Full Backup. However, an Incremental Backup requires you to have created at least one Full Backup for the RDS Instance beforehand.
    * **Backup Parents**: If you chose Incremental Backup, you must specify a Backup Parent for this Incremental Backup. The Backup Parent can be a Full Backup or a previous Incremental Backup.

    > **Note**: Incremental Backup depends on the Backup Parent. If you delete the Backup Parent, all associated Incremental Backups will be invalidated and deleted.
2. Once all information is correct, click **Create**.
   * Initially, the backup status will be **BUILDING**.
   * Once the backup is complete, the status will change to **COMPLETED**.

#### Additional:

You can also create a **Manual Backup directly** from the **Database Management** screen. Click on an RDS Instance, go to the **Backup** tab, and scroll down to the **Backup List**. You can then click **Create Backup** from here.

***

### **B. Auto-Daily Backup**

vDB supports automatic daily backups at a pre-scheduled time.

#### To check if an RDS Instance is configured for auto-daily backup:

1. Go to the **Database Management** screen.
2. Select an RDS Instance, then click the **Backup** tab.
3. In the **Backup Information** section, check if **Automatic backup** is enabled. If it is, it means the RDS Instance is configured for daily automatic backups.

#### To configure Auto-Daily Backup:

You have two options:

* **Configure it during the RDS Instance creation** (see guide for RDS Instance setup).
* **Modify it in the Database Management screen**:
  1. Go to the **Database Management** screen, select the RDS Instance you want to configure.
  2. Click **Edit Database**.
  3. Scroll down to **BACKUP SETTINGS** and configure the following options:
     * **Automatic daily backup**: Enable or disable this feature.
     * **Backup retention period**: Set the retention period for the automatic backups. Backups older than this period will be deleted to save storage space.
     * **Backup time**: Set the time for the automatic backup process. GreenNode recommends selecting a time that is least busy for your system.

4. After verifying the details, click **Save** to apply the changes. Wait a moment for the process to complete.
