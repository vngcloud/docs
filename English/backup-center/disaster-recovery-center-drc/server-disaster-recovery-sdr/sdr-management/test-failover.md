# Test Failover

The Test Failover feature allows you to simulate a failover to a Shadow Server to test your DR plan and ensure your system is ready to operate when needed, without affecting the operation of the primary server.

1. **Visit the Server Disaster Recovery homepage here:**
2. **Select the server to check**
   1. In the list of protected servers (DR Servers), identify the server you want to perform failover testing on.
   2. Click on **the DR Pair ID** corresponding to that server to view detailed information.
3. **Start Test Failover** : In the server details view, find and click the **"Test Failover"** button .
4. **Configure Test Failover Server information**

A pop-up window will appear, asking you to provide the information required for the failover test:

* **Failover Server Name:** Name the temporary failover server (5-50 characters, contain only letters, numbers, underscores, and hyphens).
* **Region:** The geographic region where you want to create the temporary failover server (default is the Shadow Server region).
* **Recovery Point:** Select the point in time you want to restore data to (current time or a previous restore point).
* **Network Settings:**
  * **VPC:** Select the VPC that you want the temporary failover server to belong to.
  * **Subnet:** Select the specific subnet in the selected VPC.
  * **IP:** (Optional) Enter the IP address you want to assign to the temporary failover server. If left blank, the system will automatically allocate an IP address.
  * **Floating Setting:** Check if you want to assign a Floating IP to the temporary failover server for access from the Internet.
* **Volume Settings:**
  * **Test Server volume type:** Select the volume type for the temporary failover server (SSD or NVMe).
  * **Test Server Volume IOPS:** Select the IOPS level for the temporary failover server.
* **Instance Type:**
  * **Instance Family:** Select a server family (e.g. General Purpose, Compute Optimized, Memory Optimized).

1. **Start testing**

* Once configured, click the **"Test Failover"** button to start the testing process.
* The pairing status in the **In Testing Failover** column will change to **"Processing"** while the system is processing your request.

1. **Change Recovery Point (optional)**

* During testing, if you want to test the recovery at a different point in time, you can change the Recovery Point.
* On the pairing details page, find and click the **"Change Recovery Point" button.**
* An interface window will appear allowing you to select the desired restore point from the list of available restore points.
* Click the **"Change Recovery Point"** button to apply the changes.

1. **Clean up the test environment**

* After completing the test, find and select **"Clean Test Environment"** to delete the temporary resources created during Test Failover to avoid incurring costs.
* The pairing status in the **In Testing Failover** column will change to blank.

**Note:**

* Data replication continues normally while you are performing the failover test.
* Perform Failover Tests regularly to ensure your DR system is always ready to operate when needed.
