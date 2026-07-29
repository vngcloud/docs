# Retry a Transfer Job

During a transfer job run, errors may occur on one file or a set of files. When the transfer job has finished, you can retry it, provided that:

* The **Source**, **Destination**, **Job Information**, and **Job Configuration** are unchanged from the previous run.
* Only the list of **files** whose transfer **status was error**, recorded from the previous run, is transferred.

To retry a Transfer Job:

**Step 1:** Go to [https://datasync.console.greennode.ai/](https://datasync.console.greennode.ai/)

**Step 2:** In the left menu, select **Transfer Job**.

**Step 3:** From the list of created transfer jobs, select the **Transfer Job** that had file errors in its previous run and that you want to retry.

**Step 4:** In the **Error** section, select **View error details**.

**Step 5:** The list of files that failed to transfer is displayed.

**Step 6:** Select the retry icon.

**Step 7:** Select **Retry** to confirm re-running the job.

{% hint style="info" %}
**Note:**

* When you Retry, GreenNode DataSync re-transfers only the previously failed files. Files that were moved successfully before are not moved again.
* You can retry multiple times until all your files have been transferred successfully. However, if retries keep failing, recheck the Transfer Job configuration and the data source.
{% endhint %}
