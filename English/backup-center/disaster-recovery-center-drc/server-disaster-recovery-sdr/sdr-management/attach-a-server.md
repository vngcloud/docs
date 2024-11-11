# Attach a Server

Follow the instructions below to add a primary server to Server Disaster Recovery.

1. In the Server Disaster Recovery Center console, click the **"Attach a Server"** button in the upper left corner.
2. A pop-up window will appear, asking you to provide configuration information for the primary and backup servers.
   * **Region:** Select the geographic region where your primary server is located (e.g. HCM-03).
   * Click **to select the primary server** to add to Server Disaster Recovery
   * **Shadow Server Configuration:**
     * **Region:** Select the geographic region where you want to place the backup server.
     * **VPC (Virtual Private Cloud):** Select the VPC you want the backup server to belong to.
     * **Subnet:** Select the specific subnet in the selected VPC to place the backup server.
   * **Select Multiple Main Servers:**
     * If you want to add multiple primary servers at once, check the boxes next to the server names.
     * You can also select all servers at once by checking the box at the top of the list.
3. **Confirm:** After providing all the information, click the **"Attach"** button to complete the server adding process.

* If the server addition process is successful, you will receive an **"Attach Server Successful"** message and the system will automatically redirect you to the Server Disaster Recovery dashboard.

**Note:**

* Expired primary servers are still displayed but cannot be selected for addition to DRC. You need to renew the server before adding it to SDR.
* Shadow Servers that are in the process of pairing or have not confirmed their failover status cannot be selected either.
* Primary servers with drives with "multi-attach" settings (allowing them to be attached to multiple servers at once) cannot be added to SDR.
