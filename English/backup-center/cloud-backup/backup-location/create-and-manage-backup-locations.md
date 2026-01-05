# Create and Manage backup locations

Backup Location is a useful feature that allows you to create separate storage locations to protect your data backups. Using multiple Backup Locations helps you manage your data more efficiently, flexibly and securely.

**This guide will help you:**

* Understand the concept of Backup Location and its importance.
* Create and manage Backup Locations yourself.
* Configure features like Soft Delete and Location Lock for optimal data protection.

## Create Backup Location <a href="#tao-backup-location" id="tao-backup-location"></a>

**Target:**

* Create a secure, custom storage location for backups.
* Efficiently manage backups based on different criteria.

**Steps to follow:**

1. **Login:** Log in to your GreenNode service management account.
2. **Access the Backup Location management section:** Find and select "Backup Location" here [https://backupcenter.console.vngcloud.vn/backup-location/list](https://backupcenter.console.vngcloud.vn/backup-location/list)
3. **Create new:** Click the "Create backup location" button, an interface window appears for you to fill in the necessary information.
4. **Fill in information:**
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
5. **Save:** Click the "Save" button to finish.

**Benefits of use:**

* **Data Classification:** Create multiple Backup Locations to classify data by project, department or importance.
* **Efficient management:** Easily track usage and data retention time for each location.
* **Cost Optimization:** Choose the right storage type for each location to save costs.
* **Security:** Enhance data security by decentralizing access to different storage locations.

## Enable Soft Delete feature <a href="#bat-tinh-nang-soft-delete" id="bat-tinh-nang-soft-delete"></a>

**Target:**

* Prevent accidental permanent deletion of backups.
* Allows to recover deleted data within a certain period of time.

**How it works:**

* When a backup is marked for deletion, it is not deleted immediately but moved to the virtual recycle bin.
* Users can restore this backup within the specified period (retention day).
* After the data retention period expires, the backup will be permanently deleted.

**Steps to enable the feature:**

Users can enable soft delete while creating a backup location, or enable it after creation. To enable soft delete for an existing backup location, follow these instructions:

* **Access Backup Location:** Find and select the Backup Location for which you want to enable Soft Delete.
*   **Enable Soft Delete:** Find and enable the "Edit Soft Delete" option.



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FICgdUWDkVcILv7fQYZkR%252Fimage.png%3Falt%3Dmedia%26token%3D0de205a1-659c-49ae-ba3f-53dd374198c6&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4c30978b&#x26;sv=1" alt=""><figcaption></figcaption></figure>
* **Configure data retention period:** Enter the number of days you want to keep data in the virtual recycle bin.
* **Save:** Click the "Save" button to finish.

**Benefit:**

* **Avoid data loss:** Prevent important backups from being accidentally deleted.
* **Increased Flexibility:** Allows recovery of deleted data when needed.

**Note:**

* For server point backups that are temporarily stored in the virtual recycle bin, users will still be charged for storage for these backups until they are permanently deleted.
* In case Soft Delete feature is turned off, backups (backup server points) that are temporarily stored in the virtual recycle bin will be permanently deleted immediately.

## Enable Location Lock <a href="#bat-tinh-nang-location-lock" id="bat-tinh-nang-location-lock"></a>

**Target:**

* Protect important backups from unauthorized deletion or modification.
* Ensure compliance with data retention regulations.

**How it works:**

* **Minimum data retention:** Backups must be retained for at least the specified period of time (min retention day).
* **Maximum data retention:** Backups will be automatically deleted after exceeding the specified time (max retention day).
* **Lock configuration changes:** Location Lock feature disabling and configuration changes will be disabled after the allowed editing period.
* **Prevent deletion of backup server point** : When Location Lock is enabled, backup server points that do not meet the deletion conditions will not be allowed to be deleted by users and systems (policy).

**Steps to enable the feature:**

* **Access Backup Location:** Find and select the Backup Location you want to enable Location Lock.
*   **Enable Location Lock:** Click the "Configure Location lock" button, a window will appear allowing you to fill in the necessary information.



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FylnStBnNmT8MzZTOTKFP%252Fimage.png%3Falt%3Dmedia%26token%3Da35b933e-c7d3-45d1-bb23-cb10accaeac1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1a71fa27&#x26;sv=1" alt=""><figcaption></figcaption></figure>
* **Fill in information:** Fill in the required configuration information
  * **Min retention day:** The shortest time that backups must be retained.
  * **Max retention day:** The longest time a backup is retained.
  * **Change duration:** During this time, users can change the Min and Max retention day settings, as well as turn off the Lock feature. After this time, the Lock feature settings cannot be changed.
* **Save:** Click the "Save" button to finish.

**Benefit:**

* **Data Security:** Prevent unauthorized deletion or modification of backups.
* **Regulatory Compliance:** Ensure compliance with data retention regulations (e.g. retaining financial data for a certain period of time).
