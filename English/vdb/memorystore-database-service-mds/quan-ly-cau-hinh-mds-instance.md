# Manage MDS Instance

The Database management interface provides an overview of all your Database Instances (DB Instances) and detailed information for each one. Let's explore the actions you can perform on MDS Instances:

**A. Create Read Replica:**

To expand the read scale for your vDB, you can create read replicas for your DB Instances. The system will automatically set up a master-slave model and synchronize data asynchronously. Here's how:

1.  Select the DB Instance you want to create read replicas from. Note that only DB Instances with the role "standalone" or "master" can create read replicas. Choose "Action" and then "Create Read Replica."

    <figure><img src="../../.gitbook/assets/image (234).png" alt=""><figcaption></figcaption></figure>
2. On the creation page, simply set the DB Instance Name for the read replica and keep other information like flavor, storage type, storage size, and backup schedule the same. However, we recommend keeping these settings the same as the Master or choosing higher values if necessary.
3. Click "Create Database" to start the creation process. After creation, wait for a while until the read replica is Active.
4. You have now successfully created a Read Replica for your vDB, also known as a master-slave model. You can check if the master's data has been synchronized to the slave.

**B. Promote To Standalone:**

If you want to convert a read replica to standalone, you can use the "Promote to Standalone" feature on the Portal. Follow these steps:

1.  Select the DB Instance with the role "slave," choose "Action," and then "Promote to Standalone."

    <figure><img src="../../.gitbook/assets/image (235).png" alt=""><figcaption></figcaption></figure>
2. Click "Confirm Promote" to complete the process.

Note: Before confirming the promotion, we recommend stopping data writes to the master and waiting until the read replica has fully synchronized the data. Otherwise, there is a chance that the read replica may not have all the data written to the master. The promotion process may take some time to complete, and after this process, the read replica will become standalone, and replication between master and slave will stop. After successful promotion, the read replica will change to the role "standalone" and can be written to, and the DB Instance with the previous master role will also change to the role "standalone" because there is no longer anyone replicating from it.

**C. Resize Instance Type:**

To change the MDS flavor configuration to better suit your actual usage needs, follow these instructions:

1.  Select the MDS Instance you want to change, click the "Action" button, and choose "Resize Instance Type."

    <figure><img src="../../.gitbook/assets/image (236).png" alt=""><figcaption></figcaption></figure>
2. An editor will appear, allowing you to select a new flavor configuration. Review the new and current configuration prices on the right before confirming.
3. Finally, click "Resize" to confirm the process. Wait for a while for the system to perform the necessary steps. When the MDS Instance configuration change is successful, it will have the status "Active."

**D. Edit Configuration Group:**

To change the association of an MDS Instance with an existing Configuration Group, you have two options:

1. Link it immediately when the MDS Instance is created.
2. Modify the MDS Instance configuration.

For option 1, please refer to the instructions on Creating an MDS Instance.

For option 2, you can do the following:

1. Go to the Database management screen at: [https://vdb.console.vngcloud.vn/memorystore/database](https://vdb.console.vngcloud.vn/memorystore/database)
2.  Select the MDS Instance and click "Edit Configuration Group."

    <figure><img src="../../.gitbook/assets/image (237) (1).png" alt=""><figcaption></figcaption></figure>
3. On the change screen, select the Configuration Group you want to apply.
4. When all selections are correct, click the "Save" button in the top right corner. Wait for a while for the configuration variables to be applied to the MDS Instance. If the change is successful, the MDS Instance will have the status "Active."

Note: In some cases, configuration variables may require restarting the Database service on the MDS Instance. The status of the MDS Instance will then be "Restart\_required." With GreenNode, you can proactively choose the time to perform this operation. After backing up tasks on the MDS Instance, click "Action" and choose "Restart" to complete the process.

**E. Edit DB Setting:**

Editing DB Settings allows you to change the Master Password, Public Accessibility, and Backup Settings. To do this, select the database you want to modify and click the "Edit DB Setting" button in the upper right corner.

<figure><img src="../../.gitbook/assets/image (238).png" alt=""><figcaption></figcaption></figure>

An editor will appear to change your DB Settings, including:

* Enable/Disable master password when accessing the MDS Instance.
* Enable/Disable public accessibility.
* Enable/Disable automatic backup settings.

Note: For MDS Instances with the role "slave," enabling/disabling the master password depends on the MDS Instance with the role "master." If the master MDS Instance has the master password enabled, all slave DBs of the master DB will have the password enabled, and vice versa.

**F. Start, Shutdown, Reboot:**

The Start, Shutdown, and Reboot actions help you optimize the use of MDS Instance resources. Perform these actions as needed. To do so, select the MDS Instance you want to change, choose "Action," and click the "Start" / "Reboot" / "Shutdown" button depending on your purpose.

<figure><img src="../../.gitbook/assets/image (239).png" alt=""><figcaption></figcaption></figure>

**G. Delete MDS:**

The "Delete" function allows you to permanently delete an MDS Instance from the system, ensuring the complete removal of the database, data, configuration, and any related dependencies. GreenNode recommends allowing our system to create a final backup of the database before deleting it for data protection and recovery by checking the "Create final backup" box before confirming the deletion.

Note: After completing the deletion process, if the MDS Instance specified for deletion has the role "master," all slave DBs of the deleted master will be promoted to standalone.
