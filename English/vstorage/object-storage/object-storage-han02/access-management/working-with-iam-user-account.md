# Working with IAM User Account

## **Tổng quan**

**IAM User Accounts** are representative accounts used to interact with GreenNode through the Portal UI page. A user account at VNG will include authentication information (login name and password) and is set to no access by default. These user accounts do not exist independently; they belong to a single root user account and do not come with any costs.

If your business has multiple members who need to be granted access to GreenNode, do not share the security information of the root user account. VNG recommends that you create user accounts for each of these members on your root user account and you will be able to grant different permissions to each of these user accounts.

***

## Create IAM User Account <a href="#khoi-tao-iam-user-account" id="khoi-tao-iam-user-account"></a>

To create an IAM user account, please first refer to the instructions below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/) with Root User Account.
2. Select **User Account** .
3. Select **Create a User Account.**
4. In the **Account username** section , enter **the Account username** you want. The IAM User Account name must be from 5 (minimum) to 50 (maximum) characters long and can only include uppercase letters, lowercase letters (az, AZ), numbers (0-9), periods (.), underscores (\_), and hyphens (-). The IAM User Account name should not contain sensitive information (e.g. IP address, login password, etc.) and the IAM User Account name must be unique on a GreenNode account until that IAM User Account is deleted. For example, the following IAM User Account name is valid: IAM\_Phong\_kinh\_doanh\_01.
5. Select **Add a username** .
6. In the **Account password** section , you can:
   1. Enter your desired **password** . Password must be between 8 (minimum) and 50 (maximum) characters long and must include at least 1 uppercase letter (A-Z), 1 lowercase letter (a-z), 1 number (0-9), and 1 special character (!@#$%,...).
   2. Select **Auto-generate** if you want the system to automatically generate a password for you.
7. Select **Copy** to copy the password. You must collect this information to access vStorage using an IAM User Account.
8. Select **Create User Account.**

<figure><img src="../../../../.gitbook/assets/image (553).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (554).png" alt=""><figcaption></figcaption></figure>

***

## Assign permissions to work with the project to the IAM User Account <a href="#phan-quyen-lam-viec-voi-project-vstorage-api-cho-service-account" id="phan-quyen-lam-viec-voi-project-vstorage-api-cho-service-account"></a>

### Create an IAM Policy <a href="#khoi-tao-iam-policy" id="khoi-tao-iam-policy"></a>

To initialize a policy used to access vStorage resources, follow the steps below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/) with Root User Account.
2. **Select the Policy** folder .
3. Select **Create a Policy** .
4. Enter **Name** and **Description** if given for Policy.
5. Select **Next step** .
6. Select **Product as&#x20;**<mark style="background-color:blue;">**vstorage**</mark> .
7. Select **Actions** :
   1. Select **Allow permissions** : by default, the vIAM system will always be on, which means allowing permissions to be applied to the policy. If you turn this mode off, the system will deny (reverse) the corresponding permissions.
      1. **Allow permissions** : allow access according to the selected action.
      2. **Deny permissions** : deny access according to the selected action.
   2. Select <mark style="background-color:blue;">**All vstorage actions**</mark> if you want to create a policy that has the right to perform all actions on vStorage. Or you can select some specific actions that you want to authorize for IAM User Account.
8. Select **Resources** : select **All resources.**
9. Select **Request conditions:** enter special conditions for the policy if any.

<figure><img src="../../../../.gitbook/assets/Screenshot-4.png" alt=""><figcaption></figcaption></figure>

### Attach IAM Policy to IAM User Account <a href="#attach-iam-policy-vao-iam-user-account" id="attach-iam-policy-vao-iam-user-account"></a>

Once you have created the desired IAM User Account and Policy, you will need to link the IAM User Account to the policy as per the instructions below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/) with Root User Account.
2. Select the User Account folder **.**
3. Select **the IAM User Account** you want to assign permissions to.
4. Select **Attach policies** .
5. Select the **policies** you want. The vIAM system supports you to assign multiple policies to an IAM User Account. If these policies contain independent permissions, they will complement each other (ie the permission list is merged). On the contrary, if these policies contain conflicting permissions, you will not be able to access the corresponding resources according to this permission list (ie the permission list is merged and when conflicting, they will cancel each other out).
6. Select **Attach**.

