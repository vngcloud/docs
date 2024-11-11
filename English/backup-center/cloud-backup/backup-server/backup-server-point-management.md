# Backup Server Point Management

Backup Server Point is a full or partial backup of server data at a specific point in time. Effective management of Backup Server Points helps you ensure business continuity and minimize the risk of data loss.

This tutorial will guide you step by step through the Backup Server Point management operations, including viewing the list, viewing history, downloading, and deleting.

## View list of backup server points <a href="#xem-danh-sach-backup-server-point" id="xem-danh-sach-backup-server-point"></a>

1. Access the backup server list page here: [https://backupcenter.console.vngcloud.vn/backup-server/list](https://backupcenter.console.vngcloud.vn/backup-server/list)
2.  Select the Backup Server to view the backup server point. You can click on the search box, enter the name of the backup server you want to find.

    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FF8FeATCif1jF6W2HHCCw%252Fimage.png%3Falt%3Dmedia%26token%3Dffabaec5-b249-456b-93ab-5d225d5fa284&#x26;width=300&#x26;dpr=4&#x26;quality=100&#x26;sign=9c86105f&#x26;sv=1" alt=""><figcaption></figcaption></figure>
3. On the Backup Server details page, click the Restore Point tab. Here, you will see a list of the server backup points that have been created. The information includes:
   1. **Backup Server Point ID** / Backup server point identifier
   2. **Estimated Backup Size** / Backup size
   3. **Backup Type** : Full / Incremental (diff)
   4. **Schedule Type** : Policy (automatic backup by schedule) / Manual (user performs [backup now](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/backup-center/backup-coming-soon/backup-server/tao-backup-server-point) )
   5. **Backup Location** : Location of backup server points
   6.  **Status** : Backup status (Active / Failed)



       <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FS9r9xPGgR0SUwvy4zBgp%252Fimage.png%3Falt%3Dmedia%26token%3Dd4ae90bd-60dd-4db7-a234-dbae71f1312e&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ecbfe6d2&#x26;sv=1" alt=""><figcaption></figcaption></figure>
4. In addition, users can delete and download server point backups from this Restore Point tab.

## View Backup Server History <a href="#xem-lich-su-backup-server" id="xem-lich-su-backup-server"></a>

To view the history of backup server point initializations, follow these instructions:

1. Access the History page of Backup Center here: [https://backupcenter.console.vngcloud.vn/backup-history/list](https://backupcenter.console.vngcloud.vn/backup-history/list)
2. Select the Backup History tab to view the history of backup initiations.
3. Enter Backup Server ID in the search box to view the backup initialization history of a backup server. The information displayed includes:
   1. **Status:** Backup server point initialization status (Active -> Created successfully; Error -> Created failed)
   2. **Backup Type** : Full / Incremental (diff)
   3. **Schedule Type** : Policy (automatic backup by schedule) / Manual (user performs [backup now](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/backup-center/backup-coming-soon/backup-server/tao-backup-server-point) ).
   4. **Size (GB)** : Backup capacity
   5. **Time period:** Backup server point initialization time
   6. **Deletion status:**
      1. **Empty** (if the backup server point exists);
      2. **Deleted** (the backup server point has been deleted);
      3. **Soft deleted** (server point backup is temporarily deleted, can be restored).

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FndphOOWysphHm81KdzoA%252Fimage.png%3Falt%3Dmedia%26token%3Dbdb2bec4-4c99-48c5-bec6-8a6408b2e6a0&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=88e3ae&#x26;sv=1" alt=""><figcaption></figcaption></figure>
