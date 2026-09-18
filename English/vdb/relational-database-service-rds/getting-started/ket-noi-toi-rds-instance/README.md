# Connect to RDS Instance

To connect to an RDS Instance whose **Database Engine** is **MySQL** or **MariaDB**, you can use any MySQL client such as mysql-client (the CLI client built by MySQL), MySQL Workbench (the GUI client built by MySQL), Heidi, and so on.

For **PostgreSQL**, you can use clients such as psql (the CLI client built by PostgreSQL) or pgAdmin (a popular GUI client).

The guide below uses mysql-client, MySQL Workbench and psql:

* [Step 0. Install a client tool](./#ketnoitoirdsinstance-buoc0.caidatclienttooldeketnoi)
* [Step 1. Identify the Endpoint & Port](./#ketnoitoirdsinstance-buoc1.xacdinhthongtinendpoint-and-portdetruycap)
* [Step 2. Adjust Security Group Rules to protect the DB Instance (optional)](./#ketnoitoirdsinstance-buoc2-tuychinhsecuritygrouprulesdebaovedbinstance-tuychon)
* [Step 3. Connect with client tools](./#ketnoitoirdsinstance-buoc3.ketnoibangcacclienttools)

### Step 0. Install a client tool <a href="#ketnoitoirdsinstance-buoc0.caidatclienttooldeketnoi" id="ketnoitoirdsinstance-buoc0.caidatclienttooldeketnoi"></a>

To install MySQL Workbench (Windows/Linux), download it from MySQL:

[https://dev.mysql.com/downloads/workbench/](https://dev.mysql.com/downloads/workbench/)

To install MySQL-Client (Linux):

Ubuntu:

```bash
sudo apt-get install mysql-client
```

CentOS:

```bash
sudo yum install mysql
```

To install psql (Linux/MacOS):

Ubuntu:

```bash
sudo apt-get install postgresql-client
```

CentOS:

```bash
sudo yum install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-redhat10-10-2.noarch.rpm
sudo yum install postgresql10
```

MacOS:

```bash
brew install libpq
```

### Step 1. Identify the Endpoint & Port <a href="#ketnoitoirdsinstance-buoc1.xacdinhthongtinendpoint-and-portdetruycap" id="ketnoitoirdsinstance-buoc1.xacdinhthongtinendpoint-and-portdetruycap"></a>

On the Database management interface, select the RDS Instance you have just created, go to the **Connectivity & Security** tab and look at the **Endpoint & Port** section.

To tell a **Public Endpoint** from a **Private Endpoint**, check the **Networking** section to find the **Private Network Subnet** of this RDS Instance.

For example, if the DB Instance has the **Private Network Subnet** 10.0.116.0/24, then 10.0.116.3 is the **Private Endpoint**.

### Step 2. Adjust Security Group Rules to protect the DB Instance (optional) <a href="#ketnoitoirdsinstance-buoc2-tuychinhsecuritygrouprulesdebaovedbinstance-tuychon" id="ketnoitoirdsinstance-buoc2-tuychinhsecuritygrouprulesdebaovedbinstance-tuychon"></a>

The **Security Group Rules** section lets you restrict which **Remote IP** addresses may reach your RDS Instance. For convenience, a newly created RDS Instance accepts connections from anywhere (0.0.0.0/0). GreenNode recommends narrowing this down so that only trusted **Remote IP** addresses have access.

* To change it, click **EDIT** and fill in the appropriate IP range (in CIDR notation).
* After editing, click **Save** and wait a moment for the change to take effect.

To make sure the path is open, you can use a tool such as telnet.

Once the connection goes through, you can start connecting to the RDS Instance.

### Step 3. Connect with client tools <a href="#ketnoitoirdsinstance-buoc3.ketnoibangcacclienttools" id="ketnoitoirdsinstance-buoc3.ketnoibangcacclienttools"></a>

Once you have the endpoint, use the **Master User** you created to connect.

Note: the master user is created only once. If you forget the password, select **Action** > **Edit Database** to change it yourself. If you forget the Master User itself, contact **GreenNode Support** for assistance.

For example, if the RDS Instance you just created has master user `dba`, public endpoint 61.28.224.201 and port 3306, you connect as follows:

* On **Linux** (**Ubuntu**, **CentOS**) you can use **mysqlclient** directly (it usually ships with the operating system):

```bash
$ mysql -h 61.28.224.201 -P 3306 -u dba -p
Password
mysql>
```

* On **Windows/Linux/MacOS** you can download **MySQL Workbench** at: [https://dev.mysql.com/downloads/workbench/](https://dev.mysql.com/downloads/workbench/)

#### Workbench

Workbench is the client tool built by MySQL itself, with an intuitive graphical interface. You can also use Workbench on Linux machines (Ubuntu, CentOS).

After downloading and installing Workbench, on the start screen select **Database** > **Connect to Database** and fill in the required information:

* Connection Name: a memorable name for this connection so you can tell it apart from others.
* Hostname: the vDB IP Endpoint, here **61.28.244.201**
* Port: keep the default 3306. (Connecting to the database on another port is not supported.)
* Username: your Master User, here **dba**

Once you are sure the information is correct, click **Test Connection**. A dialog asks for the password; you can tick **Save Password in vault** so Workbench remembers it for later sessions.

Note that if you use Workbench against MariaDB or an older MySQL version, you will see a compatibility warning. You can ignore it and select **Continue Anyway**.

For **PostgreSQL**, use psql with the following syntax and enter the password you registered when creating the vDB:

```bash
psql -h<Endpoint_vDB> -U<master_user> -W -d<Database_Name>
Password:
```

where:

* Endpoint\_vDB: the endpoint used to connect to the vDB.
* Master\_user: the master user you registered at creation time.
* Database\_Name: the Database Name you entered under DB Options. (This differs from the DB Instance Name under DB Settings at creation time, which is what the portal shows under Database.) If you forget it, contact GreenNode Support to retrieve it.

For **PostgreSQL Cluster**, for extra security you can add `sslmode=require` to the connection string, for example: `psql "host=<Endpoint_vDB> port=5432 dbname=<Database_Name> user=<master_user> sslmode=require"`.

If you need any assistance, contact the **GreenNode Support Team**. Thank you for reading this guide.
