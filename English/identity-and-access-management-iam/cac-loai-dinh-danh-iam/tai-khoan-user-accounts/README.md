# User Accounts

In VNG Cloud Services, creating IAM user accounts and groups is a straightforward process using the IAM management console. It aims to grant additional users access to services and resources on your account without sharing sensitive security information.

#### User Accounts Management <a href="#useraccounts-useraccountsmanagement" id="useraccounts-useraccountsmanagement"></a>

* **Root user account:** A root user account is an entity that you first create in VNG Cloud and use that has complete access to all VNG Cloud services and resources in the account.
* **IAM user account:** A user account or IAM user account is an entity that represents the person that uses it to interact with VNG Cloud on Portal UI. A user account in VNG Cloud consists of credentials (username, password) and is denied access by default. User accounts are not separate accounts; they are users within the same root user account and they don't need to have a payment method on file with VNG Cloud. Any activity performed by user accounts in your account is billed to your root user account.

**1. How to Create IAM Users?**

To create new IAM user accounts:

1. Navigate to the IAM Console: [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/)
2. Click on **"User account"** in the left-hand menu.
3. Click on **"Create a User account."**
4. Enter the user account details, including the _username and password_.
5. Review the settings and click **"Create User Account"** at the top right corner.

**2. Assign Permission to an IAM user account**

An IAM User Account needs to be attached to at least one Policy or under one Group, which already has at least one attached Policy to ensure the IAM User Account works in the correct concept. To attach Policies to an IAM User Account:

1. Access the IAM Console - User Account page with the URL: [https://hcm-3.console.vngcloud.vn/iam/user-accounts](https://hcm-3.console.vngcloud.vn/iam/user-accounts)
2. Sign in as a **Root user account**. You may need to provide a username and password or use other authentication methods like single sign-on (SSO) if configured.
3. **Search the IAM user account** by entering its username into the search box, and **select the correct one** in the search result.
4. By default, you will see the **Permission** tab on the IAM user account's detailed information.
5. Click on the button **"Attach policies"**, and then you will see an appearing popup that contains all Policies.
6. **Search the existing Policies** by entering the Policies' exact names into the search box.
7. **Check on the records** in the search result and click on the button **"Attach"** at the bottom right of the popup.
8. Now, your IAM User Account will have all the permissions contained in the attached Policies

**3. Assign an IAM user account to a Group**

An IAM User Account needs to be attached to at least one Policy or under one Group, which already has at least one attached Policy to ensure the IAM User Account works in the correct concept. To assign an IAM User Account to User Groups:

1. Access the IAM Console - User Account page with the URL: [https://hcm-3.console.vngcloud.vn/iam/user-accounts](https://hcm-3.console.vngcloud.vn/iam/user-accounts)
2. Sign in as a **Root user account**. You may need to provide a username and password or use other authentication methods like single sign-on (SSO) if configured.
3. **Search the IAM user account** by entering its username into the search box, and **select the correct one** in the search result.
4. Click on the **Group** tab on the IAM user account's detailed information.
5. Click on the button **"Add user to groups"**, and then you will see an appearing popup that contains all Groups.
6. **Check on the records** in the table of the Group list and click on the button **"Add to groups"** at the bottom right of the popup.
7. Now, your IAM User Account has already been assigned to the Group(s) and inherited all attached Permission from the Group(s).

**4. Manage IAM User Account Credentials**

A user account consists of credentials (username, password). You can change your IAM user account's password by following the steps of instruction below:

1. Access the IAM Console - User Account page with the URL: [https://hcm-3.console.vngcloud.vn/iam/user-accounts](https://hcm-3.console.vngcloud.vn/iam/user-accounts)
2. Sign in as a **Root user account**. You may need to provide a username and password or use other authentication methods like single sign-on (SSO) if configured.
3. **Search the IAM user account** by entering its username into the search box, and **select the correct one** in the search result.
4. Click on the **"Security credentials"** tab on the IAM user account's detailed information.
5.  Click on the **"Edit"** button as in the image below

    <figure><img src="https://docs.vngcloud.vn/download/attachments/59806682/Screenshot%202023-07-25%20144222.png?version=1&#x26;modificationDate=1690270959000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
6. An **"Edit password" popup** will be shown for **entering a new one** or clicking on the **"Auto generate"** button to generate a random one.
7. Click on the **"Save"** button after finishing reviewing the new password to save the new one.

**5. How to delete IAM User Accounts?**

You can delete IAM User Account(s) by following 2 options below:

1. **Delete multi IAM User Accounts at once time:**
   1. Access to IAM Console as Root User Account
   2. Click on **"User account"** in the left-hand menu.
   3. Select IAM User Account(s) that you want to delete (a **"Delete" button** will be enabled at the top right corner when you select at least one record)
   4. Click on the **"Delete"** button, a confirm popup will appear to ensure that you don't delete the wrong user(s), then Click on the **"Confirm"** button to complete the process.
2. **Delete an IAM User Account:** We recommend that you should access the detail of the IAM User Account, and then conduct deletion on it to make sure you don't delete the wrong user.
