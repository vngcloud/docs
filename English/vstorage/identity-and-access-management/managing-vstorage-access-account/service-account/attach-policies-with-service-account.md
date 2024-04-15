# Attach Policies with Service Account

After you have created a Service Account and the desired Policy, the next step is to attach the Service Account to the policy as instructed below:

1. Log in to [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/]\(https://hcm-3.console.vngcloud.vn/iam/\)) with your Root User Account.
2. Select the **Service Account** menu.
3. Choose the **Service Account** for which you want to assign permissions.
4. Click **Attach policies**.
5. Select the **policies** you want to attach. The vIAM system supports attaching multiple policies to a Service Account. If these policies contain independent permissions, they will complement each other (meaning the list of permissions will be consolidated). Conversely, if these policies contain conflicting permissions, you will not be able to access the corresponding resources based on this list of permissions (meaning the list of permissions will be overridden when conflicting).
6. Click **Attach**.

After completing these 6 steps, you can now use the Service Account to access vStorage resources. For more information, refer to [Access Permissions and Working Through Service Account](https://docs.vngcloud.vn/display/VSEN/Access+Permissions+and+Working+Through+Service+Account).
