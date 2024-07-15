# Working with vBackup project

vBackup project is a type of project created from the backup function to store data from the vBackup system when you create backups for your Server from the vServer system to the vStorage system according to the instructions [đây.](https://docs.vngcloud.vn/display/VSERVERENG/vBackup)

For vBackup project, there will be 2 cases:

* If you do not have any backup project on the vStorage system, when you backup the Server, a new backup project will be created with 50 GB of free capacity on the Gold class storage class and the validity period of this backup project is 1 month. from the time of successfully setting up the backup server according to the instructions above.
* If you already have a backup project that was created and then deleted in the past, when you next backup the Server, a new backup project will be created with 0 GB of free space on the Gold class storage (the backup project name remains unchanged).&#x20;

For these 2 types of vBackup projects, you can:

&#x20;Resize backup project

After a backup project is created for the first time, your backup project now has a storage capacity of 50GB with a storage period of 1 month. From the second initialization, the backup project has 0GB storage capacity. If this storage capacity is not enough for your needs, you can continue to increase the limit of this backup project by:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
2. Select the icon ![](https://docs.vngcloud.vn/download/thumbnails/69468769/image2023-12-27\_15-24-9.png?version=1\&modificationDate=1703665450000\&api=v2) at the project you want to make quota changes to. Select **Resize**.
3. The **Resize project** screen is displayed. Select the **storage quota** you want to increase. You can increase or decrease the **storage quota** to a maximum or minimum level equal to the storage quota provided by the storage package. You cannot adjust the storage quota below or beyond this value.
4. Select **Resize**.
5. Go through the cart **checkout** steps if you are a prepaid user or select **Resize project** if you are a postpaid user.

After you complete the 5 steps described above, your backup project has had its limit increased or decreased.

We only give you 50GB of free Gold class storage for a 1 month storage period. If you increase the capacity beyond 50GB, the cost will be calculated including the storage capacity beyond this 50GB. The process and pricing method are similar to when increasing or decreasing the normal project limit. For more details, please refer to [Charging Fee](https://docs.vngcloud.vn/display/VSEN/Charging+Fee).

***

&#x20;Renew backup project

After a backup project is created for the first time, your backup project now has a storage capacity of 50GB with a storage period of 1 month. From the second initialization, the backup project has a storage capacity of 0GB with a storage period of 1 month. After 1 month of use, your backup project will expire and will be deleted from our system. If you need to store backup data on this Server for more than 1 month, you can extend the backup project according to the instructions below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
2. Select the icon ![](https://docs.vngcloud.vn/download/thumbnails/69468769/image2023-12-27\_15-24-9.png?version=1\&modificationDate=1703665450000\&api=v2) at the **project** you want to perform the renewal on. Select **Renew**.
3. Select the **period** you want to renew.
4. Select **Renew** project.
5. Go through the cart **checkout** steps if you are a prepaid user or select **Renew Project** if you are a postpaid user.

After you complete the 5 steps described above, your backup project has been renewed.

We only give you 50GB of free Gold class storage for a 1 month storage period. If you renew, the cost will be calculated from the end date of your free hosting period to the expiration date of the new period you renew. The process and pricing method are similar to when renewing a regular project. For more details, please refer to [Charging Fee](https://docs.vngcloud.vn/display/VSEN/Charging+Fee).

***

&#x20;Delete backup project

After a backup project is created for the first time, your backup project now has a storage capacity of 50GB with a storage period of 1 month. From the second initialization, the backup project has 0GB storage capacity. If you do not need to use this backup project, you can delete them according to the instructions at Delete project.

Now the **deleted backup project** will be in the **Trash**, you can:

* **Permanently delete** the backup project from vStorage by selecting Delete.
* **Restore** the backup project using the instructions below.

For prepaid customers, if you have incurred costs for extending or increasing this backup project limit, when you delete the remaining backup project, we will refund you the amount. Actual funds that you have not yet used respectively in the remaining storage cycle. For details on how vStorage calculates project chargeback and recovery fees, see [Charging Fee](https://docs.vngcloud.vn/display/VSEN/Charging+Fee).

Because deleting a project is potentially risky, we recommend that you consider carefully and create a backup version of the project before deleting.

***

&#x20;Restore backup project

You can restore the backup project after deleting according to the instructions above by:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
2. Select the **Trash** menu.
3. Select the ![](https://docs.vngcloud.vn/download/thumbnails/69468769/image2023-12-27\_15-24-9.png?version=1\&modificationDate=1703665450000\&api=v2) icon on the **project** you want to perform the restore.
4. Select **Restore** project.
5. Go through the cart **checkout** steps if you are a prepaid user or select **Restore** project if you are a postpaid user.

After you complete the 5 steps described above, your backup project has been restored.

If the backup project that you restore has not been renewed or increased or decreased at any time, you can restore this backup project with payment information of 0 VND. If the backup project that you restore has had its limit extended or increased at least once, you can restore this backup project with payment information as the value of the resource to be renewed or increased with corresponding number of remaining days of use. The process and pricing method are similar to when restoring a regular project. For more details, please refer to [Charging Fee](https://docs.vngcloud.vn/display/VSEN/Charging+Fee).

***

&#x20;The backup project's expiration date has expired

At the expiration of the backup project, we will:

* Move **backup project** resources to the **trash** and store them here for 7 days.
* During these 7 days, you can completely delete the **backup project** or restore the backup project according to the instructions above.

\
