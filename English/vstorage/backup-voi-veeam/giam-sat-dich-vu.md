# Monitoring Service

## Overview



Monitoring and tracking backup and data recovery activities is an important part of storage solutions. When using Veeam, processes such as synchronization (running jobs) or data recovery are visually displayed with progress updates and result notifications. Additionally, to monitor backup activities and recoveries from past backups and recoveries, you can use Veeam's History function, and for a visual management of stored data, you can use S3 Browser to monitor the stored data:

* **History:** Tracks backup and recovery activities.
* **Versions & Event Log:** Monitors versions and interactions with the backed-up data.

***

## History - Tracking backups and recoveries

This is a feature in Veeam Backup & Replication that displays statistics for activities performed with Veeam:

* Job: Lists all jobs with information on the most recent data backup time for that job (indicating whether the backup was successful or failed);
* Restore: History of all data recovery attempts (indicating whether recovery was successful or failed);
* System: History of all sessions stored in the configuration database;

## Versions & Event Log

To check backup data versions, you can view them in the storage where data has been backed up (vStorage, AWS, etc.). This article mentions another simple way to monitor this information on the S3 Browser.

After installing and accessing the Storage Account, at the Bucket/Container where data has been backed up, you can see the necessary tabs for tracking backup activities:

* Versions: Lists all versions of the backed-up data and indicates when each data backup occurred;
* Event Log: Lists all tasks that have successfully updated the bucket/container.

**Example**

In cases where **Immutable** has been enabled to protect data;&#x20;

If there is a data incident, such as deleting a version, then the Event Log records a "Delete" task but will also record "Access Denied" denying the data deletion.

&#x20;At this point, as an administrator, you can see all existing versions and the tasks performed interacting with the backed-up data.
