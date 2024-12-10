# Create a RDS Instance

To initialize RDS Instacne, you can refer to the detailed steps in the instructions below.

### Access vDB Portal <a href="#truy-cap-vdb-portal" id="truy-cap-vdb-portal"></a>

First, you access the vDB service interface in 2 ways as follows:

* Method 1: Access the VNG Cloud homepage at the link: [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/) . At the main interface, you find the **vServer service and select the vDB Relational** service in the list of vServer products/services.
* Method 2: Directly access the vDB Relational homepage at the link: [https://vdb.console.vngcloud.vn/relational/database](https://vdb.console.vngcloud.vn/relational/database)

### Initialize RDS instance <a href="#khoi-tao-rds-instance" id="khoi-tao-rds-instance"></a>

At the Database management interface, click **Create Database** . The initialization process will go through 6 parts as instructed below:

* **Step 1 Basic configuration:** You choose the desired **Database Name** and **Database Engine .**
* **Step 2 Specifications:** You can customize configuration information, engine license, engine version as follows
  * **Engine License** : license to use the database, can be community or enterprise version (depending on the type of database).
  * **Engine Version** : database version.
  * **Flavor** : RDS Instance configuration, including number of cores, amount of RAM and included Free Backup capacity. Note: if the total capacity of all your backups exceeds this quota, you will have to pay additional costs for the backup capacity exceeding the quota.
  * **Storage type** : type of hard drive storage.
  * **Storage Size** : hard drive size for storing data (including database data and logs).
* **Step 3 Install DB version:** you choose
  * **Master username** : you will use this user to administer the database instance.
  * **Master password** : password of master user. VNG Cloud recommends that you set a strong password and store this password in a safe place. To ensure information security, the password must meet all of the following minimum requirements:
    * Password must be between 8-32 characters long.
      * Allowed characters include: AZ, az, 0-9 and special characters.
      * Allowed special characters include: !#$%&()\*+-.:<=>?@\[]^\_{|}\~
      * Password must start with an alphabetic character: AZ or az.
      * Password cannot start or end with special characters.
* **Step 4 Network and Security:** In **Network & Security** , you select
  * **The Cloud Network (VPC & Subnet)** that will be used for this RDS Instance. Every RDS Instance must be connected to a Cloud Network. If you do not have a Cloud Network, you can create a new Cloud Network with the instructions [here](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc) .
  * **Public Access:** If you want RDS Instance to have Public IP and be accessible from the Internet, you need to enable Public **Accessibility . If you want RDS Instance to have only Private IP and only Cloud Servers can access it, you need to disable Public** Accessibility.

**Note** : The choice of whether or not Public Accessibility is only selected once at this initialization time. You cannot change this setting later. For enhanced security, VNG Cloud allows you to limit the trusted IP addresses allowed to access each RDS Instance through **Security Group Rules** .

* **Step 5 DB Options:** In **DB Options** , you can configure
  * **Database Name** : Select the database name that will be automatically created.
  * **DB configuration group** (optional): Select the Configuration Group that will be applied to this RDS Instance. If you do not need to customize the configuration, you can skip this field.
* **Step 6 Backup settings:** In the **Backup** section , you can configure:
  * **Automatic daily backup** : enable/disable the feature to automatically create daily backups at a pre-selected time.
  * **Backup retention period** : the period of time for storing automatic backups. Automatic backups that are stored beyond this period will be automatically deleted from the system. This parameter does not affect the life cycle of backups that you create manually.
  * **Backup time** : the time to create automatic backups. VNG Cloud recommends that you configure this time at the time of day with the lowest system traffic, usually from 12AM - 5AM.

After configuring, in the **Summary** section on the right, you review the information, when all information is correct, you click **Create Database** to complete the process **.** During the initialization process, RDS Instance will have the status **Building** or **Build** . If the initialization is successful, RDS Instance will have the status **Active** .

**Note** :

By default, the RDS Instance created will have 3 users available:

* 2 system users are root@localhost & [os\_admin@127.0.0.1](mailto:os_admin@127.0.0.1) .
* 1 master user helps you access and manage RDS Instance.

Two system users are created for VNG Cloud to serve automatic tasks such as creating backups, configuring replication, restoring... and you do not need to care about these users. However, deleting these two system users will cause system errors for RDS Instance and make the above features ineffective. VNG Cloud will not be responsible if you try to delete the two system users but will still support you as best as possible to restore them for you.
