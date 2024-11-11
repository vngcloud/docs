# Create Backup Server Point

**Backup Server Point** is a full or partial backup of your server data at a specific point in time. Creating and managing Backup Server Points is extremely important to ensure that your data is always safe and can be restored when needed.

**Backup Center** provides you with two flexible ways to create Backup Server Points:

1. Create Backup Server Point according to Backup Policy
2. Create Backup Server Point manually by executing "Backup Now"

## Create Backup Server Point automatically according to Backup Policy <a href="#tao-backup-server-point-tu-dong-theo-backup-policy" id="tao-backup-server-point-tu-dong-theo-backup-policy"></a>

1. **Create Backup Plan (Backup Server):** If you don't have one, you need to create a new Backup Server to set up backup rules.
2. **Create Backup Policy:** In Backup Server, you create and associate a Backup Policy to meet different backup needs. For example, the Policy is set up as follows:
   * Launch time **16:00**
   * Backup frequency is **every 4 hours** , the system will create a backup.
   * The gap between 2 Full Backups will be **4 Incremental Backups.**
   * The system keeps **the 2 most recent Full Backups.**
3. **The system will automatically perform:** The system will automatically create Backup Server Point according to the set schedule as follows:
   * At **16:00** of the first launch, the system will create a backup server point **(Full version)** .
   * The next 4 hours at **20:00, 00:00, 04:00 and 08:00** (next day) will create a backup server point **(Incremental version).**
   * In the next 4 hours at 12:00, the system will create a backup server point **(Full version).**
   * Every 4 hours, the system will create server point backups (Incremental versions) until there are 4 Incremental versions, then the next time will be the server point backup (Full version).
   * After creating 3 backup server points (Full version), the system will delete the first backup server point (Full version), and the next 4 consecutive backup server points (Incremental version).

## Create Backup Server Point manually by executing "Backup Now" <a href="#tao-backup-server-point-thu-cong-bang-cach-thuc-hien-backup-now" id="tao-backup-server-point-thu-cong-bang-cach-thuc-hien-backup-now"></a>

The Backup Now feature allows you to perform an immediate data backup session by clicking a "Backup Now" button for the Backup Server or Server you select. Often, users may need to perform a periodic backup, but sometimes it is also necessary to perform an immediate backup session to protect important data at that time.

**Benefits of Instant Data Backup:**

* **Flexibility and Urgency:** Instant data backup allows you to perform a backup whenever you feel the need, instead of having to wait for a scheduled backup. This is useful in an emergency situation or when you want to protect your data immediately before a potential incident.
* **Protect Important Data in the Short Term:** If you only need to back up a small section or a specific project, backing up immediately will help you protect the important data you've just worked on.
* **Fast Recovery:** When you need to recover data, you'll have the most recent backup.

**Detailed instructions:**

### Method 1: Backup now from Backup Server <a href="#cach-1-backup-now-tu-backup-server" id="cach-1-backup-now-tu-backup-server"></a>

1. Access the Backup Server management page here: [https://backupcenter.console.vngcloud.vn/backup-server/list](https://backupcenter.console.vngcloud.vn/backup-server/list)
2. Select the Backup Server to perform Backup Now.
3.  Find and click "Backup Now" as shown below



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FVMRBL9xQnEFSfAbwBETz%252Fimage.png%3Falt%3Dmedia%26token%3Ddd8279cc-087e-4863-aa2e-51069a2b5d70&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=2c3d567c&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Note:**

* When backing up now, the server point backups will be full backups.
* The created server point backups will be of Manual type and will not be affected by backup policy. Users need to actively delete them when not needed.

### Method 2: Backup now from Server <a href="#cach-2-backup-now-tu-server" id="cach-2-backup-now-tu-server"></a>

1. Access the Server management page here: [https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server)
2. Select the Server to perform Backup Now.
3.  Find and click "Backup Now" as shown below.



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FADBCcHkGOE1GkvdzWQHf%252Fimage.png%3Falt%3Dmedia%26token%3Dfa301cdb-8904-4992-a212-b24eb9582f4a&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=31106791&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Note:**

* If the selected Server is not linked to any Backup Server, the system will automatically create a Backup Server with default Backup Policy and Backup Location, and link to this Server, then proceed to create the corresponding server backup point.
* When backing up now, the server point backups will be full backups.
* The created server point backups will be of Manual type and will not be affected by backup policy. Users need to actively delete them when not needed.
