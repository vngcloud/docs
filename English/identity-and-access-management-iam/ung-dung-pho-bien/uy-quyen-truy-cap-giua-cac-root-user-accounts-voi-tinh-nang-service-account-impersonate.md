# Authorization for access between root user accounts with Service Account Impersonate feature

When there is a need to delegate permissions to an IAM User Account of a Root User Account to access resources in another Root User Account, you need to use the Impersonate feature of the Service Account. For example, if you have resources from the vServer in Root User Account B, and you want User Account: System1 from Root User Account A to have management rights over all vServer resources of Root User Account B, you would use the Impersonate feature of the Service Account, modeled as follows:\
To set up IAM according to the model above, we will have 2 setup stages in 2 Root User Accounts as follows:

**Step 1: Set up at Root User Account B (the person who wants to share the rights)**&#x20;

* Step 1.1: Create Service Account AllowAccessFromRootUserAccountA, attach vServerFullAccess rights and set up Trust with Root User Account A&#x20;

**Step 2: Set up at Root User Account A (the authorized person)**&#x20;

* Step 2.1: Create User: System1 if there is no User Account (note that if there is already User: System1, make sure User: System1 does not have any rights or does not have rights that overlap with the instructions)&#x20;
* Step 2.2: Create Policy: ImpersonateToRootUserAccountB to grant impersonate rights to the Service Account created in step 1&#x20;
* Step 2.3: Attach Policy: ImpersonateToRootUserAccountB to User: System1 to allow System1 to have the right to use the Service Account created in step 1 Step 2.4: Log in and check the rights of User: System1

First, to follow the detailed instructions below, you need to collect the user ID information of 2 Root User Accounts. To get the User ID information, click on the email name in the upper right corner as shown below. The information of 2 Root User Accounts in this guide is as follows.

**Root User Account A has Email: demoiaas@vng.com.vn, User ID: 53461.**

**Root User Account B has Email: iaas.dev4@vng.com.vn, User ID: 60108.**

Detailed steps are as follows.

**Stage 1: Set up at Root User Account B (the person who wants to share rights).**

* Step 1.1: Create Service Account AllowAccessFromRootUserAccountA, attach vServerFullAccess rights and set up Trust with Root User Account A.

To create a Service Account, go to the Service Account tab on the IAM page here, click Create a Service Account, name the Service Account: AllowAccessFromRootUserAccountA and click Add a root user account to set up establish&#x20;

Trust with Root User Account A Fill in the User ID information of Root User Account A to establish Trust between Root User Account A and this Service Account, click Next step Search and select policy: vServerFullAccess, click Create Service Account to create Save the Client ID and Secret Key information of the Service Account if you need to use this Service Account directly.&#x20;

Save the Service Account ID information to set up in phase 2&#x20;

Thus, you have successfully created Service Account: AllowAccessFromRootUserAccountA, with vServerFullAccess rights and established Trust with Root User Account A, with this Trust establishment, Root User Account A can grant permission to 1 IAM User belonging to Root User Account A to have the right to use Service Account: AllowAccessFromRootUserAccountA to manage vServer belonging to Root User Account B.

**Step 2: Set up at Root User Account A (authorized person)**&#x20;

* Step 2.1: Create User: System1 if there is no User Account (note that if there is already a User: System1, make sure User: System1 has no rights or does not have rights that overlap with the instructions)&#x20;

Proceed to create a User Account by accessing the User Account tab on the IAM management page here, click Create a User Account, fill in the Username and Password information, then click Create User Account&#x20;

After successfully creating a User Account, it will be listed on the User Account page as below&#x20;

* Step 2.2: Create Policy: ImpersonateToRootUserAccountB to grant impersonate rights to the Service Account created in step 1&#x20;

To create a Policy, go to the Policy tab on the IAM page here, click Create a Policy, name the Policy: ImpersonateToRootUserAccountB and click Next step Select Product: iam, search and select action:&#x20;

ImpersonateServiceAccount&#x20;

Then in the Resource section, click on the arrow at Resource to select Resource information, click Add a service-account to add the User ID of Root User Account B and the Service Account ID of AllowAccessFromRootUserAccountA that were collected in phase 1 Enter the User ID information of Root User Account B and the Service Account ID of AllowAccessFromRootUserAccountA that were collected in phase 1 into the Popup that is displayed

Then click Create Policy to create Policy Thus, you have completed creating a Policy to allow Impersonate Service Account: AllowAccessFromRootUserAccountA of User Account B&#x20;

* Step 2.3: Attach Policy: ImpersonateToRootUserAccountB to User: System1 to allow System1 to have the right to use the Service Account created in phase 1&#x20;

After successfully creating Policy: ImpersonateToRootUserAccountB, you proceed to attach this Policy to User: System1, you can do it in User Account or Policy, here we will guide in Policy, click on the name of the Policy to go to the Policy details page:

Select the Policy usage tab and click Attach to add User: System1 Select User: System1 and click Add After adding User: System1 to Policy: ImpersonateToRootUserAccountB, you will see the information as below, Now User: System1 has the right to Impersonate Service Account: AllowAccessFromRootUserAccountA to manage Servers belonging to User Account B

* Step 2.4: Log in and perform Impersonate to check the rights of User: System1&#x20;

Now you can log in to User: System1 to check the rights Access vServer here, when you have not logged in to any account, you will be redirected to the sign-in page, select "Sign-in With IAM User Account" Fill in the root user account email information that User: System1 previously created, the IAM username and password information of User: System1, click Sign-in with IAM User Account&#x20;

Perform Impersonate via Service Account: AllowAccessFromRootUserAccountA by clicking on the email in the upper right corner and selecting Impersonate service account&#x20;

Enter the Service Account ID of the Service Account: AllowAccessFromRootUserAccountA and the display name when Impersonate, select Go to perform Impersonate&#x20;

Now you see that User: System1 has successfully performed Impersonate through Root User Account B (email information: iaas.dev4@vng.com.vn, Account ID: 60108) with Service Account: AllowAccessFromRootUserAccountA And has full rights on vServer, below is System1 is shutting down 1 server&#x20;

Thus, you have successfully performed the setup to allow User: System1 belonging to Root User Account A to have full rights to manage vServer of Root User Account B.
