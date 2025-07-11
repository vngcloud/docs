# Create Policies for IAM User Account

To create a policy for accessing vStorage resources, follow the steps below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/]\(https://iam.console.vngcloud.vn/\)) using your Root User Account.
2. Select the **Policy** directory.
3. Choose **Create a Policy.**
4. Enter a **Name** and **Description** for the Policy.
5. Select **Next step**.
6. Choose the **Product as vstorage**.
7. Select **Actions**:
   1. Choose **Allow permissions** (system default): The system will always enable permissions, meaning it allows the selected actions. If you disable this mode, the system will deny (reverse) the corresponding permissions.
      1. **Allow permissions**: Allow access based on the selected actions.
      2. **Deny permissions**: Deny access based on the selected actions.
   2. Choose **All vstorage actions** if you want to create a policy with permissions for all actions on vStorage. For details on the meaning of each action, refer to the vStorage Features, Resources, and Access Rights.
8. Select **Resources**:
   1. Choose **All resources** to allow the selected permissions to access all resources on your SSO account.
   2. Choose **Specify resources**: Select a specific project, container, or object you want to grant access to. You can enter information for each type of resource in the following ways:
      1. **Enter \*** to select all resources.
      2. **Enter the specific ID** of the project, the name of the container, or the name of the object for precise access.
      3. **Enter a prefix** if you want to specify a set of projects, containers, or objects starting with the declared prefix.
   3. You can also choose Any to allow access to all projects, containers, and objects in your SSO account.
   4. Select Request conditions: Enter specific conditions for the policy if needed.

After completing the above 8 steps, the policy for vStorage has been created. Next, assign it to an IAM User Account following the instructions in Linking IAM User Account with the Corresponding Policy.

In addition to creating specific policies as outlined above, we also provide you with a set of default policies with diverse permissions. You can use these default policies and directly link them to your IAM User Account. For more information on the list of default policies, please refer to the [Features, vStorage Resources, and Access Permissions](https://docs.vngcloud.vn/display/VSEN/Features%2C+vStorage+Resources%2C+and+Access+Permissions).

\
