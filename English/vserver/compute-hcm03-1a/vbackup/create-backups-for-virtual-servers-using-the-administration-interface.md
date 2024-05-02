# Create backups for virtual servers using the administration interface

On vBackup's dashboard, the protected resources page will list all resources backed up at least once. If you are using vBackup for the first time then note that there will not be any resources (such as virtual machines or protected drives) listed on this page. At VNG Cloud, we support centralized data protection for virtual machines (Servers) in the cloud computing environment. You can back up the virtual machine and the data will be transferred to vStorage. However, what you need to do now is to create a backup session for your resources according to the instructions below:

***

**Important**

When you use the vBackup service. In the first time, we will automatically create a default storage at vStorage with 50 GB free space and 1 month shelf life, however to be able to store larger capacity you need to Buy more storage. Backup usage and payment will be stored at vStorage's Gold class, see more backup storage policies and terms [here](https://docs.vngcloud.vn/vstorage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-vbackup-project)

### **Create backups at the vBackup interface** <a href="#createbackupsforvirtualserversusingtheadministrationinterface-createbackupsatthevbackupinterface" id="createbackupsforvirtualserversusingtheadministrationinterface-createbackupsatthevbackupinterface"></a>

1. Open the vBackup console at: [https://hcm-3.console.vngcloud.vn/vserver/block-store/backup/backup-server](https://hcm-3.console.vngcloud.vn/vserver/block-store/backup/backup-server)
2. Choose **Create Backup Server**
3. Select the type of resource you want to backup, here is a list of **Server** and **Volume** attached to it
4. Select the **Policy** you want to apply to the backup
5. The default storage place will be at **vStorage**, so keep in mind that when performing a resource selection operation to create a backup, the system will calculate and make a prediction about the backup capacity, so that creation without interruption and problems need to make sure that your storage space at vStorage is sufficient
6. Enter note information for your backups to create a reminder
7. Select **Create Backup Server**
8. You can then view the newly created backup job information at the list screen, select Backup Server to view information about the protected virtual machine and attached drives, policies, storage location and copy size. backup as well as the last backup time

### **Create backup on Server initialization** <a href="#createbackupsforvirtualserversusingtheadministrationinterface-createbackuponserverinitialization" id="createbackupsforvirtualserversusingtheadministrationinterface-createbackuponserverinitialization"></a>

1. In addition to creating a backup at the vBackup interface, you can also optionally create a backup when creating a new Server. Open the Server console at  [https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server)
2. Select **Create a Server**
3. The page to create a new Server will be displayed, here you can **check the box** to create Backup Server in the **Other Settings** section
4. Then when the Server is created, a Backup Server will be created with the default **Policy** calendar and displayed on the Backup Server list page

### **Create a backup at the Server list page** <a href="#createbackupsforvirtualserversusingtheadministrationinterface-createabackupattheserverlistpage" id="createbackupsforvirtualserversusingtheadministrationinterface-createabackupattheserverlistpage"></a>

1. You can quickly create backups for one or more servers at the server list management page. Open the Server control panel at [https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server)
2. Check one or more servers to create backups, then click on the toolbar and select
3. Create Backup One or more Backup Server copies will be created with the default Policy schedule depending on the number of servers you have chosen to create the backup
