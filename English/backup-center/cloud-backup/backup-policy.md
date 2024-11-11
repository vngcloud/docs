# Backup Policy

1. **What is Backup Policy?**

A backup policy is a set of rules and standards that define how a system backs up data. It includes details about how often to back up, what data to back up, what types of backups to create, and data retention rules. Simply put, a backup policy is the “blueprint” for your data backup process.

1. **Why is Backup Policy important?**

* **Data protection:** Helps ensure that your data is always secure and recoverable when needed.
* **Optimize resources:** Helps you use storage resources efficiently by backing up only the data you need and retaining backups for a reasonable period of time.
* **Regulatory Compliance:** Make sure your backups comply with data security and storage regulations.

1. **Structure of a Backup Policy**

A backup policy includes the following elements:

* **Backup frequency:**
  * **Hourly:** Hourly backup.
  * **Daily:** Daily backup.
  * **Weekly:** Weekly backup.
  * **Monthly:** Monthly backup.
* **Job run time:** Time to start automatic backup.
* **Rule to retain number of full backups:** Specifies the number of full backups to retain.
* **Rule to create incremental backups between two full backups:** Specifies the number of incremental backups created between two full backups.
* **Backup method:** Specify the backup method (e.g. full backup, incremental backup).
* **Notification:** Notify when the backup process is successful or failed.

1. **How Backup Policy works**
   1. **Schedule:** The system will automatically perform backups according to the schedule configured in the policy.
   2. **Data Backup:** The system will copy data according to the defined rules.
   3. **Data Retention:** The system will automatically delete old backups to ensure compliance with data retention rules.
2. **Example of a Backup Policy**

* **For example, the user installs a policy set as shown below:**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F63oVyvSSuRXyeBV8xnbH%252Fimage.png%3Falt%3Dmedia%26token%3Dfc257a4a-84fa-439d-aa83-347121d61109&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=f8fba1a0&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* **Explain how it works:**

| **Day** | **Launch time** | **Backup type** | **Retention applies** | **Delete backup** | **Note**                                                                                                                                                                                                                |
| ------- | --------------- | --------------- | --------------------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | 1:00            | Full            | Hourly and Daily      | Are not           |                                                                                                                                                                                                                         |
| 1       | 7:00            | Incremental     | Hourly                | Are not           |                                                                                                                                                                                                                         |
| 1       | 13:00           | Incremental     | Hourly                | Are not           |                                                                                                                                                                                                                         |
| 1       | 19:00           | Incremental     | Hourly                | Are not           |                                                                                                                                                                                                                         |
| 2       | 1:00            | Full            | Hourly and Daily      | Are not           | According to retention daily, only 1 full copy is kept. If only retention daily is applied, the first full copy will be deleted. But applying rentention daily (keeping 2 copies, so the first copy will still be kept) |
| 2       | 7:00            | Incremental     | Hourly                | Are not           |                                                                                                                                                                                                                         |
| 2       | 13:00           | Incremental     | Hourly                | Are not           |                                                                                                                                                                                                                         |
| 2       | 19:00           | Incremental     | Hourly                | Are not           |                                                                                                                                                                                                                         |
| 3       | 1:00            | Full            | Hourly and Daily      | Have              | According to retention daily (keep 2 full versions), therefore, the first full version and 3 incremental versions after that full version will be deleted.                                                              |

Above is an example of how the policy works for the first 3 days, the following days will continue to work as set if nothing changes.
