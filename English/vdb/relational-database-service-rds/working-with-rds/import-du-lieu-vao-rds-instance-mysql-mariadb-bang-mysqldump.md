# Import Data into RDS Instance (MySQL/MariaDB) using mysqldump

To import data into an RDS Instance with a MySQL/MariaDB datastore, you can use the **mysqldump** tool.

Follow these steps to perform the import:

#### 1. Dump Data from Your MySQL Server:

On your MySQL server, you can list the databases you have by running the following command:

```sql
mysql> show databases;
```

Identify the databases you want to import (for example: `mysql02`, `mysql03`, `mysql04`).

**Note**: RDS Instances do not support importing system databases like `mysql`, `performance_schema`, `information_schema`, and `sys`. Please skip these databases.

Once you have the list of databases to transfer, you can dump the data using the `mysqldump` command with the following format:

```bash
mysqldump -h<Local_DB_IP> -P<Local_DB_Port> -u<Local_DB_User> -p --single-transaction --routines --triggers --databases <Your_DB_List> > dump-database.sql
```

Where:

* **Local\_DB\_IP**: Your MySQL server's IP address.
* **Local\_DB\_Port**: Your MySQL server's port.
* **Local\_DB\_User**: The user on your MySQL server.
* **Your\_DB\_List**: The list of databases you want to dump, separated by spaces. For example: `mysql02 mysql03 mysql04`.

This will generate a file named **dump-database.sql** containing the data to import.

#### 2. Import Data into RDS Instance:

To perform the import, you will use the **Master User** created when you set up the RDS Instance.

You can run the following command:

```bash
mysql -h<RDS_Instance_IP> -P3306 -u<RDS_Instance_Master_User> -p < dump-database.sql
```

Where:

* **RDS\_Instance\_IP**: The IP address of the RDS Instance.
* **RDS\_Instance\_Master\_User**: The Master User assigned when the RDS Instance was created.

Depending on the size of your data, the import process may take some time.

This guide outlines the steps to import data into an RDS Instance with a MySQL/MariaDB datastore. Good luck with your import!
