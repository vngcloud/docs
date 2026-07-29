# Transfer data from vStorage to vStorage same account

#### **Overview**

Suppose you use vStorage, with your main data storage in region HCM04. Because this data is important, you need to back it up from region HCM04 to another project in region HAN02 within the same account. The transfer runs every month at 09:30 AM from 01/01/2024 to 31/12/2024; logs are stored in the log project `Mylogproject`; and a notification is sent to [example@gmail.com](mailto:example@gmail.com) when the transfer job runs successfully. Details:

* **Source** information: vStorage
  * Region: HCM04
  * Endpoint: [https://hcm04.vstorage.vngcloud.vn](https://hcm04.vstorage.vngcloud.vn)
  * Project: project01
  * Bucket: bucket01
  * Access key: accesskeysource
  * Secret key: secretkeysource
* **Destination** information: vStorage
  * Region: HAN02
  * Endpoint: [https://han02.vstorage.vngcloud.vn](https://han02.vstorage.vngcloud.vn)
  * Project: project02
  * Bucket: bucket02
  * Folder path: backup/fromregionhcm04
  * Access key: accesskeydestination
  * Secret key: secretkeydestination
* **Run:** Monthly at 09:00 AM from 01/01/2024 to 31/12/2024
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

1. Enter the **Job name**. Example: `Transfercungaccount`.
2. Select **Source Type** as **vStorage**.

**Step 4:** Enter the **Source configuration**:

* Select **Region:** HCM04.
* Select **Project:** project01.
* Select **Container:** bucket01.
* Enter **Access key:** accesskeysource.
* Enter **Secret key:** secretkeysource.
* Test the connection: click **Test connection**; the system verifies the information and shows the result ("**Connection successful**" or an error with details).

**Step 5:** Enter the **Destination configuration**:

* Select **Region:** HAN02.
* Select **Project:** project02.
* Select **Container:** bucket02.
* Select **Folder:** backup/fromregionhcm04.
* Enter **Access key:** accesskeydestination.
* Enter **Secret key:** secretkeydestination.
* Test the connection as described above.

**Step 6:** Enter the **Job condition**:

* Select **Run schedule:**
  * **Start date:** 01/01/2024 09:00
  * **End date:** 31/12/2024
  * **Period:** Monthly
* Select **Notification Option**. Enter [example@gmail.com](mailto:example@gmail.com), then click **Add**.

**Step 7:** Select **Create Transfer Job**.