<figure><img src="../../../../.gitbook/assets/image (556).png" alt=""><figcaption></figcaption></figure>

***

## Assign permissions to work with the bucket/object to the IAM User Account <a href="#phan-quyen-truy-cap-vao-project-cho-iam-user-account" id="phan-quyen-truy-cap-vao-project-cho-iam-user-account"></a>

To grant access to bucket/object for IAM User Account, you need to grant permission via Bucket Policy, specifically the steps are as follows:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .
2. Select the **Bucket** you want to assign permissions to the IAM User Account.
3. Select the **Action** icon and select **Configure policy.**

<figure><img src="../../../../.gitbook/assets/image (558).png" alt=""><figcaption></figcaption></figure>

4. Here, you can choose the configuration for each **Statement** on the left or directly edit the JSON file in the right column. Specifically, the structure of a Bucket Policy includes:

* **Version** : Specifies the version of the Bucket Policy (recommended `"2012-10-17"`).
* **Statement** : Each policy will have one or more **Statements** (specific purposes of the policy).
  * **Effect** : `Allow`or `Deny`access.
  * **Principal** : The object granted access, which is the IAM vStorage User ID information of selected IAM user account.
  * **Action** : Actions allowed on the bucket, for example: `s3:GetObject`(view object), `s3:PutObject`(upload object), `s3:DeleteObject`(delete object),…
  * **Resource** : Specific buckets and objects affected by the policy (using ARN to identify resources).
  * **Condition** : (Optional) Specific condition that restricts access.

5. Select **Save** to save the Bucket Policy configuration.

<figure><img src="../../../../.gitbook/assets/Screenshot from 2025-11-10 13-54-54.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/Screenshot from 2025-11-10 13-57-09 (1).png" alt=""><figcaption></figcaption></figure>

## Access to vStorage via IAM User Account <a href="#thuc-hien-truy-cap-vao-vstorage-thong-qua-iam-user-account" id="thuc-hien-truy-cap-vao-vstorage-thong-qua-iam-user-account"></a>

Follow the steps below to log in to vStorage with an IAM user account:

1. Access the vStorage service login page: [https://signin.vngcloud.vn.](https://signin.vngcloud.vn/ap/auth?clientId=c9e78411-f2a2-41ba-a9e4-3c56263c181a\&responseType=code\&codeChallenge=f09ybYi-GTZYYwuHVRv2f1UPRhjM_wI-0J_aXpbUsv4\&codeChallengeMethod=S256\&appState=55eab53a-30f3-43ae-837b-bf3a469dd9db\&redirectUri=https%3A%2F%2Fdashboard.console.vngcloud.vn%2F)
2. The main login page will appear. Select **LOG IN WITH IAM USER ACCOUNT** .
3. Enter the Root user's **email** address when registering for a GreenNode account.
4. Enter **the username** and **password** of the IAM user account created on the vIAM system.
5. Select **LOG IN WITH IAM USER ACCOUNT** . If you have previously logged in as an IAM user account in this browser, your browser may remember the IAM user account address. If so, you will see the screen shown in step 3. After successfully logging in with an IAM user account, the main screen of vStorage will show the type of user you are using to log in (Root user account or IAM user account).
6. After successful login, you have the right to access and perform the features provided by the vStorage service on the resources authorized to you.

<figure><img src="../../../../.gitbook/assets/image (560).png" alt=""><figcaption></figcaption></figure>

***

## Delete IAM User Account <a href="#xoa-iam-user-account" id="xoa-iam-user-account"></a>

To cancel (delete) a previously created IAM User Account, follow the instructions below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/) with Root User Account.
2. Select **User Account** .
3. From the list of existing IAM User Accounts, select one or more IAM user accounts that you want to cancel (delete).
4. Select **Delete** .

Once the IAM User Account is successfully canceled, you will no longer be able to use this IAM User Account to access vStorage. Be careful when canceling (deleting) an IAM User Account because you will not be able to recover this deleted account.
