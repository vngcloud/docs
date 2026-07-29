# Transfer data from vStorage to vStorage cross account

#### **Overview**

Suppose you were initially using **account1** on vStorage, with your main data storage in region HCM04. You have now created **account2** in region HAN02 and want to move this data to region HAN02 for more efficient access. The transfer runs once, at the moment you click to run the Transfer Job.

* **Source** information: vStorage
  * Account: account01
  * Region: HCM04
  * Endpoint: [https://hcm04.vstorage.vngcloud.vn](https://hcm04.vstorage.vngcloud.vn)
  * Project: project01
  * Bucket: bucket01
  * Access key: accesskeysource
  * Secret key: secretkeysource
* **Destination** information: vStorage
  * Account: account02
  * Region: HAN02
  * Endpoint: [https://han02.vstorage.vngcloud.vn](https://han02.vstorage.vngcloud.vn)
  * Project: project02
  * Bucket: bucket02
  * Folder path: backup/fromregionhcm04
  * Access key: accesskeydestination
  * Secret key: secretkeydestination

***

#### **Prerequisites**

To ensure a successful transfer, make sure the Source and Destination information is valid, where:

* The **Access key and Secret key** at the Source must have at least read permission.
* The **Access key and Secret key** at the Destination must have at least read and write permission.

***

#### **Create the Transfer Job**

**Step 1:** Log in to [https://datasync.console.greennode.ai/](https://datasync.console.greennode.ai/). If you don't have an account, [register for free](https://register.vngcloud.vn/signup). **Note: you must log in with account02 to transfer data from account01 to account02.**

**Step 2:** Click **Create a transfer job** to start creating a data transfer job.

**Step 3:** Enter the **Basic configuration**:

1. Enter the **Job name**.
2. Select **Source Type** as **S3 compatible object storage**.

**Step 4:** Enter the **Source configuration**:

* Enter **Region:** HCM04.
* Enter **Bucket:** bucket01.
* Enter **Endpoint:** [https://hcm04.vstorage.vngcloud.vn](https://hcm04.vstorage.vngcloud.vn)
* Enter **Access Key:** accesskeysource.
* Enter **Secret Key:** secretkeysource.
* Test the connection: click **Test connection**; the system verifies the information and shows the result ("**Connection successful**" or an error with details).

**Step 5:** Enter the **Destination configuration**:

* Select **Region:** HAN02.
* Select **Project:** project02.
* Select **Container:** bucket02.
* Select **Folder:** backup/fromregionhcm04.
* Enter **Access key:** accesskeydestination.
* Enter **Secret key:** secretkeydestination.
* Test the connection as described above.

**Step 6:** Select **Create Transfer Job**.

**Step 7:** At the time you want, select **Run** to run the job.
