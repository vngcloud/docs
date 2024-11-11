# Create Backup Plan (Backup Server)

To protect your server by creating regular backups, you first need to link your server to a backup plan (backup server). Backup Center supports server users in creating backup plans (backup servers) in the following ways:

* Create backup plan and link to server.
* Enable backup plan creation when creating server

## Create backup plan (backup server) <a href="#tao-backup-plan-backup-server" id="tao-backup-plan-backup-server"></a>

1. Access the Backup Server interface of Backup Center here: [https://backupcenter.console.vngcloud.vn/backup-server/list](https://backupcenter.console.vngcloud.vn/backup-server/list)
2. Select **Create Backup Server.**
3. Select the server to backup, note that this page only shows servers that do not have a backup plan linked.
4. Select the backup policy that applies to this backup plan (backup server). Learn more about backup policies here.
5. Select the backup location (where the backup server points are stored). Learn more about backup locations here.
6. Fill in descriptive information to remind (optional).
7. Click **Create**

Then you can view the information of the backup job you just created in the list screen, select Backup Server to view information about the protected server and attached volume, backup policy, backup server and backup point size as well as the most recent backup time.

## Enable backup plan creation when creating server <a href="#kich-hoat-tao-backup-plan-khi-tao-server" id="kich-hoat-tao-backup-plan-khi-tao-server"></a>

Users can activate the backup plan (backup server) along with server initialization to save time, as well as protect the server comprehensively. Refer to the following instructions.

1. Access the Cloud Server interface.
2. Select **Create a server**
3.  On the new Server creation page, you can check the **Enable Backup** box in the **Other settings section.**



    <figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fyt9U878fM3Dehu8ZJFQl%252Fimage.png%3Falt%3Dmedia%26token%3D4654d39e-d34f-4f99-8ab7-51039ad388c7&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=a51d69a2&#x26;sv=1" alt=""><figcaption></figcaption></figure>
4. Then when the Server is created **,** a backup plan (backup server) will be created with a default backup policy and backup location. That means, the backup creation and storage location for this server will depend on the default backup policy and backup location. You can freely change the backup policy and backup location later.
