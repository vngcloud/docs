# Use case

## Overview

Data backup scenarios using Veeam are typically used in the following cases:

* Data Backup;
* &#x20;Data Recovery;&#x20;
* Ransomware Protection;&#x20;
* Managing Multiple Backup Repositories.

***

## Data Backup

Suppose ABC Corporation has important financial files and folders on their company system server. Therefore, they need to back up these sensitive documents to another secure storage location such as on vStorage (or on systems like Ceph or AWS) outside the existing server.&#x20;

Using Veeam for data backup:

* Set up a storage repository on Veeam;
* Set up a regular backup job for these data;
* You can check the most recent update version on Veeam.

## Data Recovery

Suppose ABC Corporation has been using Veeam for regular backups of critical data. However, one day the server system experiences a severe problem and some data stored on the server is lost. Using Veeam for data recovery:

* Select the job that performed the backup of the data to the storage locations;
* In the list of backup points of the job, choose the appropriate time point to recover data (usually the last time the job was run).

## Ransomware Protection

Suppose ABC Corporation has important documents that need to be stored and is aware of the potential risk of data destruction by Ransomware. The company really wants the data backed up and measures in place to ensure it is safe from dangerous agents like Ransomware. Using Veeam in conjunction with Storage supporting the Object Lock feature:

* The storage needs to create a Bucket/Container that supports Object Lock;
* When creating a Repository, select the option "Make recent backups immutable for (30) days" to activate Immutable to protect against Ransomware;
* The Immutable feature protects backups from being deleted or altered for a certain period.

## Managing Multiple Backup Repositories

Suppose ABC Corporation has been using Veeam for data backup, but now the company has multiple backup repositories spread across various storage locations and is facing difficulties in managing and optimizing storage space.&#x20;

Using Veeam with the Scale-out Backup Repository (SOBR) feature:

* Set up individual Repositories in places as usual;
* Create a Scale-out Repositories, adding individual Repositories to SOBR;
* The company creates jobs with SOBR and only manages a single Repository, which is SOBR;
* If one repository encounters a problem, data can be accessed from other repositories within the SOBR.
