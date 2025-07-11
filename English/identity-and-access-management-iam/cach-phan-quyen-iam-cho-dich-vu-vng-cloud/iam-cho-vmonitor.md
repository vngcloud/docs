# IAM for vMonitor

IAM is essential to protecting resources within vMonitor services. Without proper access control, unauthorized users can access sensitive data or disrupt critical operations. IAM helps enforce the principle of least privilege, minimizing potential attack surfaces and protecting your server resources from unauthorized access and data compromise.

### 1. Getting Started with IAM&#x20;

This guide is intended to guide users to quickly get started with IAM in vMonitor services by using the default permission (defined by VNG Cloud Managed Policies) for the vMonitor system called vStorageFullAccess.

1. Accessing the IAM Console&#x20;

* Open your web browser and access the IAM Console URL: https://iam.console.vngcloud.vn/
* Log in as a Root User Account or a User Account with access rights. You will need to provide a username/email and password when logging in.&#x20;
* After logging in, you will see the IAM Console interface, which provides an overview of your IAM configuration.

2. Create a new IAM User Account&#x20;

* Click "Create user" in the left menu
* Click "Create a user account."&#x20;
* Enter the user account details, including username and password.&#x20;
* Review the settings and click "Create user account" in the upper right corner.

3. Access the vMonitor Portal with the IAM User Account&#x20;

* Open your web browser and go to the vMonitor website URL: [https://console.vstorage.vngcloud.vn/ ](https://vmonitor.console.vngcloud.vn/)
* Remember to log out of the Root User account and log in with the IAM User Account created in step 2.&#x20;
* After logging in, you will see an overview of the vMonitor website.&#x20;
* Try to access the Network, Server, Bock store, Load balancer, Container & Billing pages, you will see a notification about limited permissions as below.

Notice

* The IAM User Account created in Step 2 does not currently have permissions to perform actions on the vMonitor cloud service.&#x20;
* To grant permissions to the above IAM User Account, refer to the instructions in Step 4 below. Note that this guide provides an example of vMonitorFullAccess.

**4.** Assign Permissions to IAM Accounts&#x20;

* Open your web browser and go to the IAM Console URL: https://iam.console.vngcloud.vn/
* Log in as the Root User account. You may need to provide a username and password or use other authentication methods such as single sign-on (SSO) if configured.&#x20;
* Once logged in, you will see the IAM Console interface, which provides an overview of your IAM configuration.&#x20;
* Click on "User account" in the left menu.
* Search for an IAM user account by entering the username in the search box.&#x20;
* Click on the row containing the IAM user account information in the search results.&#x20;
* By default, you will see the "Permission" tab on the IAM user account details page.&#x20;
* Click on the "Attach policies" button and then you will see a dialog box appear containing all the Policies.&#x20;
* Search for the vMonitorFullAccess policy by entering its exact name in the search box.&#x20;
* Tick the result and click the "Attach" button in the lower right corner of the dialog box.

**5.** Re-Access the vMonitor Portal with an IAM User Account&#x20;

Re-Access the vMonitor Portal by following the instructions in Step 3, and then you can access all sections of the vMonitor Portal after assigning the vMonitorFullAccess policy to the IAM user account.

### **2. List of VNG Managed Policies** <a href="#iamforvstorage-2.danhsachvngmanagedpolicies" id="iamforvstorage-2.danhsachvngmanagedpolicies"></a>

VNG Managed Policy is an IAM Policy created by default by the VNG Cloud IAM system. These Policies are managed by VNG Cloud itself to support users in quickly setting up the necessary access rights for IAM user accounts for resources of each specific Product. Let's find out the list of VNG Managed Policies for vMonitor :

* vMonitorFullAccess: Includes full access to resources in the vMonitor system&#x20;
* vMonitorMetricPush: Includes only permissions related to Push Metric&#x20;
* vMonitorMetricNormalAccess: Includes full access to resources of type Metric (except for Billing related actions)&#x20;
* vMonitorMetricReadOnlyAccess: Includes only Read permissions to Metric resources.&#x20;
* vMonitorMetricFullAccess: Includes full access to resources of type Metric&#x20;
* vMonitorSyntheticReadOnlyAccess: Includes only Read permissions to Synthetic resources.&#x20;
* vMonitorSyntheticNormalAccess: Includes full access to Synthetic resources (except Billing related actions)&#x20;
* vMonitorSyntheticFullAccess: Includes full access to Synthetic resources&#x20;
* vMonitorNotificationReadOnlyAccess: Includes only Read access to Notification resources.&#x20;
* vMonitorNotificationFullAccess: Includes full access to Notification resources&#x20;
* vMonitorLogNormalAccess: Includes full access to Log resources (except Billing related actions)&#x20;
* vMonitorLogReadOnlyAccess: Includes only Read access to Log resources.&#x20;
* vMonitorLogFullAccess: Includes full access to Log resources&#x20;
* vMonitorBillingFullAccess: Includes full access to vMonitor - Billing page&#x20;
* vMonitorDashboardReadOnlyAccess: Includes only Read access to vMonitor - Dashboard page.&#x20;
* vMonitorDashboardFullAccess: Includes full access to the vMonitor - Dashboard page

### **3.** Explore IAM for vMonitor in Detail  <a href="#iamforvserver-3.khamphachitietcachsudungiamchovserver" id="iamforvserver-3.khamphachitietcachsudungiamchovserver"></a>

Learn more about IAM for vMonitor : Identity and Access Management (IAM) for vMonitor&#x20;

Learn more about IAM:&#x20;

* IAM Identity&#x20;
* Common Use Cases for IAM
