# Access Management

When deploying and managing Server Disaster Recovery (SDR) on GreenNode, setting up access and authorization policies (IAM) is very important to ensure security and tight control of DR-related activities. Refer to the article below to manage access and authorization on SDR.

### 1. Endpoint list <a href="#id-1.-danh-sach-endpoint" id="id-1.-danh-sach-endpoint"></a>

<table data-header-hidden><thead><tr><th width="148"></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Level</strong></td><td><strong>Action</strong></td><td><strong>Describe</strong></td></tr><tr><td>Write</td><td>DrPairAttachServer</td><td>Add master server to DRC</td></tr><tr><td>Write</td><td>DrPairStartReplication</td><td>Initiate the copy process</td></tr><tr><td>Write</td><td>DrPairTestFailover</td><td>Failover test</td></tr><tr><td>Write</td><td>DrPairChangeRecoveryPoint</td><td>Change Recovery Point</td></tr><tr><td>Write</td><td>DrPairCleanTestEnvironment</td><td>Delete failover test environment</td></tr><tr><td>Write</td><td>DrPairCommitFailover</td><td>Confirm failover</td></tr><tr><td>Write</td><td>DrPairDetachServer</td><td>Delete pairing information</td></tr><tr><td>Write</td><td>DrPairFailover</td><td>Failover</td></tr><tr><td>Write</td><td>DrPairRestartReplication</td><td>Restart the copy process</td></tr><tr><td>Write</td><td>DrPairResumeReplication</td><td>Continue copying</td></tr><tr><td>Write</td><td>DrPairStopReplication</td><td>Pause copying</td></tr><tr><td>List</td><td>ListDrPairs</td><td>View pairing list</td></tr><tr><td>Get</td><td>GetDrPair</td><td>View pairing details</td></tr><tr><td>Get</td><td>GetDrPairHistory</td><td>View pairing operation history</td></tr><tr><td>Get</td><td>GetDrPairRecoveryPoints</td><td>View recovery point list</td></tr></tbody></table>

### **2. List of VNG Managed DR Policies** <a href="#iamforvserver-2.danhsachvngmanagedpolicies" id="iamforvserver-2.danhsachvngmanagedpolicies"></a>

VNG Managed Policy is an IAM Policy created by default by the GreenNode IAM system. These Policies are managed by GreenNode itself to support users in quickly setting up the necessary access rights for IAM user accounts for resources of each specific Product. Let's find out the list of VNG Managed Policies for DR:

* [DRFullAccess:](https://iam.console.vngcloud.vn/policies/76de3567-c57c-4167-b304-9133f9af7daf) Includes full access to Disaster Recovery Center resources
* [DRReadOnlyAccess:](https://iam.console.vngcloud.vn/policies/3d44e007-fcd1-4d6f-85b9-f3981ef286a1) Includes Read access only on resources in the Disaster Recovery Center system

### 3. Get Started Using IAM with DRC <a href="#id-3.-bat-dau-su-dung-iam-voi-drc" id="id-3.-bat-dau-su-dung-iam-voi-drc"></a>

This guide is intended to guide users to quickly start using IAM in DRC services by using the default permissions **(defined by GreenNode Managed Policies)** for the DRC system called **DRFullAccess.** However, the features and services at DRC are linked and inherited from vServer, so to be able to delegate permissions on DRC, you need to pay attention to the corresponding permissions of vServer (permissions on Server, Volume, ...)

#### **3.1 Access IAM Console** <a href="#id-3.1-truy-cap-iam-console" id="id-3.1-truy-cap-iam-console"></a>

1. Open your web browser and go to the IAM Console URL: [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/)
2. Log in as a Root User Account or a User Account with access granted. You will need to provide a username/email and password when logging in.
3. Once signed in, you'll see the IAM Console interface, which provides an overview of your IAM configuration.

#### **3.2 Create a new IAM User Account** <a href="#id-3.2-tao-tai-khoan-nguoi-dung-iam-moi" id="id-3.2-tao-tai-khoan-nguoi-dung-iam-moi"></a>

1. Click "Create user" in the left menu.
2. Click "Create a user account."
3. Enter your user account details, including username and password.
4. Review the settings and click "Create user account" in the upper right corner.

#### **3.3 Accessing the DRC Portal with an IAM User Account** <a href="#id-3.3-truy-cap-cong-thong-tin-drc-voi-tai-khoan-nguoi-dung-iam" id="id-3.3-truy-cap-cong-thong-tin-drc-voi-tai-khoan-nguoi-dung-iam"></a>

1. Open your web browser and go to the DRC website URL here:
2. Remember to log out of the Root User account and Log in with the IAM User Account created in step 2.
3. Once logged in, you will see an overview of the DRC website but will not have access to any features.

**Note:**

* **The IAM User account** created in step 3.2 currently does not have permissions to perform actions on the DRC service.
* To grant permissions to the above IAM User Account, refer to the instructions in **Step 3.4 below** . Note that this guide provides an example of **DRFullAccess and vServerFullAccess.**

#### **3.4 Assign Permissions to IAM Accounts** <a href="#id-3.4-gan-quyen-cho-tai-khoan-iam" id="id-3.4-gan-quyen-cho-tai-khoan-iam"></a>

1. Open your web browser and go to the IAM Console URL: [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/)
2. Log in as the **Root User** account . You may need to provide a username and password or use other authentication methods such as single sign-on (SSO) if configured.
3. Once signed in, you'll see the IAM Console interface, which provides an overview of your IAM configuration.
4. Click on **"User account"** in the left menu.
5. Search for an IAM user account by entering the username in the search box.
6. Click the line containing the IAM user account information in the search results.
7. By default, you will see the " **Permission** " tab on the IAM user account details page.
8. Click on the " **Attach policies** " button and then you will see a dialog box appear containing all the Policies.
9. Search for the DRFullAccess and **vServerFullAccess policies** by entering their exact names in the search box.
10. Tick ​​the found result and click the **"Attach"** button in the lower right corner of the dialog box.

**5. Re-access the vServer Portal with the IAM User Account**

Re-access the DRC Portal by following the instructions in Step 3.3, and then you can access all the features on the DRC after assigning the DRFullAccess and vServerFullAccess policies to the IAM user account.
