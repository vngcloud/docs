# Access Management

## Access account <a href="#tai-khoan-truy-cap" id="tai-khoan-truy-cap"></a>

On the File Storage system, you can use 2 types of accounts to access File Storage. Details of these 2 types include:

* **Root user account: Is the** [first initial](https://register.vngcloud.vn/signup) account to access VNG Cloud with full access to all resource services on VNG Cloud.
* **IAM user account:** Is an account created through the IAM system and used to operate through the File Storage Portal.

### Root user account <a href="#root-user-account" id="root-user-account"></a>

#### **Create Root User Account**

To create a Root user account, please register an account at the registration page [https://register.vngcloud.vn/signup](https://register.vngcloud.vn/signup) .

After you create a Root user account, you collect the following information to access and work with resources using the Root user account:

* The email address used to create the Root user account.
* Password for the Root user account.

***

#### **Cancel Root User Account**

To cancel your Root account, you need to contact us by creating a ticket to request account cancellation. For more details, see [Account Cancellation Instructions](https://docs.vngcloud.vn/vng-cloud-document/v/vn/huong-dan-su-dung-tai-khoan/huong-dan-huy-tai-khoan) .

### IAM user account <a href="#root-user-account-1" id="root-user-account-1"></a>

#### **Create IAM User Account**

To create an IAM user account, please first refer to the instructions below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/) with Root User Account.
2. Select **User Account** .
3. Select **Create a User Account.**
4. In the **Account username** section , enter **the Account username** you want. The IAM User Account name must be from 5 (minimum) to 50 (maximum) characters long and can only include uppercase letters, lowercase letters (az, AZ), numbers (0-9), periods (.), underscores (\_), and hyphens (-). The IAM User Account name should not contain sensitive information (e.g. IP address, login password, etc.) and the IAM User Account name must be unique on a VNG Cloud account until that IAM User Account is deleted. For example, the following IAM User Account name is valid: IAM\_Phong\_kinh\_doanh\_01.
5. Select **Add a username** .
6. In the **Account password** section , you can:
   1. Enter your desired **password** . Password must be between 8 (minimum) and 50 (maximum) characters long and must include at least 1 uppercase letter (A-Z), 1 lowercase letter (a-z), 1 number (0-9), and 1 special character (!@#$%,...).
   2. Select **Auto-generate** if you want the system to automatically generate a password for you.
7. Select **Copy** to copy the password. You must collect this information to access File Storage using an IAM User Account.
8. Select **Create User Account.**

<figure><img src="../../../.gitbook/assets/image (39) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

#### **Create a policy for IAM user account**

To initialize a policy used to access File Storage resources, follow the steps below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/) with Root User Account.
2. **Select the Policy** folder .
3. Select **Create a Policy** .
4. Enter **Name** and **Description** if given for Policy.
5. Select **Next step** .
6. Select **Product as file-storage** .
7. Select **Actions** :
   1. Select **Allow permissions** : by default, the vIAM system will always be on, which means allowing permissions to be applied to the policy. If you turn this mode off, the system will deny (reverse) the corresponding permissions.
      1. **Allow permissions** : allow access according to the selected action.
      2. **Deny permissions** : deny access according to the selected action.
   2. Select **All file storage actions** if you want to create a policy that has the right to perform all actions on File Storage. For details on the meaning of the actions, please refer to [File Storage Features, Resources and Access Rights.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/filestorage/quan-ly-truy-cap/tinh-nang-tai-nguyen-file-storage-va-quyen-truy-cap)
8. Select **Resources** :
   1. Select **All resources** if you want the access selected above to be allowed to access all resources on your SSO account.
   2. Select **Specify resources** : select the specific storage id file that you want to allow access to. You can enter information for each of these resources in one of the following ways:
      1. **Enter \*** if you want to select all resources.
      2. **Enter the specific ID of the storage file** if you want to point to that exact storage file.
   3. You can also select **Any** to allow access to all file storage in your SSO account.
   4. Select **Request conditions:** enter special conditions for the policy if any.

After you have completed the above 8 steps, the file storage policy has been created. Next, you need to assign it to your IAM User Account.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### **Attach IAM User Account with corresponding policy**

Once you have created the desired IAM User Account and Policy, you will need to link the IAM User Account to the policy as per the instructions below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/) with Root User Account.
2. Select the User Account folder **.**
3. Select **the IAM User Account** you want to assign permissions to.
4. Select **Attach policies** .
5. Select the **policies** you want. The vIAM system supports you to assign multiple policies to an IAM User Account. If these policies contain independent permissions, they will complement each other (ie the permission list is merged). On the contrary, if these policies contain conflicting permissions, you will not be able to access the corresponding resources according to this permission list (ie the permission list is merged and when conflicting, they will cancel each other out).
6. Select **Attach** .

## Access Management <a href="#quan-ly-truy-cap" id="quan-ly-truy-cap"></a>

### Access resources using Root user account <a href="#truy-cap-tai-nguyen-su-dung-root-user-account" id="truy-cap-tai-nguyen-su-dung-root-user-account"></a>

Follow the steps below to log in to File Storage with the Root user account:

1. Access the File storage service login page: [https://signin.vngcloud.vn.](https://signin.vngcloud.vn/ap/auth?clientId=c9e78411-f2a2-41ba-a9e4-3c56263c181a\&responseType=code\&codeChallenge=f09ybYi-GTZYYwuHVRv2f1UPRhjM_wI-0J_aXpbUsv4\&codeChallengeMethod=S256\&appState=55eab53a-30f3-43ae-837b-bf3a469dd9db\&redirectUri=https%3A%2F%2Fdashboard.console.vngcloud.vn%2F)
2. The main login page will appear. Select **LOG IN WITH ROOT USER** .
3. **Enter the email** address and **password** associated with your account and select **Sign In** . If you previously signed in as the root user in this browser, your browser may remember the email address for the Root User Account. If so, you will see the screen shown in the next step. If you previously signed in as an IAM user using an IAM User Account in this browser, your browser may display the IAM user login page instead. To return to the main login page, select **LOG IN AS ROOT USER.**
4. After successfully logging in, you have full access and perform the features provided by the File storage service on your resources.

### Access resources using IAM user account <a href="#truy-cap-tai-nguyen-su-dung-iam-user-account" id="truy-cap-tai-nguyen-su-dung-iam-user-account"></a>

Follow the steps below to log in to File storage with an IAM user account:

1. Access the File storage service login page: [https://signin.vngcloud.vn.](https://signin.vngcloud.vn/ap/auth?clientId=c9e78411-f2a2-41ba-a9e4-3c56263c181a\&responseType=code\&codeChallenge=f09ybYi-GTZYYwuHVRv2f1UPRhjM_wI-0J_aXpbUsv4\&codeChallengeMethod=S256\&appState=55eab53a-30f3-43ae-837b-bf3a469dd9db\&redirectUri=https%3A%2F%2Fdashboard.console.vngcloud.vn%2F)
2. The main login page will appear. Select **LOG IN WITH IAM USER ACCOUNT** .
3. Enter the Root user's **email** address when registering for a VNG Cloud account.
4. Enter **the username** and **password** of the IAM user account created on the vIAM system.
5. Select **LOG IN WITH IAM USER ACCOUNT** . If you have previously logged in as an IAM user account in this browser, your browser may remember the address of the IAM user account. If so, you will see the screen displayed in step 3. After successfully logging in with the IAM user account, the main screen of File storage will show the type of user you are using to log in (Root user account or IAM user account).
6. After successfully logging in, you have the right to access and perform the features provided by the File storage service on the resources authorized to you.
