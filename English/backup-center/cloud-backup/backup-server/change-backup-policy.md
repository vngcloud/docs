# Change backup policy

Updating backup policies is a regular activity to ensure that data is protected effectively and meets current needs. This tutorial will guide you through updating backup policies on your backup server, including changing backup schedules, retention rules, and other configurations.

**There are two ways to change the policy currently applied at a backup server:**

* Switch the application from one backup policy to another.
* Edit directly on the applied backup policy.

**The following instructions help you update the policy applied at one backup server to another policy:**

### 1. Select the backup server whose policy needs to be changed <a href="#id-1.-chon-backup-server-can-thay-doi-policy" id="id-1.-chon-backup-server-can-thay-doi-policy"></a>

First, you need to access the backup server page to select the backup servers that need to change the policy.

* Access the backup server page here: [https://backupcenter.console.vngcloud.vn/backup-server/list](https://backupcenter.console.vngcloud.vn/backup-server/list)
*   Find and **select the backup servers** that need to update the policy, then click **Change policy.**



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FuIaCm7i6o0KnJzSguBzw%252Fimage.png%3Falt%3Dmedia%26token%3D2f272c39-6737-4737-97dd-75afc4a634aa&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ad8fab6b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

### 2. Select the new policy to apply to the selected backup servers. <a href="#id-2.-chon-policy-moi-de-ap-dung-tai-cac-backup-server-vua-chon" id="id-2.-chon-policy-moi-de-ap-dung-tai-cac-backup-server-vua-chon"></a>

After selecting **Change policy** , an interface will appear allowing you to select a backup policy to apply to these backup servers. Next, click **"Apply"** to complete the change process.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FPg6TgqxZpS0X1bCEb5Kr%252Fimage.png%3Falt%3Dmedia%26token%3Df977e694-8dba-4cc9-9af5-505def168af7&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c41a82a5&#x26;sv=1" alt=""><figcaption></figcaption></figure>

### 3. Automatically apply new policy at backup server <a href="#id-3.-tu-dong-ap-dung-policy-moi-tai-backup-server" id="id-3.-tu-dong-ap-dung-policy-moi-tai-backup-server"></a>

After confirming the successful application, one minute later, the system will automatically apply the new policy to the backup server points of the newly changed backup servers. Refer to the following example to understand more about how it works:

* **Old policy:** Run at **00:00** every day, **run every 6 hours** , keep **2 full backups** and have **4 incremental backups** between 2 full versions.
* **New policy:** Run at **00:00** every day, **run every 6 hours** , keep **1 full backup** and have **3 incremental backups** between 2 full versions.
* At the time of change confirmation:
  * Time to complete: 15 hours
  * Number of backup server points: 2 full backups and 4 incremental backups.
* **The system updates the backup server point according to the new policy:**
  * Time to complete: 15h01
  * Action: Keep only 1 full backup (most recent) and 3 incremental backups (most recent).
* **After updating the backup server point according to the new policy, the backup schedule will operate according to the updated policy as follows:**
  * Next backup: 18:00
  * Type of backup server point created: 1 Full Backup is created, and 1 previous Full Backup is deleted (according to the new policy)
