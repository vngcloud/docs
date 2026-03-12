# Access Management

## Access Accounts <a href="#tai-khoan-truy-cap" id="tai-khoan-truy-cap"></a>

On the vDB service, you can use 2 types of accounts to access OpenSearch. Details of these 2 types include:

* **Root user account:** This is the [first account created](https://register.vngcloud.vn/signup) to access GreenNode with full access to all resource services on GreenNode.
* **IAM user account:** This is an account created through the IAM system and used to operate through the vDB Portal.

### Root user account <a href="#root-user-account" id="root-user-account"></a>

#### **Create Root User Account**

To create a Root user account, please register at the registration page [https://register.vngcloud.vn/signup](https://register.vngcloud.vn/signup).

After creating the Root user account, collect the following information to access and work with resources using the Root user account:

* The email address used to create the Root user account.
* The password for the Root user account.

***

#### **Cancel Root User Account**

To cancel a Root account, you need to contact us by creating a ticket requesting account cancellation. For more details, see [Account Cancellation Guide](https://docs.vngcloud.vn/vng-cloud-document/v/vn/huong-dan-su-dung-tai-khoan/huong-dan-huy-tai-khoan).

### IAM user account <a href="#root-user-account-1" id="root-user-account-1"></a>

#### **Create IAM User Account**

To create an IAM user account, please first refer to the guide below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/) with your Root User Account.
2. Select **User Account**.
3. Select **Create a User Account.**
4. In the **Account username** field, enter your desired **Account username**. The IAM User Account name must be between 5 (minimum) and 50 (maximum) characters long and can only include uppercase and lowercase letters (a-z, A-Z), numbers (0-9), periods (.), underscores (\_), and hyphens (-). The IAM User Account name should not contain sensitive information (e.g., IP addresses, login passwords,...) and the IAM User Account name must be unique within a GreenNode account until that IAM User Account is deleted. For example, the following IAM User Account name is valid: IAM\_Sales\_Department\_01.
5. Select **Add a username**.
6. In the **Account password** field, you can:
   1. Enter your desired **password**. The password must be between 8 (minimum) and 50 (maximum) characters long and must include at least 1 uppercase letter (A-Z), 1 lowercase letter (a-z), 1 number (0-9), and 1 special character (!@#$%,...).
   2. Select **Auto-generate** if you want the system to automatically create a password for you.
7. Select **Copy** to copy the password. You must collect this information to access vDB OpenSearch using the IAM User Account.
8. Select **Create User Account.**

***

#### **Create policy for IAM user account**

To create a policy for accessing vDB OpenSearch resources, follow the steps below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/) with your Root User Account.
2. Select the **Policy** folder.
3. Select **Create a Policy**.
4. Enter **Name** and **Description** for the Policy.
5. Select **Next step**.
6. Select **Product as vdb-opensearch**.
7. Select **Actions**:
   1. Select **Allow permissions**: by default, the vIAM system will always enable this, meaning permissions are allowed to be applied on the policy. If you disable this mode, the system will deny (reverse) the corresponding permissions.
      1. **Allow permissions**: allows access according to the selected action.
      2. **Deny permissions**: denies access according to the selected action.
   2. Select **All vdb-opensearch actions** if you want to create a policy with permission to perform all actions on vDB OpenSearch. For detailed action descriptions, please refer to [Features, OpenSearch Cluster Resources and Access Rights](tinh-nang-tai-nguyen-opensearch-cluster-va-quyen-truy-cap.md).
8. Select **Resources**: Select **All resources** if you want the selected access permissions to be allowed to access all resources on your SSO account.

After completing these 8 steps, the policy for OpenSearch cluster has been created. Next, assign it to the IAM User Account.

<figure><img src="../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Link IAM User Account with corresponding policy**

After you have created the IAM User Account and desired Policy, you need to link the IAM User Account to the policy following the guide below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/) with your Root User Account.
2. Select the **User Account** folder.
3. Select the **IAM User Account** you want to assign permissions to.
4. Select **Attach policies**.
5. Select the **policies** you want. The vIAM system supports attaching multiple policies to a single IAM User Account. If these policies contain independent permissions, they will complement each other (i.e., permission lists are merged). Conversely, if these policies contain conflicting permissions, you will not be able to access the corresponding resources according to these permission lists (i.e., permission lists are merged and when conflicting, they cancel each other out).
6. Select **Attach**.

## Access Management <a href="#quan-ly-truy-cap" id="quan-ly-truy-cap"></a>

### Access resources using Root user account <a href="#truy-cap-tai-nguyen-su-dung-root-user-account" id="truy-cap-tai-nguyen-su-dung-root-user-account"></a>

Follow the steps below to log in to vDB OpenSearch with a Root user account:

1. Access the vDB OpenSearch login page: [https://signin.vngcloud.vn.](https://signin.vngcloud.vn/ap/auth?clientId=c9e78411-f2a2-41ba-a9e4-3c56263c181a\&responseType=code\&codeChallenge=f09ybYi-GTZYYwuHVRv2f1UPRhjM_wI-0J_aXpbUsv4\&codeChallengeMethod=S256\&appState=55eab53a-30f3-43ae-837b-bf3a469dd9db\&redirectUri=https%3A%2F%2Fdashboard.console.vngcloud.vn%2F)
2. The main login page will appear. Select **LOG IN WITH ROOT USER**.
3. Enter the **email** address and **password** linked to your account and select **Log in**. If you previously logged in as root user in this browser, your browser may remember the email address for the Root User Account. If so, you will see the screen shown in the next step. If you previously logged in as an IAM user using an IAM User Account in this browser, your browser may display the IAM user login page instead. To return to the main login page, select **LOG IN WITH ROOT USER.**
4. After successful login, you have full access and can perform all features provided by the vDB OpenSearch service on your resources.

### Access resources using IAM user account <a href="#truy-cap-tai-nguyen-su-dung-iam-user-account" id="truy-cap-tai-nguyen-su-dung-iam-user-account"></a>

Follow the steps below to log in to vDB OpenSearch with an IAM user account:

1. Access the vDB OpenSearch login page: [https://signin.vngcloud.vn.](https://signin.vngcloud.vn/ap/auth?clientId=c9e78411-f2a2-41ba-a9e4-3c56263c181a\&responseType=code\&codeChallenge=f09ybYi-GTZYYwuHVRv2f1UPRhjM_wI-0J_aXpbUsv4\&codeChallengeMethod=S256\&appState=55eab53a-30f3-43ae-837b-bf3a469dd9db\&redirectUri=https%3A%2F%2Fdashboard.console.vngcloud.vn%2F)
2. The main login page will appear. Select **LOG IN WITH IAM USER ACCOUNT**.
3. Enter the **email** address of the Root user when registering the GreenNode account.
4. Enter the **username** and **password** of the IAM user account created on the vIAM system.
5. Select **LOG IN WITH IAM USER ACCOUNT**. If you previously logged in as an IAM user account in this browser, your browser may remember the IAM user account address. If so, you will see the screen shown in step 3. After successful login with IAM user account, the main screen of vDB OpenSearch will display the user type you are using to log in (Root user account or IAM user account).
6. After successful login, you have access and can perform features provided by the vDB OpenSearch service on resources that have been authorized for you.
