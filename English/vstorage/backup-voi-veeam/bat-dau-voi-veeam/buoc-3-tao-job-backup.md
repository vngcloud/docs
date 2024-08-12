# Bước 3: Create Job backup



After[ initializing the Repository](buoc-2-khoi-tao-repository.md), you will proceed to create an automatic backup job to vStorage. Creating a backup job allows you to set up a regular automatic backup to the storage (repository). If you create a job running on a Scale-out Repository, it means that running the job can backup to multiple locations.

### Follow these steps to create a Backup Job:

1. In the "Inventory" section, select "**Backup Job**" choose the appropriate type of computer;
2. In the "Job Mode" screen, click "**Next**";
3. In the "Name" screen, you can name the Job, then click "**Next**";
4. In the "Computer" screen, select the computer you want to backup, then click "**Next**";
5. In the "Backup Mode" screen, select a mode then click "**Next**";

* Choose "**Entire Computer**" to backup the entire computer, if you select this mode you can skip step 6.
* Choose "**File level backup (slower)**" to backup selected files or folders, if you select this mode then proceed to step 6.

6. In the "Object" screen, select the objects to be backed up, then click "**Next**";
7. In the "Storage" screen, select the Repository, then click "**Next**";
8. In the "Guest Processing" screen, deselect all options, then click "**Nex**t";
9. In the "Schedule" screen, you can set up a periodic backup schedule, then click "**Apply**";
10. In the "Summary" screen, if you choose "Run the job when I click Finish" to run the backup when the Job creation is successful, then click "**Finish**" to let the system create and run the synchronization job.

***

### Installation guide video

Updating

***

### Example: Guide to Creating a Job with Veeam Backup & Replication Version 12

**Step 1**: Users go to the **Inventory** section, select Object - Computer (infrastructure to be backed up), in this guide localhost is the Object to be backed up, then right-click on the Object to select "Add to backup job" and press "**New Job**".

<figure><img src="../../../.gitbook/assets/image (257).png" alt="" width="563"><figcaption></figcaption></figure>

**Step 2:** The **New Agent Backup Job** interface appears, in the **Job Mode** tab, the user selects the Mode "**Managed by backup server**", then press **Next**.

<figure><img src="../../../.gitbook/assets/image (258).png" alt="" width="563"><figcaption></figcaption></figure>

**Step 3:** In the **Name** tab, the user names the Job, then presses **Next**.

<figure><img src="../../../.gitbook/assets/image (259).png" alt="" width="563"><figcaption></figcaption></figure>

**Step 4:** In the **Computer** tab, the user can choose the computer to perform the backup. Then press **Next**.

<figure><img src="../../../.gitbook/assets/image (260).png" alt="" width="563"><figcaption></figcaption></figure>

**Step 5:** In the **Backup Mode** tab, the user chooses the mode "**File level backup (slower)**" to backup only selected files or folders, or if backing up the entire computer then choose the mode "Entire computer". Then press **Next**.

<figure><img src="../../../.gitbook/assets/image (261).png" alt="" width="563"><figcaption></figcaption></figure>

**Step 6:** If the "File level backup (slower)" mode is chosen in step 5, then the **Object** tab appears to select the objects to backup, the user chooses the option "**The following file system objects**:", then press "Add" to enter the path of the folder to backup, then press "OK" and finally press **Next**.&#x20;

\*If "Entire computer" mode is chosen in step 5, skip step 6.

<figure><img src="../../../.gitbook/assets/image (262).png" alt="" width="563"><figcaption></figcaption></figure>

**Step 7:** In the **Storage** tab, the user selects the previously created **Backup Repository**, then press **Next**. The system will check the backup file.

<figure><img src="../../../.gitbook/assets/image (263).png" alt="" width="563"><figcaption></figcaption></figure>

**Step 8:** After the system finishes checking, navigate to the **Guest Processing** tab, the user **deselects the first option "Enable application-aware processing"**. If the user wants to ensure consistent backups for applications running on virtual servers by interacting with them and using Microsoft VSS, then it can still be enabled and Veeam will have to perform pre and post backup tasks. Then press **Next**.

<figure><img src="../../../.gitbook/assets/image (264).png" alt="" width="563"><figcaption></figcaption></figure>

**Step 9:** In the **Schedule** tab, the user can set the schedule to run the job automatically, if running manually then press **Next**.

<figure><img src="../../../.gitbook/assets/image (265).png" alt="" width="563"><figcaption></figcaption></figure>

**Step 10:** In the Summary tab, the user can see a summary of the Job information to be created, choose "**Run the job when I click Finish**" then press **Finish** for the system to start creating the Job.

<figure><img src="../../../.gitbook/assets/image (266).png" alt="" width="563"><figcaption></figcaption></figure>

**Step 11:** After the job is created, the user can check by: going to the Home section, select Jobs/Backup, select the created Job if the status is Success then the job has been created, the user can perform the backup.

<figure><img src="../../../.gitbook/assets/image (267).png" alt="" width="563"><figcaption></figcaption></figure>

Complete the process of creating a Job to backup data.
