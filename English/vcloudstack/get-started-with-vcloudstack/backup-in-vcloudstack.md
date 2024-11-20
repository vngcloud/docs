---
description: Coming soon
---

# Backup in vCloudStack

### Overview <a href="#tong-quan" id="tong-quan"></a>

Backup is VNG Cloud’s full backup function, brought into the vCloudStack service to help protect your business data, allowing you to automate backups of virtual machine drives and archive them. Using Backup, you can centrally configure backup policies and monitor backup activity for your resources including creating automatic daily, weekly, and monthly backups. Each backup is a complete file-based snapshot of your drives taken at a preferred scheduled timeframe based on your policies while the virtual machine is still running. This means that the Backup service is non-disruptive and provides you with a complete set of recovery options. Backup automates and consolidates backup tasks previously performed by each service, eliminating the need for custom scripting and time-consuming manual processes, allowing you to meet your regulatory and business backup compliance requirements.

vBackup service provides you with key functions including:

* **Backup:** Create backups for the drives on your virtual server;
* **Restore:** Perform a restore from the virtual server backup file to a new server at the time the backup file was created.

{% hint style="info" %}


vCloudStack provides backup functionality that allows data backup on both environments:

* Cloud Backup (vStorage)
* Backup on Local (Worker) - updating
{% endhint %}

***

#### **Create backup to vStorage according to Policy schedule** <a href="#taobansaoluuchomaychuaotheobolichpolicy-taobansaoluutheobolichpolicytaigiaodienvbackup" id="taobansaoluuchomaychuaotheobolichpolicy-taobansaoluutheobolichpolicytaigiaodienvbackup"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack, go to the Backup page.

**Step 2:** Select **Create Backup Server** ;

**Step 3:** Select the type of resource you want to backup, here is the list of Servers and Volumes attached to it

