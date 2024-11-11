# Get Started with Backup Server

**Protect your data comprehensively with Backup Server service**

Are you worried about losing important data due to computer crashes, cyber attacks or natural disasters? Backup Server service will be the perfect solution to help you protect your data safely and effectively.

With Backup Server service, you can automatically create and store backups of your data in a secure location. This gives you peace of mind while working and minimizes the risk of data loss.

**This guide will help you:**

* Understand the basic concepts of Backup Server.
* Set up and use the service yourself with ease.
* Optimize backup process for most effective data protection.

**Start now to protect your data**

## 1. Create a backup location <a href="#id-1.-tao-vi-tri-luu-tru-backup-backup-location" id="id-1.-tao-vi-tri-luu-tru-backup-backup-location"></a>

* **Purpose:** Set up a secure storage location for backups.
* **Steps:**
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

## 2. Create Backup Policy <a href="#id-2.-tao-chinh-sach-sao-luu-backup-policy" id="id-2.-tao-chinh-sach-sao-luu-backup-policy"></a>

* **Purpose:** Set up backup schedules and rules.
* **Steps:**
  * **Policy Name:** Give the policy a memorable and descriptive name.
  * **Time configuration:**
    * **Select Time:** Select the time to start the backup (hour, minute).
    * **Time zone:** Select the appropriate time zone.
  * **Data retention configuration:**
    * **Hourly, daily, weekly, monthly:** Choose how often to keep backups.
    * **Combine multiple rules:** Multiple rules can be combined to create flexible schedules.
  * **Enable server protection:** Automatically create backups for the server as soon as this feature is enabled, no need to wait for a schedule.
  * **Notifications:** Choose to receive email notifications when the backup process succeeds or fails.

## 3. Create Backup Server <a href="#id-3.-tao-may-chu-sao-luu-backup-server" id="id-3.-tao-may-chu-sao-luu-backup-server"></a>

* **Purpose:** Associate the server to be protected with a policy and storage location.
* **Steps:**
  * **Select Server:** Select the server to backup from the list.
  * **Select policy:** Apply the created backup policy.
  * **Select storage location:** Select a storage location for your server backup.

## 4. View Backup History <a href="#id-4.-xem-lich-su-sao-luu" id="id-4.-xem-lich-su-sao-luu"></a>

* **Purpose:** Monitor backup and restore activities.
* **Steps:**
  * Access the history section.
  * View details of backup, restore, error (if any) activities.
  * Filter data by server, policy, time to find specific information.
