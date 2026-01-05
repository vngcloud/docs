# Identity Providers

An Identity Provider is a feature that allows you to manage resources on GreenNode using a user directory from your organization's authentication system. It enables centralized user management without the need to create additional IAM user accounts on GreenNode. IAM supports the SAML 2.0 protocol for integration with authentication systems and currently supports Azure AD.

#### Why Use an Identity Provider?

To better understand how IAM Identity Provider works and the benefits it brings to businesses, we present a specific use case for a clearer picture:

**Context**

Company A has 10 employees managed via Microsoft accounts named nhanvien1 to nhanvien10.

Company A is structured into 3 departments: Administration & Accounting, IT, and Sales.

Company A uses GreenNode services, including vServer, vStorage, and vMonitor.

**Requirements**

* **Single Sign-On (SSO):** Simplify access to GreenNode using a single enterprise account.

**Solution**

Using the Identity Provider feature we provide will help your company save time and simplify permission management and user identity within the GreenNode system. Refer to the following guide to address your company’s needs.

***

#### How to Use Identity Provider?

To use the Identity Provider, follow these steps:

1. **Set up the Identity Provider from the third-party provider (Azure AD).**
2. **Configure the Identity Provider connection on GreenNode.**
3. **Access Azure AD to configure the connection to GreenNode IAM using the SAML Entity ID and Reply URL.**
4. **Once setup is complete, use the Login URL in IAM to sign in to GreenNode with your enterprise’s Azure AD account.**

***

#### 1. Set Up Identity Provider from the Third-Party Provider (Azure AD)

Currently, GreenNode IAM only supports Azure AD via the SAML 2.0 protocol. To set up the Identity Provider between GreenNode and Azure AD, follow these steps:

* Go to the Azure homepage: [https://portal.azure.com/#home](https://portal.azure.com/#home)
* Click on **“Azure Active Directory”** in the left menu. Note: You must have permission to access your organization’s Azure AD.
* Under the **Enterprise Applications** tab, click **“New application”**, then **“Create your own application”**, name the app, and click **Create** (as shown in the example image).

**Note:**

* The created application corresponds to the IT department.
* Add IT department users to the application, such as nhanvien1 and nhanvien2.
* After creating the application, go to the **Single sign-on** section and select **SAML protocol**.

Next, copy the **Login URL** (as shown) and proceed with the connection setup from GreenNode to Azure AD (see Step 2 below).

***

#### 2. Configure Identity Provider Connection from GreenNode

After obtaining the Login URL from Azure AD, proceed with the following steps:

* Visit IAM Identity Provider at: [https://iam.console.vngcloud.vn/identity-providers](https://iam.console.vngcloud.vn/identity-providers)
* Click **Add an Identity Provider**
* Fill in the following information:
  * **Provider Name**: Name of the Identity Provider
  * **Provider Type**: Leave as default (only SAML is supported)
  * **Vendor**: Leave as default (currently only Azure AD is supported)
  * **Login URL**: Paste the Login URL obtained from Step 1
* Click **Create** to create the Identity Provider

Once created, you will receive the **SAML Entity ID** and **Reply URL** as shown. Proceed to Step 3 to complete the setup.

***

#### 3. Configure Connection from Identity Provider to GreenNode IAM using SAML Entity ID and Reply URL

After obtaining the SAML Entity ID and Reply URL, return to Azure AD and follow these steps:

* Open the previously created app
* Go to **Single sign-on**, then click **Edit** in the **Basic SAML Configuration** section
* Enter the SAML Entity ID and Reply URL from Step 2 into the appropriate fields and click **Save**

***

#### Notification

After completing Steps 1 to 3, the connection between Azure AD and GreenNode IAM is successfully established.

Continue to Step 4 to use the IAM Login URL (skip if you already know how to use this feature).

***

#### 4. Use IAM Login URL to Sign in to GreenNode Using Enterprise Azure AD Account

After setup, enterprise users can use the VNG Login URL (shown below) to sign in to GreenNode with their Azure AD account. The IAM system will automatically create a user account upon login, which will have no default permissions like other IAM user accounts.

**Note:**

* Only **nhanvien1** and **nhanvien2** can sign in to GreenNode via the login URL.
* They must log in for the first time using the login URL for the system to automatically create IAM User Accounts with corresponding usernames.
* By default, newly created IAM User Accounts for **nhanvien1** and **nhanvien2** will have no permissions on the GreenNode system.
* Therefore, the **Root User Account** representing the company must access the IAM Console to assign access permissions to these two IAM User Accounts.

Once permissions are granted, **nhanvien1** and **nhanvien2** will be able to access GreenNode services (vServer, vStorage, and vMonitor).
