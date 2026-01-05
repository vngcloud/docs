# Migrate backup server from vStorage to Vault (backup location)

This article aims to guide Backup Server service users to update backup server point storage location from vStorage to Vault.

Note that GreenNode only encourages users to change the backup server point storage location, because of the [outstanding features that Vault (backup location) brings](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/backup-center/backup-coming-soon/backup-location) . Therefore, if there is no need to change, users can still continue to store backups at vStorage without affecting the quality of the backup server service.

Follow the instructions below to update the new storage location for your backup servers:

## 1. Create a new backup location <a href="#id-1.-tao-moi-mot-backup-location" id="id-1.-tao-moi-mot-backup-location"></a>

First, you need to create a new backup location to prepare for changing the backup server storage location.

* **Login:** Log in to your GreenNode service management account.
* **Access the Backup Location management section:** Find and select "Backup Location" here [https://backupcenter.console.vngcloud.vn/backup-location/list](https://backupcenter.console.vngcloud.vn/backup-location/list)
* **Create new:** Click the "Create backup location" button, an interface window appears for you to fill in the necessary information.
* **Fill in information:**
  * **Location Name:** Give the storage location a memorable and descriptive name.
  * **Backup region:** Select the geographic region where you want to store the backup.
  * **Max quota:** Defines the maximum capacity limit for the storage location.
  * **Soft Delete:**
    * **Enable/Disable:** Decide whether to allow soft delete of backups.
    * **Retention day:** If soft delete is enabled, enter the number of days the backup will be kept before being permanently deleted.
  * **Set as default location:** Select this backup location as the default storage location for new backups.
  * **Location Lock:**
    * **Min retention day:** The shortest time that backups must be retained.
    * **Max retention day:** The longest time a backup is retained.
    * **Change duration:** During this time, users can change the Min and Max retention day settings, as well as turn off the Lock feature. After this time, the Lock feature settings cannot be changed.
* **Save:** Click the "Save" button to finish. The newly created backup location will have a default type of Vault.

## 2. Select the backup servers whose storage locations need to be changed. <a href="#id-2.-chon-cac-backup-server-can-thay-doi-vi-tri-luu-tru" id="id-2.-chon-cac-backup-server-can-thay-doi-vi-tri-luu-tru"></a>

Next, you need to access the backup server page to select the backup servers that need to change the storage location.

* **Access the backup server page** here: [https://backupcenter.console.vngcloud.vn/backup-server/list](https://backupcenter.console.vngcloud.vn/backup-server/list)
* **Find and select the backup server saved in the vStorage project:**
  *   First, you need to **determine the name of the old storage location** by accessing the backup location, determine the name of the backup location with **type = vStorage** as shown below.

      <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FCKYC7GTl5LtuadKb3iDL%252Fimage.png%3Falt%3Dmedia%26token%3Daf958c42-66e4-4001-8e9c-d4b5aa26794e&#x26;width=300&#x26;dpr=4&#x26;quality=100&#x26;sign=5b1ad41f&#x26;sv=1" alt=""><figcaption></figcaption></figure>
  *   Next, go to the **backup server** page , select the backup server with the storage location **vBackup-Project-5fa985c8** (note that this name will vary from user to user).



      <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FNEEXSalsuTRfzcufx3kU%252Fimage.png%3Falt%3Dmedia%26token%3Da781b654-90ab-42ae-bf98-31e2476dc455&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4167a2f7&#x26;sv=1" alt=""><figcaption></figcaption></figure>

## 3. Find and select change location <a href="#id-3.-tim-va-nhan-chon-change-location" id="id-3.-tim-va-nhan-chon-change-location"></a>

After selecting the backup servers that need to be changed, click on the **Change Location** feature , an interface will appear allowing you to select a new storage location for these backup servers.

*   Select a new storage location for the backup server as shown below.



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FqVYHAUNiLmx1z7T60mm5%252Fimage.png%3Falt%3Dmedia%26token%3D271f7462-ee1e-445f-bfe4-1374aa0c6aaf&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6366e1aa&#x26;sv=1" alt=""><figcaption></figcaption></figure>
* Click **"Change"** to confirm the change is complete.

## 4. Save the backup server point to the new storage location <a href="#id-4.-luu-backup-server-point-tai-noi-luu-tru-moi" id="id-4.-luu-backup-server-point-tai-noi-luu-tru-moi"></a>

Once the changes are complete, you can go to the [backup server](https://backupcenter.console.vngcloud.vn/backup-server/list) page to see the new backup location recorded. Note that:

* **The backup schedule** and **retention rules** still follow the backup policy, the only difference is that the newly created backup server points will be stored at the new backup location.
* The **backup server points stored in vBackup-Project** before are unchanged, users can still access them when needed.
* GreenNode recommends that customers should download the backup server points needed, and delete **vBackup-Project** to avoid incurring storage costs at vStorage after transferring **all backup servers to the new backup location** and **incurring storage of backup server points (Full)** here.
