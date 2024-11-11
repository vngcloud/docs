# Restore resources

This guide will help you perform the process of restoring resources (servers or volumes) from previously created backups. The restore process will help you bring the system back to its previous state at a specific point in time, ensuring the continuity and safety of your data.

**Concept**

* **Backup server point:** A complete backup of the entire server at a specific point in time.
* **Backup volume point:** A backup of a specific volume (drive) in the server.
* **Server Restore:** Restore the entire server to the state of a backup server point.
* **Restore volume:** Restore a specific volume to the state of a backup volume point.

**Steps to follow**

1. Access the backup server list page here: [https://backupcenter.console.vngcloud.vn/backup-server/list](https://backupcenter.console.vngcloud.vn/backup-server/list)
2.  Select the Backup Server you want to restore. You can click on the search box and enter the name of the backup server you want to find.

    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FF8FeATCif1jF6W2HHCCw%252Fimage.png%3Falt%3Dmedia%26token%3Dffabaec5-b249-456b-93ab-5d225d5fa284&#x26;width=300&#x26;dpr=4&#x26;quality=100&#x26;sign=9c86105f&#x26;sv=1" alt=""><figcaption></figcaption></figure>
3.  On the Backup Server details page, click the Restore Point tab. Here, you will see a list of created server point backups.



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FvWCqeWaCo4UOfN0dCYe0%252Fimage.png%3Falt%3Dmedia%26token%3D6a63f2cb-b5cb-495a-ac02-eebe9ef842c0&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=92e44c6f&#x26;sv=1" alt=""><figcaption></figcaption></figure>
4. Select the backup to restore and click restore for the following 2 cases:

*   **Select backup server point:** If you want to restore the entire server, select the desired backup server point and press restore.



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FnJlV048BzcPogyvm4lgo%252Fimage.png%3Falt%3Dmedia%26token%3Df2592b77-1f81-4a61-bf79-2310c0c6453a&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7f9ec67e&#x26;sv=1" alt=""><figcaption></figcaption></figure>
*   **Select backup volume point:** If you only want to restore a specific volume, select the backup server point containing that volume, then select the backup volume point to restore and click restore.



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F6M0Nyw8oPwLwD1LSc7oX%252Fimage.png%3Falt%3Dmedia%26token%3D7f314bed-251d-4e08-b603-78ec8b8f7ecf&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b197e225&#x26;sv=1" alt=""><figcaption></figcaption></figure>

1. After clicking Restore, the system will navigate the user to the Server or Volume initialization page to configure the necessary parameters. Click initialize to start the restore process.

**Important Note**

* The newly created server from restoring the backup server point will have the **Shutdown** status . Users need to proactively start the server when they need to use it.
* **Full Backup:** Make sure the backup you choose contains all the data you need to restore.
* **Check data:** After restoring, check the data again to ensure accuracy and completeness.
* **Permissions:** You need permission to perform restore operations.
* **Recovery Plan:** There should be a detailed recovery plan in place to respond quickly in case of an incident.
