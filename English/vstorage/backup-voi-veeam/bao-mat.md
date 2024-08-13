# Security

## Overview <a href="#baomat-security-tongquan" id="baomat-security-tongquan"></a>

VNG Cloud is responsible for ensuring the security of both its physical and virtual infrastructure that supports VNG Cloud services. Additionally, VNG provides services that allow customers to deploy their security functions for systems hosted on VNG Cloud.

Therefore, backing up data with Veeam software also ensures safety and reduces the risk of intrusion during regular backup processes, with security control measures such as:

* Secure transmission channels during backups
* Data access control
* Multi-factor authentication (MFA)
* Data encryption during transmission
* Control and audit logging

***

## Secure Transmission Channels During Backups

To secure transmission channels for backups, consider the following recommendations:

* Use network segmentation: Create network segmentation policies to control traffic and restrict access to sensitive backup infrastructures. Ensure that only necessary ports are open.
* Isolate backup traffic: Use an isolated network for data transmission between backup infrastructure components.
* Disable outdated network protocols such as SSL 2.0, SSL 3.0, TLS 1.0, TLS 1.1, SMB 1.0, LLMNR, NetBIOS.

***

## Data Access Control

Administrative rights on backup machines only allow user access to backup infrastructure components. If hackers obtain these rights, they can compromise most data and backups. To minimize risk, Veeam segments accounts for backup data management. See the [Access Management](quan-ly-truy-cap.md) section for more details.

***

## Multi-factor Authentication

Veeam software supports Multi-Factor Authentication (MFA) to authenticate users, with OTPs generated in an authentication app on mobile devices used as a verification method. Combined with login information and passwords, this creates a safer environment and protects user accounts from malicious attacks.&#x20;

**Activating MFA:**

1. Log into Veeam as an Administrator;
2. Select the User and Roles, the Security screen appears;
3. The screen lists Users or Groups with corresponding Roles;
4. Choose the option "Enable Multi-factor Authentication (MFA)";
5. Click OK to complete the activation of MFA.

***

## Data Encryption During Transmission

When configuring automatic backup jobs, if data encryption and compression features are enabled, the data source will first compress the data and then encrypt the compressed data blocks. Once encrypted, the data becomes unreadable, and with the support of encryption algorithms and a secret key, hackers cannot open or read the encrypted data. Only those who know the secret key can decrypt and view the data. Data encryption activities include:

* Running data backup jobs;
* Running transaction log backup jobs;
* Running backup copy jobs;

***

## Control and Logging

Veeam provides the capability to log all activities performed, such as data backup tasks or recovery actions in case of incidents.

{% hint style="info" %}
**For example:**

* The list of files restored during Restores. The results of such activity checks are stored in a \*.csv file called audit logs.
{% endhint %}

You can specify the directory where the audit logs will be stored. By default, log files are stored in the following directory: %ProgramData%\Veeam\Backup\Audit.
