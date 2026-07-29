# Transfer data from Amazon S3 to vStorage

#### **Overview**

Suppose you use Amazon S3 as your data storage and now need to move this data to vStorage. The transfer runs every day of the week at 09:30 AM from 01/01/2024 to 10/01/2024; the transferred objects are tagged `froms3`; and a notification is sent to `example@gmail.com` when the transfer job runs successfully. Details:

* **Source** information: Amazon S3
  * Region: ap-southeast-1
  * Endpoint: [https://s3.amazonaws.com](https://s3.amazonaws.com)
  * Bucket: bucket-source
  * Access key: accesskeysource
  * Secret key: secretkeysource
* **Destination** information: vStorage
  * Region: HCM03
  * Endpoint: [https://hcm03.vstorage.vngcloud.vn](https://hcm03.vstorage.vngcloud.vn)
  * Project: project01
  * Bucket: container01
  * Access key: accesskeydestination
  * Secret key: secretkeydestination
* **Run:** Daily at 09:00 AM from 01/01/2024 to 10/01/2024
* **Tag:** fromS3
* **Email notification:** [example@gmail.com](mailto:example@gmail.com)

***

#### **Prerequisites**

To ensure a successful transfer, make sure the Source and Destination information is valid, where:

* The **Access key and Secret key** at the Source must have at least read permission.
* The **Access key and Secret key** at the Destination must have at least read and write permission.

***

#### **Create the Transfer Job**

**Step 1:** Log in to [https://datasync.console.greennode.ai/](https://datasync.console.greennode.ai/). If you don't have an account, [register for free](https://register.vngcloud.vn/signup).

**Step 2:** Click **Create a transfer job** to start creating a data transfer job.

**Step 3:** Enter the **Basic configuration**:

1. Enter the **Job name**. Example: `Transfer from S3`.
2. Select **Source Type** as **Amazon S3**.

**Step 4:** Enter the **Source configuration**:

* Select **Region:** ap-southeast-1.
* Enter **Bucket:** bucket-source.
* Enter **Access Key:** accesskeysource.
* Enter **Secret Key:** secretkeysource.
* After entering all the information above, you can click **Test connection** to verify it. The system checks the validity and displays the result. If successful, you receive a "**Connection successful**" message; if it fails, you receive an error message with a detailed description.

**Step 5:** Enter the **Destination configuration**:

* Select **Region:** HCM03.
* Select **Project:** project01.
* Select **Container:** container01.
* Enter **Access key:** accesskeydestination.
* Enter **Secret key:** secretkeydestination.
* Test the connection as described above.

**Step 6:** Enter the **Job condition**:

* Select **Advanced configuration**. Enter `froms3`, then select **Add**.
* Select **Run schedule:**
  * **Start date:** 01/01/2024 09:00
  * **End date:** 10/01/2024
  * **Period:** Daily
* Select **Notification Option**. Enter [example@gmail.com](mailto:example@gmail.com), then click **Add**.

**Step 7:** Select **Create Transfer Job**.

