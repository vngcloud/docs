# Create Policies for Service Account

In a general overview, the process of creating a policy has similarities for both IAM User Accounts and Service Accounts. However, we will reiterate the steps to make it easy for you to observe and execute.

To create a policy for accessing vStorage resources, follow these steps:

1. Log in to [https://iam.console.vngcloud.vn](https://iam.console.vngcloud.vn/]\(https://iam.console.vngcloud.vn/\)) with your Root User Account.
2. Choose the **Policy** menu.
3. Select **Create a Policy**.
4. Enter the **Name** and **Description** for the Policy.
5. Click **Next step**.
6. Choose the **Product** as **vstorage-hcm03**.
7. Choose **Actions**:
   1. Select **Allow permissions**: By default, the vIAM system will always enable permissions to be applied in the policy. If you disable this mode, the system will deny (reverse) the corresponding permissions.
      1. **Allow permissions**: Allow access based on the selected action.
      2. **Deny permissions**: Deny access based on the selected action.
   2. Choose **All vstorage-hcm03 actions** if you want to create a policy with permission for all actions on vStorage. For detailed meanings of actions, refer to the Features, vStorage Resources, and Access Permissions.
8. Choose **Resources**:
   1. Select **All resources** if you want the selected permissions to be allowed access to all resources in your SSO account.
   2. Choose **Specify resources**: Select the specific project, container, or object you want to allow access to. You can enter information for each resource type in one of the following ways:
      1. **Enter \*** if you want to select all resources.
      2. **Enter the specific ID** of the project, the name of the container, or the name of the object if you want to specify the exact project, container, or object.
      3. **Enter a prefix** if you want to specify a set of projects, containers, or objects starting with the declared prefix.
   3. You can also choose **Any** to allow access to all projects, containers, or objects in your SSO account.
   4. Choose **Request conditions**: Enter special conditions for the policy if any.

After completing the above 8 steps, the policy for vStorage has been created. Next, assign it to the Service Account as instructed in [Attach Policies with Service Account](https://docs.vngcloud.vn/display/VSEN/Attach+Policies+with+Service+Account).

In addition to the specific policy creation steps provided above, we also offer you a set of default policies with diverse permissions. You can use this policy set and directly link them to your Service Account. For more information on the list of default policies, please refer to [Features, vStorage Resources, and Access Permissions](https://docs.vngcloud.vn/display/VSEN/Features%2C+vStorage+Resources%2C+and+Access+Permissions).

\\
