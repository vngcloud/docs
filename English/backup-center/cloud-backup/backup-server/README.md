# Backup Server

**Backup Server** is a specialized service that protects system data by creating and storing backups automatically and periodically. This service provides a comprehensive solution to protect data from unexpected incidents such as hardware failure, software errors, network attacks, or natural disasters.

## Mechanism of action <a href="#co-che-hoat-dong" id="co-che-hoat-dong"></a>

**1. Backup Location:**

* **Function:** This is where backups (Backup Server Points) created from Backup Servers are stored.
* **Features:**
  * **Location Lock:** Prevents accidental deletion of backups, ensuring data integrity.
  * **Soft Delete:** When a backup is deleted, it is stored for a certain period of time (retention day) before being permanently deleted, providing an opportunity to recover data if needed.

**2. Backup Server:**

* **Function:** Acts as a backup plan.
* **Operation:** To back up a server, the user needs to create a corresponding Backup Server. The Backup Server will be configured with parameters such as:
  * **Backup Policy:** Specifies the automatic backup schedule.
  * **Backup Location:** Specify where to store backups.
* **Objective:** Ensure that server data is backed up regularly and securely.

**3. Backup Policy:**

* **Function:** Manage and set up automatic running schedules of Backup Servers.
* **Configuration:** Users can customize the backup schedule according to their needs, for example, daily, weekly, monthly, or on a custom schedule.

**4. History:**

* **Function:** Stores all activities related to Backup Server service, including:
  * **Backup Server Run History:** Records the start time, end time, and results of each backup.
  * **Restore History:** Records data restores from backups.
  * **Backup Location Edit History:** Records changes to the configuration of the storage location.
* **Purpose:** Provide a detailed log of system activities, helping users monitor and manage the backup process effectively.

## Benefits of Backup Server and Backup Location <a href="#loi-ich-tu-backup-server-va-backup-location" id="loi-ich-tu-backup-server-va-backup-location"></a>

Backup Server and its accompanying features such as Backup Location, Lock, Soft Delete, and Cross-region storage are a comprehensive data protection solution that helps businesses minimize the risk of data loss, increase system availability, and ensure compliance with security regulations.

**1. Comprehensive data protection**

* **Fast data recovery:** In case of data loss, restoring from backup will be quick, helping businesses quickly return to normal operations.
* **Prevent permanent data loss:** Backups are stored in a separate location, protecting data from risks like hardware failure, accidental deletion, or ransomware attacks.
* **Regulatory Compliance:** Ensure compliance with data storage and security regulations, especially for industries with high security requirements such as finance and healthcare.

**2. Advanced Backup Location feature**

* **Cross-region storage:**
  * **Disaster protection:** Storing backups in multiple geographic regions helps minimize the risk of data loss due to natural disasters or infrastructure failures in one area.
  * **Increased availability:** Even if one region fails, data is still securely protected in other regions.
* **Lock and Soft Delete Features:**
  * **Protect data from accidental deletion:** Lock feature prevents deletion of important backups, ensuring data integrity.
  * **Restore deleted data:** Soft Delete feature allows to restore deleted backups within a certain period of time, avoiding unnecessary data loss.
* **Ransomware Prevention:**
  * **Prevent data encryption:** Backups are stored in a separate location, not directly accessible from the system under attack, helping to prevent ransomware from encrypting all data.
  * **Recover data quickly:** After removing the ransomware, businesses can quickly restore data from backups.

**3. Cost benefits and high availability**

* **Increased system availability:** Having backups available helps minimize system downtime when a problem occurs.
* **Reduced Costs:** Compared to building a separate backup system, using a Backup Server service is often lower cost and easier to manage.
* **Increased productivity:** IT staff can focus on other tasks instead of managing backup systems.
