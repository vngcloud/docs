# Run a Transfer Job

After creating a Transfer Job, you can start running the task to transfer data. Each run of a transfer job is called a task.

**To run a Transfer Job, follow the instructions:**

**Step 1:** Login into [https://datasync.console.vngcloud.vn/](https://datasync.console.vngcloud.vn/transfer-job/list)

**Step 2**: In the left menu, select **Transfer Job**.&#x20;

**Step 3**: On the list of created transfer jobs, select the **Transfer Job** you want to run.

**Step 4:** Select the icon or select the icon then select the action

Now you can select that transfer job to see details about the transfer job's parameters when running. For details, please refer to Monitoring the results of running Transfer Job

{% hint style="info" %}
**Note:**

* To ensure successful data transfer, you need to ensure valid Source and Destination information, including:&#x20;
  * The Access key and Secret key at the Source must have at least the right to read data.&#x20;
  * The Access key and Secret key at Destination must have at least the right to read and write data.&#x20;
* Transferring large amounts of data in one transfer job run can affect transfer job performance and execution time. To increase speed as well as improve system stability, we recommend that you split the data set through the Data Filtering feature (Filter Include Prefix, Filter Exclude Prefix) to help reduce system load and push Fast data migration process. Let's say you have a transfer job transferring 100GB of data from Amazon S3 to vStorage. Transfer can take a long time and affect the system. You can split the data into 10 parts, each part 10GB. Then, use the Data Filtering feature to transfer each individual piece of data.
{% endhint %}
