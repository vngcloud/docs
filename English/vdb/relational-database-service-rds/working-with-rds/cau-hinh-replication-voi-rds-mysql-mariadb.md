# Configuring Replication with RDS (MySQL/MariaDB)

To synchronize data between your MySQL server and the RDS Instance, you can set up MySQL Replication. In this configuration, your MySQL server will act as the Master, and the RDS Instance will act as the Slave Read-Only. After successful configuration, any changes on your MySQL server will be synchronized to the RDS Instance via MySQL Asynchronous Replication.

#### Steps to configure Replication:

***

#### 1. **Create Replication User on Your MySQL Server**

On your MySQL server, create a user to handle the replication:

```sql
mysql> create user 'rep'@'%' identified by 'abcd1234';
mysql> grant replication slave on *.* to 'rep'@'%';
mysql> flush privileges;
```

* `rep` is the replication user.
* `abcd1234` is the password for the user.

***

#### 2. **Check the Binary Log Status on Your DB Server**

MySQL requires binary logs for replication. To check if binary logs are enabled, run the following query:

```sql
mysql> show variables like "log_bin";
```

* If the result is **OFF**, you need to enable the binary log. To do so, add the following lines to the configuration file `my.cnf` (typically located at `/etc/mysql/my.cnf`):

```ini
[mysqld]
log-bin=bin.log
log-bin-index=bin-log.index
max_binlog_size=100M
binlog_format=row
```

Then, restart the MySQL/MariaDB service:

```bash
systemctl restart mysql
```

Check again with:

```sql
mysql> show variables like "log_bin";
```
