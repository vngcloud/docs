# Attach Policies with IAM User Account

After creating the IAM User Account and the desired Policy, the next step is to associate the IAM User Account with the policy. Follow the instructions below:

1\. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/]\(https://iam.console.vngcloud.vn/\)) using your Root User Account.\
2\. Navigate to the **User Account** section.\
3\. Choose the **IAM User Account** to which you want to assign permissions.\
4\. Select **Attach policies**.\
5\. Choose the **policies** you want to associate. The vIAM system allows you to attach multiple policies to one IAM User Account. If these policies contain independent permissions, they will complement each other (meaning the permission lists will be merged). Conversely, if these policies contain conflicting permissions, you will not be able to access the corresponding resources based on this permission list (meaning the permission lists will be merged, and conflicting permissions will override each other).\
6\. Select **Attach**.

After completing the above 6 steps, you can now use the Service Account to access vStorage resources. For more information, please refer to [Access Permissions and Working Through IAM User Account](https://docs.vngcloud.vn/display/VSEN/Access+Permissions+and+Working+Through+IAM+User+Account).
