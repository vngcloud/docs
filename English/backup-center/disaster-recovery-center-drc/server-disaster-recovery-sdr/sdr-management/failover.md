# Failover

Failover is an important action in Disaster Recovery (DR), performed when the main server (Main Server) has a problem and cannot operate normally. This conversion ensures business continuity by redirecting all operations to the backup server (Shadow Server) that has previously replicated data.

Follow the instructions below to perform a failover when necessary:

**Step 1: Server Disaster Recovery here:**

**Step 2: Select the server to failover**

* In the list of protected servers (Server Disaster Recovery), identify the server you want to failover to.
* Click on **the DR Pair ID** corresponding to that server to view detailed information.

**Step 3: Start Failover**

* In the server details interface, find and click the **"Failover"** button .

**Step 4: Select a recovery point**

* A pop-up window will appear, asking you to select the time point to restore data.
* Select the desired restore point from the list of available restore points.
* Click the **"Failover"** button to start the failover process.

**Step 5: Monitor the Failover process**

* The server status will change to **"Failover Processing"** while the system is processing your request.
* Replication will be stopped completely during Failover.

**Step 6: Error handling (if any)**

* **Failover Error Case:** If the Failover process fails, you can:
  * **Restart Replication:** Restart the replication process from the beginning and try Failover again later.
  * **Failover again:** Select another Recovery Point and try Failover again.
  * **Contact support:** If you cannot resolve the issue yourself, please contact GreenNode's support team for assistance.

**Step 7: Check and change Recovery Point (if necessary)**

* **Failover success case:**
  * Access the Failover server to check if the data was restored as expected.
  * If necessary, you can perform **"Change Recovery Point"** to restore data to another point in time.

**Step 8: Commit Failover**

* Once you have completed the test and are satisfied with the results, press the **"Commit Failover"** button to complete the failover process.
* Check/uncheck the **"Delete all associated recovery points"** option if you want to delete all associated restore points.
* Click the **"Commit Failover"** button to confirm.

**Note:**

* After Commit Failover, the standby server becomes the primary server and replication will no longer work.
* Please consider carefully before performing Commit Failover as it will affect your entire system.
