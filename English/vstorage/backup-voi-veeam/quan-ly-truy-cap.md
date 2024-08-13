# Access Management

## Overview

VNG Cloud is committed to protecting the infrastructure of VNG Cloud services, especially data storage services. Access control is one of the top priorities, including the use of Veeam software for data backup.

Access control is a crucial aspect of security aimed at determining who and under what conditions can access the software and perform backup or recovery operations.&#x20;

In addition to user-based access control that allows software usage, Veeam also ensures the security of backup and data recovery actions with a Four-Eyes Authorization mechanism. This article will describe user access rights and four-eyes authentication below.

## Access Rights

The access control policy based on Veeam's regulations with different roles is designed to manage user access and rights to various system features. Here is the definition and comparison of roles:

<table><thead><tr><th width="79">No.</th><th width="258">Roles</th><th>Description</th></tr></thead><tbody><tr><td>1</td><td><strong>Veeam Backup Administrator</strong></td><td>Allows for the execution of <strong>all administrative operations</strong> within Veeam Backup &#x26; Replication. Note that this role has full access to all files on the servers and hosts added to the backup infrastructure.</td></tr><tr><td>2</td><td><strong>Veeam Restore Operator</strong></td><td><p>Allows for the <strong>execution of recovery operations</strong> using existing backups and replicas. However, this role cannot migrate a restored VM back into the production environment during Instant Recovery.</p><p>Consider the following: </p><ul><li>This role can restore data from any backup. This enables them to restore disks and files that may contain malicious content created specifically. This opens the possibility for insider attacks, including but not limited to privilege escalation leading to the takeover of the entire system. Due to this capability, this role should be considered as sensitive as Veeam Backup Administrators. </li><li>During the recovery process, this role can overwrite existing versions: virtual machines during VM recovery, disks during disk recovery, and files during file-level recovery.</li></ul></td></tr><tr><td>3</td><td><strong>Veeam Backup Operator</strong></td><td>Can <strong>start and stop</strong> existing jobs, export backups, copy backup copies, and create VeeamZip backups.</td></tr><tr><td>4</td><td><strong>Veeam Backup Viewer</strong></td><td>Only has <strong>read-only access</strong> to Veeam Backup &#x26; Replication. Can view the list of existing jobs and view details of job sessions.</td></tr><tr><td>5</td><td><strong>Veeam Tape Operator</strong></td><td>Can <strong>manage tapes</strong> and perform the following operations: rescan library/server, eject tape, export tape, import tape, mark tape as free, move tape to media pool, erase tape, catalog tape, inventory tape, set tape password, copy tape, verify tape, start and stop tape backup jobs.</td></tr></tbody></table>

{% hint style="info" %}
You can **assign multiple roles to the same user**. For example, if a user needs the ability to start jobs and perform recovery operations, you can assign the roles of Veeam Backup Operator and Veeam Restore Operator to this user.
{% endhint %}

To manage access permissions and for instructions on adding users, please refer to the following official Veeam documentation: [https://helpcenter.veeam.com/docs/backup/vsphere/configuring\_users.html?ver=120](https://helpcenter.veeam.com/docs/backup/vsphere/configuring\_users.html?ver=120)

## Four Eyes Authorization

You can activate this function to reduce the risk of accidental actions affecting sensitive stored data. This function uses an additional control mechanism that requires further approval from another user with the Veeam Backup Administrator role for specific operations in Veeam.

{% hint style="info" %}
Before activating this function, ensure that there are at least two users assigned the role of Veeam Backup Administrator.
{% endhint %}

To activate and review the operations of the Veeam Backup Administrator role, please refer to the following official Veeam documentation: [https://helpcenter.veeam.com/docs/backup/vsphere/four\_eyes\_authorization.html?ver=120](https://helpcenter.veeam.com/docs/backup/vsphere/four\_eyes\_authorization.html?ver=120)
