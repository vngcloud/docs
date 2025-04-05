# Managing RDS Instance Information

**Managing RDS Instance Information**

VNG Cloud vDB provides intuitive dashboards that help you manage your RDS Instances, backups, and configuration groups efficiently and conveniently.

Let’s explore these dashboards:

***

#### A - Database Management Dashboard

This dashboard gives you a complete overview of all current RDS Instances along with detailed information for each. You can create a new database by clicking **CREATE DATABASE**.

When you click on a specific RDS Instance, you can:

* Perform **lifecycle actions** like `START`, `STOP`, `RESTART`, or `DELETE`.
* Edit RDS Instance configuration via **EDIT DATABASE**.
* View detailed configuration info of the selected RDS Instance.

**Edit Database**

Clicking **EDIT DATABASE** takes you to the editing interface where you can:

* **Database Instance Flavor**: Change CPU/Memory configuration and free backup storage quota.
* **Database Instance Storage**: Change storage type (IOPS) and size.
* **Configuration Group**: Attach or detach a Configuration Group.
* **Database Settings**: Update Master User password, enable/disable Public Access (attach/detach Public IP), and toggle automatic daily backup with configurable schedule.

**View Detailed Information**

Each database has the following tabs:

* **CONFIGURATION**: General RDS details including DB name, engine type/version, and computing/storage specs.
* **CONNECTIVITY & SECURITY**: Shows Endpoint & Port info. Every RDS has a Private Endpoint tied to the Cloud Network. If Public Access was enabled during creation, there will also be a Public Endpoint. You can manage access via **Security Group Rules**.
* **BACKUP**: Shows:
  * Whether automatic backups are enabled.
  * Backup schedule.
  * Storage used within the free backup quota.
  * List of all backups (automatic and manual). You can also create a manual backup with the **Create Backup** button.
* **REPLICATION**: Displays master instance and associated slave instances.

***

#### B - Backup Management Dashboard

This dashboard provides a complete overview of all existing backups with details for each.

You can create a **Manual Backup** using the **CREATE BACKUP** button. Upon selecting a backup, you can:

* **RESTORE**: Create a new RDS Instance from the selected backup.
* **DELETE**: Remove the selected backup.

If your **Free Backup Storage Quota** is full, you can purchase additional storage under **Buy Paid Quota**. After purchasing, you can monitor usage, resize, or delete paid backup storage as needed.

***

#### C - Configuration Group Management Dashboard

A Configuration Group is a set of database engine parameters for RDS Instances. Unlike traditional methods requiring file edits and restarts, vDBaaS lets you modify parameters with just a few clicks.

A single Configuration Group can be applied to multiple RDS Instances, making it highly efficient.

This dashboard lists all existing Configuration Groups, compatible database engines and versions, and any linked RDS Instances.

You can:

* Create new Configuration Groups.
* **DELETE** existing ones by selecting them.
* Click on a group name to:
  * View all parameters.
  * **EDIT** them.
  * Apply changes via **APPLY CHANGES** to associated RDS Instances.

For detailed usage, refer to the guide: _"How to Use Configuration Groups."_
