# Monitor Transfer Job Results

When your Transfer Job is running or has finished running, you can view its detailed parameters as follows:

**Step 1:** Go to [https://datasync.console.greennode.ai/](https://datasync.console.greennode.ai/)

**Step 2:** In the left menu, select **Transfer Job**.

**Step 3:** From the list of transfer jobs that have run or are running, select the **Transfer Job** you want to view.

**Step 4:** The Transfer Job detail screen appears, where:

**Step 4.1 — Check the information in General Information**

1. **Job ID:** the job's ID.
2. **Job Description:** the job description.
3. **Job Schedule:** the run-once / recurring-schedule configuration of the job.
4. **Source Information:** information about the data source.
5. **Destination Information:** information about the data destination.

**Step 4.2 — Check the information in Operation**

The run history of the Transfer Job is displayed, including:

* **Latest run:** the most recent past run (if the transfer job is not currently running) or the real-time result of the current run. In this section, you can view:
  * **Status:** status of the Transfer Job run.
  * **Duration:** total run time of the job.
  * **Start time:** the time the job started.
  * **End time:** the time the job ended.
  * **Progress:** the job's progress; this value updates in real time based on the actual results of the running transfer job.
  * **Data transferred:** total number of bytes and files transferred by the DataSync system. Note: not all of these bytes/files are transferred successfully — errors may occur on one or more files during transfer. You can view this list in the section below.
  * **Error:** total number of bytes and files that failed during transfer. You can retry the transfer job with this file list following the guide at [Retry a Transfer Job](chay-lai-transfer-job.md).
  * **Data skipped:** total number of files skipped during transfer.
  * **Average speed estimate:** the system's average bandwidth during transfer.
* **Run history:** results of the transfer job's past runs. Click the icon on each run to view the detailed result of that run. The displayed parameters are the same as in the **Latest run** section above.

**Step 4.3 — Check the information in Monitor**

Statistical charts of the data transfer process are displayed. Every 60 seconds, we collect metrics into one data point; for more on working with them, refer to [_Working with Metric Information_](../../../vmonitor-platform/cach-tinh-nang-cua-vmonitor-platform/metrics/lam-viec-voi-metruc-information.md). You can also choose a time range to view the chart. On GreenNode DataSync, the metrics displayed via charts include:

* **Data throughput** (byte/s): number of bytes transferred per second.
* **File throughput** (file/s): number of files transferred per second.
* **Object transfer error** (file): number of files that failed during transfer.

**Step 4.4 — Check the information in Configuration**

The Transfer Job's configuration is displayed, including:

* **Source:** source details — Source type, Region, Project name, Bucket name, Endpoint, Folder path, Access key.
* **Destination:** destination details — Destination type, Region, Project name, Container name, Folder path, Access key.
* **Job condition:** whether Copy object metadata is on/off, whether Overwrite is on/off, and the Tags, Metadata, Job Report storage location, Log destination, and Notification email you configured on the Transfer Job.
