# Working with Root User Account

## **Overview** <a href="#tong-quan" id="tong-quan"></a>

A Root User Account is an account that a user creates on the first day of accessing and using the services on VNG Cloud. A Root User Account has full access to all of the user's services and resources. When you create a VNG Cloud account, you start with a login identity that has full access to all of VNG Cloud's services and resources in the account. This identity is called a Root User Account and is accessed by logging in with the email address and password you used to create the account. We encourage you to not use the Root User Account for your daily tasks and only use this account to perform tasks that only the Root User Account can perform.

***

## **Create Root User Account** <a href="#khoi-tao-root-user-account" id="khoi-tao-root-user-account"></a>

To create a Root user account, please register an account at the registration page [https://register.vngcloud.vn/signup](https://register.vngcloud.vn/signup) .

After you create a Root user account, you collect the following information to access and work with resources using the Root user account:

* The email address used to create the Root user account.
* Password for the Root user account.

To log in to vStorage with the Root account, see [Accessing resources using the Root user account](https://docs.vngcloud.vn/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-truy-cap-tai-nguyen-vstorage/truy-cap-tai-nguyen-su-dung-tai-khoan-nguoi-dung-root) .

***

## **Cancel Root User Account** <a href="#huy-root-user-account" id="huy-root-user-account"></a>

To cancel your Root account, you need to contact us by creating a ticket to request account cancellation. For more details, see [Account Cancellation Instructions](https://docs.vngcloud.vn/vng-cloud-document/vn/huong-dan-su-dung-tai-khoan/huong-dan-huy-tai-khoan) .

***

## Access to vStorage using Root User Account <a href="#truy-cap-vao-vstorage-su-dung-root-user-account" id="truy-cap-vao-vstorage-su-dung-root-user-account"></a>

To access your resources on vStorage storage service, you can access through vStorage Portal, vStorage API, S3 Rest API and Swift/ s3 client tool. For vStorage Portal, you use Root User Account to access. If you do not have Root User Account, please refer to [Root User Account](https://docs.vngcloud.vn/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-nguoi-dung-root) .

Follow the steps below to log into vStorage with the Root user account:

1. Access the vStorage service login page: [https://signin.vngcloud.vn.](https://signin.vngcloud.vn/ap/auth?clientId=c9e78411-f2a2-41ba-a9e4-3c56263c181a\&responseType=code\&codeChallenge=f09ybYi-GTZYYwuHVRv2f1UPRhjM_wI-0J_aXpbUsv4\&codeChallengeMethod=S256\&appState=55eab53a-30f3-43ae-837b-bf3a469dd9db\&redirectUri=https%3A%2F%2Fdashboard.console.vngcloud.vn%2F)
2. The main login page will appear. Select **LOG IN WITH ROOT USER** .
3. **Enter the email** address and **password** associated with your account and select **Sign In** . If you previously signed in as the root user in this browser, your browser may remember the email address for the Root User Account. If so, you will see the screen shown in the next step. If you previously signed in as an IAM user using an IAM User Account in this browser, your browser may display the IAM user login page instead. To return to the main login page, select **LOG IN AS ROOT USER.**
4. After successful login, you have full access and perform the features provided by vStorage service on your resources.

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Assign permissions to Root User Account <a href="#phan-quyen-lam-viec-cho-root-user-account" id="phan-quyen-lam-viec-cho-root-user-account"></a>

By default, **the Root User Account** will have **full access** to your bucket, but you can also grant **other Root User Accounts** access to your bucket as your **IAM User Account through Bucket ACLs** and **Bucket Policy** .

<details>

<summary>Bucket ACLs</summary>

You can grant Read, Write or Read and Write permissions to 1 or all other Root users. (Root users granted access via ACLS must be authorized accounts on our VNG Cloud system). For more information, see Using [ACLs.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/object-storage-hcm04/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-acls)

</details>

<details>

<summary>Bucket Policy</summary>

You can manage access to your buckets through JSON rules. For more information, see [Using Bucket Policy.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/object-storage-hcm04/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-bucket-policy)

</details>
