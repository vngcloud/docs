# Stop & Resume Replication

During the use of Server Disaster Recovery (SDR) service, there may be times when you need to pause the replication process from the primary server to the backup server. The Stop Replication & Resume Replication feature gives you flexibility in managing replication, helping you:

* **Cost savings:** In some cases, you may want to pause replication to save on snapshot storage costs, especially when the primary server doesn't have many data changes.
* **Perform maintenance:** When the primary server needs maintenance, you can pause replication to avoid data conflicts and ensure the integrity of the maintenance process.
* **Control the copy process:** You can proactively pause and resume copying at any time, depending on your needs and actual situation.

## **Stop Replication** <a href="#tam-dung-sao-chep-stop-replication" id="tam-dung-sao-chep-stop-replication"></a>

**Step 1: Visit the Server Disaster Recovery homepage here:**

**Step 2: Select server**

* In the list of protected servers (Servers Disaster Recovery), identify the server you want to pause replication on.
* Click on **the DR Pair ID** corresponding to that server to view detailed information.

**Step 3: Pause copying**

* In the server details view, find and click the **"Stop Replication"** button .

**Step 4: Confirm**

* A pop-up will appear to confirm your action.
* Click the **"Stop Replication"** button to pause the replication process.
* The pairing status will change to **"Pending"** while Replication is temporarily paused.

## **Resume Replication** <a href="#tiep-tuc-sao-chep-resume-replication" id="tiep-tuc-sao-chep-resume-replication"></a>

**Step 1: Visit the Server Disaster Recovery homepage here:**

**Step 2: Select server**

* In the list of protected servers (Servers Disaster Recovery), identify the server you want to pause replication on.
* Click on **the DR Pair ID** corresponding to that server to view detailed information.

**Step 3: Continue copying**

* In the server details interface, find and click the **"Actions"** button .
* From the drop-down menu, select **"Resume Replication"** .

**Step 4: Confirm**

* A pop-up will appear to confirm your action.
* Click the **"Resume Replication"** button to continue the replication process.
* The server status will change to **"Replicating"** when replication has resumed.

**Note:**

* You can only pause and resume replication while the server is in **"Replicating"** state .
* When replication is paused, previously created Recovery Points are preserved.
* As cloning continues, the system will continue to create new restore points on a pre-set schedule.

With Stop Replication & Resume Replication, you can flexibly manage data replication, optimize costs, and ensure system integrity during maintenance.