**Step 4:** Select **the Policy** you want to apply to the backup. Note that you need to create a Policy to be able to add it to your Backup Server. See instructions [for creating a Policy](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcloudstack/bat-dau-voi-vcloudstack/backup-trong-vcloudstack#tao-chinh-sach-policy-sao-luu) below.

**Step 5:** The default storage location (Backup Location) will be in **vStorage;**

{% hint style="info" %}
**Note:**

* When performing the operation of selecting resources to create a backup, the system will calculate and give a **prediction result about the backup capacity** . To ensure that the creation is not interrupted and has problems, it is necessary to ensure that the capacity of your storage location at vStorage is sufficient.
* Use vBackup service. For the first time, we will automatically create a default storage location at vStorage with a **free capacity of 50 GB and a 1-month usage period** , however, to be able to store with a larger capacity, you need to purchase additional storage space.
* If you don't have a Backup Location, you can create a default storage location in vStorage by going to Backup Location and selecting **Create backup location** , the system will automatically create it.
{% endhint %}

**Step 6: Enter notes** for your backups to create a reminder

**Step 7:** Select the **Create button**

**Step 8:** Then you can view the information of the backup job you just created in the list screen, select Backup Server to view information about the protected virtual machine and attached drive, policy, storage location and backup size as well as the most recent backup time.

***

### Create backup policy <a href="#tao-chinh-sach-policy-sao-luu" id="tao-chinh-sach-policy-sao-luu"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack;

**Step 2** : In the navigation menu bar, select the **Backup Policy Tab**

**Step 3:** Select **Create Backup Policy**

**Step 4: On the Policy creation page, enter the Policy Name** information in the **Basic Information section.**

**Step 5:** Then in the **Policy Configuration** section , select **the time** and **time zone** in which the system will perform the backup.

**Step 6** : Choose **the backup frequency** that suits your needs: Daily, Weekly, Monthly. Note that you can combine all 3 together to create the most perfect schedule.

**Step 7** : Enter **the number of copies** (Retention) that the system will keep the most recent backups.

**Step 8:** You can also choose to **automatically back up** drives added to the virtual machine later.

**Step 9:** Select **Create** , then the system will initialize the new policy you just created.

{% hint style="info" %}
**How backup policy works**

A backup policy is selected with a backup frequency **of Daily** at **12:00** and a number of copies to keep **4.** Every day at 12:00 noon, the system will create a backup for the virtual server according to the above time frame, with the first backup being a full backup for the virtual server, the next day will back up the changed parts of the virtual machine since the last backup of yesterday, the number of copies to keep will be 4 copies according to the last 4 days.
{% endhint %}

### **Edit backup policy** <a href="#tao-chinhsua-xoachinhsachsaoluu-chinhsuachinhsachsaoluu" id="tao-chinhsua-xoachinhsachsaoluu-chinhsuachinhsachsaoluu"></a>

When the backup policy no longer fits the business requirements or data size or faster recovery times are required, you need to edit the backup policy parameters.

**Backup policy editing process:**

**Step 1:** Access the vServer interface with Region as vCloudstack;

**Step 2:** In the navigation menu bar, select the **Backup Policy Tab**

**Step 3** : Select **Edit Backup Policy**

**Step 4:** You can re-enter the policy name, as well as change all the parameters about the time, backup time zone, as well as the backup schedule, the number of copies of the Backup Policy you want to update.

**Step 5:** After updating the policy, select **Save** to change.

### **Delete backup policy** <a href="#tao-chinhsua-xoachinhsachsaoluu-xoachinhsachsaoluu" id="tao-chinhsua-xoachinhsachsaoluu-xoachinhsachsaoluu"></a>

You can delete a backup policy if you no longer need it, but note that you cannot delete the default backup policy created by the system.

**Procedure to delete backup policy:**

**Step 1:** Access the vServer interface with Region as vCloudstack;

**Step 2:** In the navigation menu bar, select the **Backup Policy Tab**

**Step 3:** Select **Delete Backup Policy**

**Step 4:** After deleting, the backup policy will disappear from the list page.

***

### Restore backup <a href="#khoi-phuc-ban-sao-luu" id="khoi-phuc-ban-sao-luu"></a>

Once a resource has been backed up at least once, it is considered protected and available for restore.

If you're restoring a virtual machine, you can perform a Full Restore to restore the entire virtual machine system to a new virtual machine. Or, you can restore specific drives within a virtual machine. Follow the steps below to completely restore a virtual machine or your drives:

#### **Virtual Server Recovery Process** <a href="#khoiphucbansaoluu-quytrinhkhoiphucmaychuao" id="khoiphucbansaoluu-quytrinhkhoiphucmaychuao"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack;

**Step 2** : Select Backup

**Step 3:** Select the virtual server to be backed up and click **Restore**

**Step 4:** The new virtual server creation page will display with the configuration of the backup, you need to select the remaining parameters to complete the backup restoration to a virtual machine.

**Step 5:** Select **create new virtual machine**

**Step 6:** A virtual server will be created in **Shutdown** state with the configuration of the backup you selected earlier.

#### **Drive recovery process** <a href="#khoiphucbansaoluu-quytrinhkhoiphucodia" id="khoiphucbansaoluu-quytrinhkhoiphucodia"></a>

**Step 1:** Access the vServer interface with Region as vCloudstack;

**Step 2** : Select Backup

**Step 3:** View details of the backed up virtual server

**Step 4:** In the list of drives attached to the virtual machine, select the drive you backed up and click **Restore**

**Step 5:** The new drive creation page will appear with the configuration of the backup, you need to select the remaining parameters to complete the backup restoration to a drive.

**Step 6:** Select **create new drive**

**Step 7:** A new drive is created with the configuration of the backup you selected earlier.

{% hint style="info" %}
**Note**

Regardless of whether you restore a virtual machine or a disk, each restore will create a new one. If you attempt to restore the same resource multiple times, there may be duplicate entries for that resource.
{% endhint %}
