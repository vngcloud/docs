# Attach Policies with IAM User Account

After you have created the IAM User Account and the Policy you want, attach the account to the policy as follows:

1. Log in to [https://iam.console.greennode.ai/](https://iam.console.greennode.ai/) with your Root User Account.
2. Select the **User Account** folder.
3. Select the **IAM User Account** you want to assign permissions to.
4. Select **Attach policies**.
5. Select the **policies** you want. The vIAM system lets you attach multiple policies to one IAM User Account. If the policies contain independent permissions, they complement each other (the permission lists are merged). If they contain conflicting permissions, you will not be able to access the corresponding resource under this permission list (the merged lists cancel each other out where they conflict).
6. Select **Attach**.

After completing the 6 steps above, you can use the account to access DataSync resources. For more information, see [Access Permissions and Working Through IAM](https://github.com/vngcloud/docs/blob/main/English/vstorage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-truy-cap-tai-nguyen-vstorage/truy-cap-tai-nguyen-su-dung-tai-khoan-nguoi-dung-iam.md).
