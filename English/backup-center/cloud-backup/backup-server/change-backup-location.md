# Change backup location

Backup points are an important part of your data protection strategy. Choosing the right storage location will help ensure the safety and effectiveness of your backups. If you want to change the location of your backup point, this article will provide you with detailed and easy-to-understand instructions.

First, you need to have a backup location ready to store the new backup point:

* Refer to the article on how to initialize backup location [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/backup-center/backup-coming-soon/backup-location/tao-va-quan-ly-backup-location#tao-backup-location) .

If you already have a backup location ready for storing backup points, follow the steps below to update the new backup location for your backup server:

## 1. Select the backup servers whose storage locations need to be changed <a href="#id-1.-chon-cac-backup-server-can-thay-doi-vi-tri-luu-tru" id="id-1.-chon-cac-backup-server-can-thay-doi-vi-tri-luu-tru"></a>

First, you need to access the backup server page to select the backup servers that need to change storage locations.

* Access the backup server page here: [https://backupcenter.console.vngcloud.vn/backup-server/list](https://backupcenter.console.vngcloud.vn/backup-server/list)
*   Find and **select the backup servers** whose storage locations need to be updated, then click **Change location.**



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FIuYezybDnrrOAtN6zQ76%252Fimage.png%3Falt%3Dmedia%26token%3D007ba821-ca1e-4717-b828-986d062f05b8&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=9c062a6b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

## 2. Select a new backup location <a href="#id-2.-chon-vi-tri-luu-tru-moi-backup-location" id="id-2.-chon-vi-tri-luu-tru-moi-backup-location"></a>

After selecting **Change Location** , an interface will appear allowing you to select a new storage location for these server backups.

*   Select a new storage location for the backup server as shown below.



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FqVYHAUNiLmx1z7T60mm5%252Fimage.png%3Falt%3Dmedia%26token%3D271f7462-ee1e-445f-bfe4-1374aa0c6aaf&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6366e1aa&#x26;sv=1" alt=""><figcaption></figcaption></figure>
* Click **"Change"** to confirm the change is complete.

## 3. Save the backup server point to the new storage location <a href="#id-3.-luu-backup-server-point-tai-noi-luu-tru-moi" id="id-3.-luu-backup-server-point-tai-noi-luu-tru-moi"></a>

Once the changes are complete, you can go to the [backup server](https://backupcenter.console.vngcloud.vn/backup-server/list) page to see the new backup location recorded. Note that:

* **The backup schedule** and **retention rules** still follow the backup policy, the only difference is that the newly created backup server points will be stored at the new backup location.
* The **backup server points stored at** the previous backup location remain unchanged and can still be accessed by users when needed.
