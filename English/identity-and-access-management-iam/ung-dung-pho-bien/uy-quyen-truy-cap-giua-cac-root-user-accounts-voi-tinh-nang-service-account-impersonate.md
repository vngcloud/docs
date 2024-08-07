# Authorization for access between root user accounts with Service Account Impersonate feature

When there is a need to decentralize permissions to allow the IAM User Account of one Root User Account to access resources in another Root User Account, you need to use the Impersonate feature of the Service Account. For example, if you have vServer resources in Root User Account B, when you want User Account: System1 of Root User Account A to have the right to manage all vServer resources of Root User Account B, then you use the Impersonate feature. of Service Account, the model is as below:

To set up IAM according to the above model, we will have 2 setup stages at 2 Root User Accounts as follows:

**Stage 1** : Setup at Root User Account B (person who wants to share rights)

* **Step 1.1** : Create Service Account AllowAccessFromRootUserAccountA, assign vServerFullAccess permissions and set up Trust with Root User Account A

**Stage 2** : Setup at Root User Account A (authorized person)

* **Step 2.1** : Create User: System1 if there is no User Account (note that if User: System1 already exists, make sure User: System1 does not have any rights or does not have rights that overlap with the instructions)
* **Step 2.2** : Create Policy: ImpersonateToRootUserAccountB to grant impersonate rights to the Service Account created in stage 1
* **Step 2.3** : Attach Policy: ImpersonateToRootUserAccountB to User: System1 to allow System1 to have the right to use the Service Account created in stage 1
* **Step 2.4** : Log in and check the rights of User: System1

First, to follow the detailed instructions below, you need to collect user ID information of 2 Root User Accounts. To be able to get User ID information, click on the email name in the upper right corner as shown below.

The information of the 2 Root User Accounts in this guide is as follows

**Root User Account A has Email: demoiaas@vng.com.vn, User ID: 53461**

**Root User Account B has Email: iaas.dev4@vng.com.vn, User ID: 60108**

Detailed steps are as follows

**Stage 1: Setup at Root User Account B (person who wants to share rights)**

**Step 1.1: Create Service Account AllowAccessFromRootUserAccountA, assign vServerFullAccess permissions and set up Trust with Root User Account A**

To create a Service Account, go to the Service Account tab on the IAM page here [,](https://hcm-3.console.vngcloud.vn/iam/service-accounts) click **Create a Service Account** , **name** the Service Account: AllowAccessFromRootUserAccountA and click **Add a root user account** to set up Trust with Root User Account A

Fill in the User ID information of Root User Account A to establish **Trust** between Root User Account A and this Service Account, click **Next step**

Search and **select policy: vServerFullAccess, click Create Service Account** to create

Save the Client ID and Secret Key information of the Service Account if you need to use this Service Account directly.

Save the Service Account ID information for setup in stage 2

So you have successfully created Service Account: **AllowAccessFromRootUserAccountA,** have vServerFullAccess rights and set up **Trust** with Root User Account A. With this Trust setup, Root User Account A can grant permissions to 1 IAM User belonging to Root User Account A has the right to use Service Account: **AllowAccessFromRootUserAccountA** to manage vServer under Root User Account B.

**Stage 2: Setup at Root User Account A (authorized person)**

**Step 2.1: Create User: System1 if there is no User Account (note that if User: System1 already exists, make sure User: System1 does not have any rights or does not have rights that overlap with the instructions)**

Create a User Account by accessing the User Account tab on the IAM management page here [,](https://hcm-3.console.vngcloud.vn/iam/user-accounts) clicking **Create a User Account,** filling in Username and Password information, then clicking **Create User Account**

After successfully creating a User Account, it will be listed on the User Account page as below

**Step 2.2: Create Policy: ImpersonateToRootUserAccountB to grant impersonate rights to the Service Account created in stage 1**

To create a Policy, go to the Policy tab on the IAM page here [,](https://hcm-3.console.vngcloud.vn/iam/policies) click **Create a Policy** , **name** the Policy: **ImpersonateToRootUserAccountB** and click **Next step**

Select **Product** : **iam, search and select action: ImpersonateServiceAccount**

Then in the **Resource section,** click on **the Resource arrow** to select Resource information, click **Add a service-account** to add the User ID of Root User Account B and the Service Account ID of AllowAccessFromRootUserAccountA that were collected in stage 1.

**Fill in the User ID information** of Root User Account B and **the Service Account ID** of AllowAccessFromRootUserAccountA that was collected in stage 1 into the displayed Popup.

Then click **Create Policy** to create the Policy

So you have finished creating the Policy to allow Impersonate Service Account: AllowAccessFromRootUserAccountA of User Account B

**Step 2.3: Attach Policy: ImpersonateToRootUserAccountB to User: System1 to allow System1 to have the right to use the Service Account created in stage 1**

After successfully creating Policy: ImpersonateToRootUserAccountB, you proceed to attach this Policy to User: System1, you can do it in User Account or Policy, here we will guide in Policy, **click on the name of the Policy** to go to the details page. Policy details:

**Select the Policy usage tab** and **click Attach** to add User: System1

**Select User: System1** and **click Add**

After adding User: System1 to Policy: ImpersonateToRootUserAccountB, you will see information like below,

At this time, User: System1 has the right to Impersonate Service Account: AllowAccessFromRootUserAccountA to manage Servers under User Account B.

**Step 2.4: Log in and perform Impersonate to check the rights of User: System1**

Now you can log in to User: System1 to check permissions

Access vServer here [,](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) without logging into any account you will be redirected to the sign-in page, select " **Sign-in With IAM User Account** "

Fill in the root user email account information that User: System1 was previously created, IAM username and password information of User: System1, click **Sign-in with IAM User Account**

Perform Impersonate via Service Account: AllowAccessFromRootUserAccountA by **clicking on email** in the upper right corner and selecting **Impersonate service account**

**Fill in Service account ID** of Service Account: AllowAccessFromRootUserAccountA and **display name when Impersonate** , **select Go** to perform Impersonate

Now you see that User: System1 has successfully performed the Impersonate job via Root User Account B (email information: iaas.dev4@vng.com.vn, Account ID: 60108) with Service Account: AllowAccessFromRootUserAccountA

And with full rights on vServer, below is System1 shutting down a server![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs.vngcloud.vn%2Fdownload%2Fattachments%2F59805248%2Fimage2023-7-19\_11-43-21.png%3Fversion%3D1%26modificationDate%3D1689741802000%26api%3Dv2\&width=768\&dpr=4\&quality=100\&sign=9aae750a\&sv=1)

So you have successfully set up to allow User: System1 of Root User Account A to have full rights to manage vServer of Root User Account B.
