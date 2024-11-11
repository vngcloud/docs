# Restart Replication

In some cases, the process of replicating data from the primary server to the backup server may fail or you want to restart the replication process from the beginning to ensure data synchronization and integrity. The Restart Replication feature allows you to do this easily.

**When to use Restart Replication:**

* **Copy process encountered an error:** If the copy process is interrupted due to technical errors, network or other problems, you can restart the copy so that the system can automatically fix it and continue the copy process.
* **Resynchronize data:** If you suspect there is a missynchronization between the data on the primary and standby servers, you can restart replication to ensure that the data is fully synchronized.
* **Configuration changes:** If you have changed the configuration of the primary server (for example, adding or removing drives), you can restart replication to ensure that the standby server is also updated with the corresponding configuration.

## Restart Replication <a href="#khoi-dong-lai-restart-replication" id="khoi-dong-lai-restart-replication"></a>

**Step 1: Visit the Server Disaster Recovery homepage here:**

**Step 2: Select server**

* In the list of protected servers (Servers Disaster Recovery), identify the server you want to pause replication on.
* Click on **the DR Pair ID** corresponding to that server to view detailed information.

**Step 3: Restart copying**

* In the server details view, find and click the **"Restart Replication"** button .
* From the drop-down menu, select **"Restart Replication"** .

**Step 4: Confirm**

* A pop-up window will appear to confirm your action and warn that all previously created Recovery Points will be deleted.
* Click the **"Restart Replication"** button to begin the replication restart process.
* The server status will change to **"Start Replication"** while the system is processing your request. The status will then change to **"Replicating"** when the new replication process has started.

**Important Note**

* **Delete Recovery Point:** When you restart replication, all previously created restore points will be permanently deleted. Consider carefully before performing this action, especially if you need to restore data to a specific point in the past.
* **Replication Time:** Recopying all data can take a significant amount of time, depending on the data capacity of the primary server. During this time, the standby server will not be ready for failover.

**Summary:**

The Restart Replication feature allows you to restart the data replication process from the beginning, useful in cases where the replication process fails or you need to resynchronize your data. Use this feature with caution and be aware of deleting previously created restore points.
