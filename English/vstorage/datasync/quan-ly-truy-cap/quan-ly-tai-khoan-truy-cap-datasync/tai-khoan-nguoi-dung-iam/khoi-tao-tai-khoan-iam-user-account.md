# Create an IAM User Account

To create an IAM user account, first refer to the step-by-step guide [here](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59805240). Below is our detailed guide to help you create an IAM user account for accessing DataSync resources:

1. Log in to [https://iam.console.greennode.ai/](https://iam.console.greennode.ai/) with your Root User Account.
2. Select **User Account**.
3. Select **Create a User Account**.
4. In **Account username**, enter the username you want. The IAM User Account name must be 5 (minimum) to 50 (maximum) characters long and may only contain uppercase and lowercase letters (a–z, A–Z), numbers (0–9), periods (.), underscores (\_), and hyphens (-). It should not contain sensitive information (e.g., IP address, login password), and it must be unique within a GreenNode account until that IAM User Account is deleted. For example, `IAM_Phong_kinh_doanh_01` is a valid name.
5. Select **Add a username**.
6. In **Account password**, you can:
   1. Enter your desired **password**. The password must be 8 (minimum) to 50 (maximum) characters and must include at least 1 uppercase letter (A–Z), 1 lowercase letter (a–z), 1 number (0–9), and 1 special character (!@#$%, …).
   2. Select **Auto-generate** if you want the system to generate a password for you.
7. Select **Copy** to copy the password. You must capture this information to access DataSync using the IAM User Account.
8. Select **Create User Account**.

After completing the 8 steps above, an IAM User Account is created. You can now use it; however, the newly created IAM User Account has no policy yet, so all access is denied. Therefore, continue by creating a policy following the guide at [Create Policies for IAM User Account](https://github.com/vngcloud/docs/blob/main/English/vstorage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-nguoi-dung-iam/khoi-tao-policy-cho-iam-user-account.md).

