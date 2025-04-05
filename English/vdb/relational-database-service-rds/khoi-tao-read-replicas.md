# Creating Read Replicas

**Creating Read Replicas**

To expand the read scale for vDB, you can create read replicas for your DB instances. The system will automatically set up a master-slave model and synchronize the data asynchronously.

#### Detailed Steps:

1. **Choose the DB Instance**:\
   First, select the DB Instance from which you want to create a read replica. Note that only DB instances with the role `standalone` or `master` can be used to create read replicas.
2. **Create Read Replica**:\
   Click on the **Action** button and select **Create Read Replica**.
3. **Configure Read Replica**:\
   Here, you will only need to set the **DB Instance Name** for the read replica and leave the other settings as they are, such as flavor, storage type, storage size, and backup schedule. However, we recommend keeping these settings identical to the master or selecting higher values if necessary. Click **Create** to initiate the process.
4. **Wait for Read Replica to Become Active**:\
   After creation, wait for the read replica to reach an **ACTIVE** status.

#### Verifying Data Synchronization:

Once the read replica is created, you can verify that data is being synchronized from the master to the read replica.

* **On dbmaster (IP: 103.245.249.88)**: You should see 6 databases, and for the database `vngtest`, there is 1 table and 1 record.
* **On dbslave1 (IP: 61.28.229.96)**: You will see that the data from dbmaster has been correctly synchronized to dbslave1.
* **Adding Data to dbmaster**:\
  On dbmaster, add data to the `authors` table in the `vngtest` database. You will observe that the data has been replicated to dbslave1.

#### Important Notes:

* You cannot write data to read replicas (e.g., dbslave1) since they are configured with the `read_only=true` flag.

#### Congratulations! You have successfully configured a read replica and set up the master-slave model.
