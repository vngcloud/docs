# Getting Start with DataSync

If you have not used any GreenNode services (have not registered an account with GreenNode), you need to register an account with GreenNode Service here to access VNGCloud DataSync. To start using the service, you need to create a transfer job. In DataSync, a transfer job is a task configured to transfer data between a source and a destination. At a time you can own one or more Transfer jobs in parallel and use them for different purposes.

**Getting Started with DataSync, you can follow these steps below:**

**Step 1:** Login into [https://datasync.console.vngcloud.vn/](https://datasync.console.vngcloud.vn/) . If you don't have an account, register for free here.

**Step 2:** Select the button **Create a transfer job** to create a job uses to transfer data.

**Step 3:** Enter the **Basic configuration,** includes:

1. Enter the **Job name** . Job name is the only one on an SSO User Account and the job name can be from a minimum of 5 to 50 characters long.
2. Enter the **Job description** : brief description of the job.
3. Select the **Source Type** you want to transfer data to. GreenNode DataSync currently supports 4 source types:
   * Amazon S3
   * Google Cloud Storage
   * S3 compatible object storage
   * vStorage
4. **Destination type** : currently we only support 1 type of data receiving destination, vStorage.

**Step 4:** Enter the **Source configuration** , including:

**Step 4.1** : In the **Source Information** box , click **Select** . If you choose **Source type** as **vStorage** , you can select source information from the pre-displayed list that we provide. If it is different from this type, you must enter information. Specifically, with source type:

**Case 1: If you choose Source Type as Amazon S3** , you need to:

1. Select a **Region** from the list of Regions supported by Amazon.
2. Enter **Bucket** : enter the name of your source bucket on Amazon S3.
3. Enter **Folder path** : if you only want to transfer data of one folder in the bucket, enter the folder path in this field. For example:

* To move data from bucket01/folder01/subfolder02 to vStorage, you need to enter folder01/subfolder02.
* To transfer all data in bucket01, leave this field blank.

1. Enter **Access Key/ Secret Key** : enter your access key and secret key.

**Case 2: If you choose Source Type as Google Cloud Storage** , you need to:

1. Enter **Bucket** : enter the name of your source bucket on Google Cloud Storage.
2. Enter **Folder path** : if you only want to transfer data of one folder in the bucket, enter the folder path in this field. For example:
   * To move data from bucket01/folder01/subfolder02 to vStorage, you need to enter folder01/subfolder02.
   * To transfer all data in bucket01, leave this field blank.
3. Enter **Access Key/ Secret Key:** enter your access key and secret key.

**Case 3: If you choose Source Type as S3 compatible Object Storage** , you need to:

1. Enter **Region** : where your bucket is located. For example: ap-southeast-1 (Singapore), us-east-1 (Ohio), etc.
2. Enter **Bucket** : the name of your source bucket on S3 compatible Object Storage.
3. Enter **Endpoint** : the endpoint of the S3 compatible Object Storage you are using. For example: [https://s3.example.com](https://s3.example.com/) .
4. Enter **Folder path** : if you only want to transfer data of one folder in the bucket, enter the folder path in this field. For example:
   * To move data from bucket01/folder01/subfolder02 to vStorage, you need to enter folder01/subfolder02.
   * To transfer all data in bucket01, leave this field empty.
5. Enter **Access Key/ Secret Key** : enter your access key and secret key.

**Case 4: If you choose Source Type as vStorage,** you need to:

1. Select **Region** : where your container is located. For example: HCM03
2. Select **Project** : the project containing the container to which you want to transfer data.
3. Select **Container** : the name of your source container on vStorage.
4. Select **Folder path** : if you only want to transfer data of a folder in the container, select the folder you want to transfer data to in this section. For example:
   * To move data from container01/folder01/subfolder02 to vStorage, you need to select folder01 then select subfolder02.
   * To transfer all data in container01, leave this field blank.
5. Enter **Access Key/ Secret Key** : enter your access key and secret key. This S3 key pair is created and managed via IAM, please refer to [IAM for vStorage](../identity-and-access-management-iam/cach-phan-quyen-iam-cho-dich-vu-vng-cloud/iam-cho-vstorage.md) .

**Step 4.2:** After entering all the required information in the sections above, you need to check the connection by clicking the **Test connection** button. At this point, our system will verify the information and display the results. If the connection is successful, you will receive a " **Connection successful** " notification. If the connection fails, you will receive an error notification with a detailed description of the error.

**Step 4.3:** At **Data Filtering** . Click on each box to select the type of filter you want. Filtering aims to move only the objects you really need, saving time and bandwidth, and avoiding moving unwanted objects. Currently, we offer two filter types for you to choose the objects you want to move:

1. Filter Exclude Prefix ( **Select objects not to be transferred based on prefix** ): exclude objects **that do not meet** the specified conditions from the transfer process.
2. Filter Include Prefix ( **Select objects to transfer based on prefix** ): only move objects **matching** the specified conditions.

**Step 5:** Enter the **Destination configuration** , including:

**Step 5.1:** In the **Destination Information** box , click Select. Enter the Destination Configuration, including:

1. Select **Region** : where your container is located. For example: HCM03
2. Select **Project** : the project containing the container to which you want to transfer data.
3. Select **Container** : the name of your source container on vStorage.
4. Select **Folder path** : if you only want to transfer data of a folder in the container, select the folder you want to transfer data to in this section. For example:
   * To move data from container01/folder01/subfolder02 to vStorage, you need to select folder01 then select subfolder02.
   * To transfer all data in container01, leave this field blank.
5. Enter **Access Key/ Secret Key** : enter your access key and secret key. This S3 key pair is created and managed via IAM, please refer to [IAM for vStorage](../identity-and-access-management-iam/cach-phan-quyen-iam-cho-dich-vu-vng-cloud/iam-cho-vstorage.md) .

**Step 5.2:** After entering all the required information in the fields above, you can choose to test the connection by clicking the **Test connection** button. Our system will then verify the validity of the information and display the results. If the connection is successful, you will receive a " **Connection successful** " notification. If the connection fails, you will receive an error message with detailed error descriptions.

**Step 6:** Enter **Job condition** , including:

**Step 6.1: Copy Metadata, Add new tag or Add new metadata**

1. At **Copy Metadata** of object: select if you want to keep the description and properties of the data.
2. Or you can attach new tags or metadata to the entire migration by selecting **Advanced configuration.**
   1. **Case 1: Add more tags** : you need to enter the tag you want to assign to all transferred objects then select **Add** . Repeat the above steps to assign more tags to these objects.
   2.  **Case 2: Add metadata** : you need to enter metadata according to the key:value structure that you want to assign to all transferred objects, then select **Add** . In which:

       1. **Default key** : select a key from the list of available keys we provide.
       2. **Custom key** : create a custom key according to your needs with the prefix X-Object-Meta-Vng-.Add metadata: choose 1 of 2 key types.

       You enter the Value **corresponding** to the selected or created **Key . Select the Add icon.**

**Step 6.1:** At **Choose when to overwrite** : specify the action when the target data already exists:

1. Do not select **Overwrite file** : Keep the destination data intact.
2. **Overwrite file** selected : Replace destination data with source data.

**Step 6.3:** At **Choose when to run** : choose 1 of 2 options

1. **One time** : you choose a specific date and time in the future to run the transfer job.
2. **Run schedule: you choose the start time, end time and schedule run cycle. Specifically:**
   1. Select **Daily** and enter the start time and end time. For example, if you select the start date as 01/01/2024 08:00 and the end date as 01/31/2024, the transfer job will run daily at 08:00. To ensure data accuracy, only run the transfer job the next day if the transfer job for the previous day has completed successfully.
   2. Choose **Weekly** and enter the start time and end time. For example, if you select the start date as 01/01/2024 08:00 and the end date as 01/31/2024, the transfer job will run weekly at 08:00 on 01/01/2024, 01/08/2024, 01/15/2024, 01/22/2024, and January 29, 2024. To ensure data accuracy, only run the transfer job for the next week if the transfer job for the previous week has been completed.
   3. Select **Monthly** and enter the start time and end time. For example, if you choose the start date as 01/01/2024 08:00 and the end date as 03/31/2024, the transfer job will run at 08:00 on 01/01/2024, 02/01/2024, and 03/01/2024. To ensure data accuracy, only run the transfer job for the following week when the transfer job from the previous week has been completed.

**Step 6.4:** In **Job Report** : view detailed reports on the data transfer process:

1. **Report type** : **Summary** or **Standard**
   1. If you choose **Report type** as Summary, you do not need to choose **Report level.**
   2. If you choose **Report type** as **Standard** , you can choose **Report level** as **Successful** , **Failed** or both **Successful and Failed.**
2. Select the Container that contains the reports: by default, the destination container that receives your migration data. You can change to other containers by
   1. Select **Region** : where your container is located. For example: HCM03
   2. Select **Project** : the project containing the container to which you want to transfer data.
   3. Select **Container** : the name of your source container on vStorage.
   4. **Access Key/ Secret Key** : enter your access key and secret key. This S3 key pair is created and managed via IAM, please refer to [IAM for vStorage](../identity-and-access-management-iam/cach-phan-quyen-iam-cho-dich-vu-vng-cloud/iam-cho-vstorage.md) .
3. Once you have entered all the required information in the fields above, you can check the connection by clicking the **Test connection** button. At this point, our system will validate the information and display the results. If the connection is successful, you will receive a " **Connection successful** " message. If the connection fails, you will receive an error message with a detailed description of the error.

**Step 6.5:** Select **Logging Option** if you want to push log transfers to the vMonitor Platform. To perform log pushing, you need at least 1 log project on the vMonitor Platform. For details, refer to Working with Log Project.

**Step 6.6:** Select **Notification Option** to send notifications to your desired email when a transfer job completes. You can enter the email in the correct format and select the **Add** icon.

**Step 7:** Select the button **Create Transfer Job.**
