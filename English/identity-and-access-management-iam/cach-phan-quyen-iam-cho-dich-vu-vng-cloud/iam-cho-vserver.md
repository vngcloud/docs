# IAM for vServer

IAM is essential to protecting resources within vServer services. Without proper access control, unauthorized users can access sensitive data or disrupt critical operations. IAM helps enforce the principle of least privilege, minimizing potential attack surfaces and protecting your server resources from unauthorized access and data compromise.

### 1. Getting Started with IAM&#x20;

This guide is intended to guide users to quickly get started with IAM in vServer services by using the default permission (defined by GreenNode Managed Policies) for the vServer system called vServerFullAccess.

1. Accessing the IAM Console&#x20;

* Open your web browser and access the IAM Console URL: https://iam.console.vngcloud.vn/
* Log in as a Root User Account or a User Account with access rights. You will need to provide a username/email and password when logging in.&#x20;
* After logging in, you will see the IAM Console interface, which provides an overview of your IAM configuration.

2. Create a new IAM User Account&#x20;

* Click "Create user" in the left menu
* Click "Create a user account."&#x20;
* Enter the user account details, including username and password.&#x20;
* Review the settings and click "Create user account" in the upper right corner.

3. Access the vServer Portal with the IAM User Account&#x20;

* Open your web browser and go to the vServer website URL: https://hcm-3.console.vngcloud.vn/vserver/&#x20;
* Remember to log out of the Root User account and log in with the IAM User Account created in step 2.&#x20;
* After logging in, you will see an overview of the vServer website.&#x20;
* Try to access the Network, Server, Bock store, Load balancer, Container & Billing pages, you will see a notification about limited permissions as below.

Notice

* The IAM User Account created in Step 2 does not currently have permissions to perform actions on the vServer cloud service.&#x20;
* To grant permissions to the above IAM User Account, refer to the instructions in Step 4 below. Note that this guide provides an example of vServerFullAccess.

**4.** Assign Permissions to IAM Accounts&#x20;

* Open your web browser and go to the IAM Console URL: https://iam.console.vngcloud.vn/
* Log in as the Root User account. You may need to provide a username and password or use other authentication methods such as single sign-on (SSO) if configured.&#x20;
* Once logged in, you will see the IAM Console interface, which provides an overview of your IAM configuration.&#x20;
* Click on "User account" in the left menu.
* Search for an IAM user account by entering the username in the search box.&#x20;
* Click on the row containing the IAM user account information in the search results.&#x20;
* By default, you will see the "Permission" tab on the IAM user account details page.&#x20;
* Click on the "Attach policies" button and then you will see a dialog box appear containing all the Policies.&#x20;
* Search for the vServerFullAccess policy by entering its exact name in the search box.&#x20;
* Tick the result and click the "Attach" button in the lower right corner of the dialog box.

**5.** Re-Access the vServer Portal with an IAM User Account&#x20;

Re-Access the vServer Portal by following the instructions in Step 3, and then you can access all sections of the vServer Portal after assigning the vServerFullAccess policy to the IAM user account.

### 2. List of VNG Managed Policies&#x20;

VNG Managed Policy is an IAM Policy created by default by the GreenNode IAM system. These Policies are managed by GreenNode itself to support users in quickly setting up the necessary access rights for IAM user accounts for resources of each specific Product. Let's explore the list of VNG Managed Policies for vServer:&#x20;

* vServerFullAccess: Includes full access rights to resources in the vServer system
* vServerReadOnlyAccess: Includes only Read rights on resources in the vServer system
* vLBFullAccess: Includes full access rights to resources in the Load Balancer service
* vLBReadOnlyAccess: Includes only Read rights on resources in the Load Balancer service

### **3.** Explore IAM for vServer in Detail  <a href="#iamforvserver-3.khamphachitietcachsudungiamchovserver" id="iamforvserver-3.khamphachitietcachsudungiamchovserver"></a>

Learn more about IAM for vServer: Identity and Access Management (IAM) for vServer&#x20;

Learn more about IAM:&#x20;

* IAM Identity&#x20;
* Common Use Cases for IAM

### &#x20;<a href="#iamforvserver-3.khamphachitietcachsudungiamchovserver" id="iamforvserver-3.khamphachitietcachsudungiamchovserver"></a>
