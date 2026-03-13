# Promote Read Relica to Standalone

**Promote a Read Replica to Standalone**

When you want to convert a read replica into a standalone DB instance, you can use the **Promote to Standalone** feature on the Portal.

#### Steps:

1. **Select the Read Replica**:\
   Choose the DB instance with the role `slave` (read replica) that you want to promote.
2. **Choose Action**:\
   Click on the **Action** button and select **Promote to Standalone**.
3. **Wait for Synchronization**:\
   Before confirming the promotion, it is recommended that you stop writing data to the master instance and wait until the read replica has fully synchronized all data. However, there may be instances where the read replica has not yet fully synchronized the data written on the master. Keep in mind that the promotion process may take some time to complete.
4. **Promotion Process**:\
   Once the promotion process is complete, the read replica will be converted into a standalone instance. The replication between the master and slave will stop.

#### Result:

* After the promotion is successful, the read replica will have the role `standalone` and will be able to accept writes.
* The DB instance that was previously the master will also be changed to the `standalone` role, as there will no longer be any replicas replicating from it.
