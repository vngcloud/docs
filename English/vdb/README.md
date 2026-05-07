# vDB

GreenNode Database as a Service (vDB) is a service that allows easy setup, operation and expansion of enterprise databases on GreenNode's cloud computing platform. vDB provides the ability to automate tasks such as hardware initialization, database installation, backup and recovery at a cost-effective level. When using vDB, customers can completely focus on building and running their applications.

vDB includes many types of services for each type of database, currently we are providing:

* [Relational Databases Service (RDS)](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vdb/relational-database-service-rds) : includes familiar relational databases such as MySQL, Mariadb, Postgresql.
* [MemoryStore Database Service (MDS)](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vdb/memorystore-database-service-mds) : includes in-memory data storage systems such as Redis, Memcached.

## Benefit <a href="#vdb-database-loiich" id="vdb-database-loiich"></a>

**Easy and simple management**

* vDB makes it easy to deploy and manage a database in the cloud, using an intuitive interface or application programming interface (API) to manage your database in minutes. There is no need to initialize infrastructure, nor do you need to go through complicated installation or configuration steps.

**Flexible scalability**

* You can expand the computing resources (CPU, Memory) and storage resources of the database with just a few simple operations on the interface or call the application programming interface (API), helping to meet the need for rapid expansion.

**Easy data backup and recovery**

* vDB provides automatic daily data backup capabilities to ensure data recovery from backups in the event of a disaster, while also allowing you to create backups according to your needs.

**High performance**

* Enterprise-grade hardware combined with SSD storage gives you the high performance you need.

**Safe**

* vDB makes it easy to control network access to your database, and also allows you to run your database system in a virtual private network (vVPC), which provides many other security features.

**Pay only for what you use**

* vDB can help you optimize resource usage and cost efficiency, you can scale up resources when needed and scale down the system when not needed, you only pay for what you are using.

### Supported Engines

#### Single Mode:

| Engine                   | MySQL             | MariaDB           | PostgreSQL        | Redis              |
| ------------------------ | ----------------- | ----------------- | ----------------- | ------------------ |
| Version                  | 5.7, 8.0          | 10.3, 10.4, 10.5  | 12, 13, 14, 15    | 4.0, 5.0, 6.2, 7.2 |
| Supported AZ             | HCM 1a, 1b, 1c    | HCM 1a, 1b, 1c    | HCM 1a, 1b, 1c    | HCM 1a, 1b, 1c     |
| Multi-AZ Replication     | yes               | yes               | yes               | yes                |
| Auto Failover            | no                | no                | no                | no                 |
| Scale Up Flavor          | yes               | yes               | yes               | yes                |
| Scale Up Storage         | yes               | yes               | yes               | n/a                |
| Scale out (read-replica) | up to 5           | up to 5           | up to 5           | up to 5            |
| Scale out (writer)       | n/a               | n/a               | n/a               | n/a                |
| Configuration Group      | yes               | yes               | yes               | yes                |
| Monitoring               | metric            | metric            | metric            | metric             |
| Backup Method            | Full, Incremental | Full, Incremental | Full, Incremental | Full, Incremental  |
| Auto Backup              | Daily             | Daily             | Daily             | Daily              |
| Integrate vBackup        | no                | no                | no                | no                 |
| Backup Location          | HCM               | HCM               | HCM               | HCM                |
| Authentication           | Username/Password | Username/Password | Username/Password | Password           |
| Encryption at-rest       | no                | no                | no                | no                 |

#### Cluster Mode:

<table><thead><tr><th>Engine</th><th>Kafka</th><th>OpenSearch</th><th>PostgreSQL (New)</th><th data-hidden>Redis (coming soon)</th></tr></thead><tbody><tr><td>Version</td><td>3.6.0, 3.6.1, 3.7.0</td><td>2.15, 2.17</td><td>15, 16, 17</td><td>7.0, 7.1, 7.2</td></tr><tr><td>Supported AZ</td><td>HCM 1a</td><td>HCM 1a, 1b, 1c</td><td>HCM 1a, 1b, 1c</td><td>HCM 1a, 1b, 1c</td></tr><tr><td>Multi-AZ Replication</td><td>no</td><td>no</td><td>coming soon</td><td>coming soon</td></tr><tr><td>Auto Failover</td><td>yes</td><td>yes</td><td>yes</td><td>yes</td></tr><tr><td>Scale Up Flavor</td><td>yes</td><td>yes</td><td>coming soon</td><td>coming soon</td></tr><tr><td>Scale Up Storage</td><td>yes</td><td>yes</td><td>yes</td><td>n/a</td></tr><tr><td>Scale out (read-replica)</td><td>no</td><td>no</td><td>up to 9</td><td>up to 9</td></tr><tr><td>Scale out (writer)</td><td>up to 10</td><td>up to 9</td><td>n/a</td><td>n/a</td></tr><tr><td>Configuration Group</td><td>yes</td><td>no</td><td>yes</td><td>yes</td></tr><tr><td>Monitoring</td><td>metric + log</td><td>no</td><td>coming soon</td><td>coming soon</td></tr><tr><td>Backup Method</td><td>n/a</td><td>n/a</td><td>Full</td><td>Full</td></tr><tr><td>Auto Backup</td><td>n/a</td><td>n/a</td><td>Hourly, Daily, Weekly, Monthly</td><td>Hourly, Daily, Weekly, Monthly</td></tr><tr><td>Integrate vBackup</td><td>no</td><td>no</td><td>yes</td><td>yes</td></tr><tr><td>Backup Location</td><td>n/a</td><td>n/a</td><td>HCM or HAN</td><td>HCM or HAN</td></tr><tr><td>Authentication</td><td>SASL/mTLS</td><td>Username/Password</td><td>Username/Password</td><td>Password</td></tr><tr><td>Encryption at-rest</td><td>yes</td><td>no</td><td>no</td><td>no</td></tr></tbody></table>
