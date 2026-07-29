# Create Policies for IAM User Account

To create a policy for accessing DataSync resources, follow the steps below:

1. Log in to [https://iam.console.greennode.ai/](https://iam.console.greennode.ai/) with your Root User Account.
2. Select the **Policy** folder.
3. Select **Create a Policy**.
4. Enter a **Name** and **Description** for the Policy.
5. Select **Next step**.
6. Select **Product** as **DataSync**.
7. Select **Actions**:
   1. **Allow permissions** toggle: by default, the vIAM system keeps this on, meaning the permissions are allowed on the policy. If you turn this mode off, the system denies (inverts) the corresponding permissions.
      * **Allow permissions:** allow access for the selected action.
      * **Deny permissions:** deny access for the selected action.
   2. Select **All DataSync actions** if you want a policy with permission to perform all actions on DataSync. For the meaning of each action, refer to [Features, DataSync Resources, and Access Permissions](../../quan-ly-truy-cap-tai-nguyen-datasync/tinh-nang-tai-nguyen-datasync-va-quyen-truy-cap.md).
8. Select **Resources**:
   1. Select **All resources** if you want the selected permissions above to apply to every resource in your SSO account.
   2. Select **Specify resources**: choose the specific project, container, or object you want to grant access to. You can enter each resource type in one of the following ways:
      * Enter `*` to select all resources.
      * Enter a specific **project ID, container name, or object name** to target that exact resource.
      * Enter a **prefix** to target a set of projects, containers, or objects that start with the declared prefix.
   3. You can also select **Any** to allow access to every project, container, and object in your SSO account.
   4. Select **Request conditions:** enter special conditions for the policy, if any.

After completing the 8 steps above, the DataSync policy is created. Next, attach it to the IAM User Account following the guide at [Attach Policies with IAM User Account](https://github.com/vngcloud/docs/blob/main/English/vstorage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-nguoi-dung-iam/lien-ket-tai-khoan-iam-user-account-voi-policy-tuong-ung.md).

In addition to creating your own custom policy as above, we also provide a set of default policies with a range of permissions. You can use this set and attach them directly to IAM User Accounts for quick authorization without creating a detailed policy. For more information about the default policy list, refer to [Features, DataSync Resources, and Access Permissions](../../quan-ly-truy-cap-tai-nguyen-datasync/tinh-nang-tai-nguyen-datasync-va-quyen-truy-cap.md).
