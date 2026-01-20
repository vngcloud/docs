# Attention & Limitations

**A. Master User Privileges:**

For vDB relational databases, when creating a vDB, you are provided with a Master User to access the database.

The Master User will be granted the following privileges:

*   **MySQL/MariaDB:**

    * **Global Privileges:** ALTER ROUTINE, ALTER, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE USER, CREATE VIEW, CREATE, DELETE, EVENT, EXECUTE, INDEX, INSERT, LOCK TABLES, PROCESS, REFERENCES, RELOAD, REPLICATION CLIENT, REPLICATION SLAVE, SELECT, SHOW DATABASES, SHOW VIEW, TRIGGER, UPDATE.
    * **Database Privileges:** Full Privileges.

    **Note:** Database privileges exclude system databases such as `mysql`, `information_schema`, `performance_schema`, and `sys`. When creating a new database, the system will automatically grant all privileges to the Master User. If this is not done, please wait a moment or contact GreenNode Support.
* **PostgreSQL:**
  * **Privileges:** `Createrole`, `CreateDB`, `Replication`.

***

**B. Service Users/Roles:**

For vDB relational databases, the system will automatically create service users/roles to perform automated tasks. Please do not delete these users/roles to avoid errors in automatic features.

* **MySQL/MariaDB:** `os_admin`@`127.0.0.1`, `root`@`localhost`
* **PostgreSQL:** `os_admin`, `postgres`

***

**C. Import Database:**

For relational vDBs, when backing up the source database, only back up the databases containing data, avoiding backup of all databases (which includes system databases like `mysql`, `sys`, `performance_schema`, `information_schema`) or stored procedures with the definer set to `root`. If the dump file contains stored procedures with the definer set to `root`, please replace it with the Master User defined during vDB creation. For example:

```bash
sed -i 's/definer=root/definer=<master_user>/g' dump.sql
```

***

**D. Failover When vDB Master Role Goes Down:**

Currently, vDB does not automatically failover when the Master vDB role (Read/Write) in the Master/Read-Replica model faces issues. The decision to promote a Read Replica to the new Master role lies with the customer. Please note that after promotion, synchronization with the previous Master will be interrupted, and it cannot be rolled back.

To restore High Availability for the system, you can create a new read-replica from the Standalone vDB.

To do this, follow these steps:

1. Select the instance with the Replica role and perform the **Promote to Standalone** action.
2. Update the `connection_string` in your application to Read/Write data to the new Master.
3. After verifying that the application is stable, select the new Master and proceed to create a read-replica from this new Master.
4. You can delete the old Master if no longer needed.
