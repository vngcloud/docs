# Getting Start with IAM

In this section, we will explore the basic concepts of Identity and Access Management (IAM) and how to start managing access to cloud resources securely.

1. **Accessing the IAM Console**

Before we begin, please refer to the login guide with the Root User Account and IAM User Account here:

* [How to login to GreenNode](cac-loai-dinh-danh-iam/tai-khoan-user-accounts/cach-dang-nhap-vao-vng-cloud.md)

IAM Console is a web-based user interface that allows you to manage IAM User Accounts, Groups, Service Accounts, and Policies in your cloud computing environment. It provides a visual interface to control access to your resources and configure security settings.

**How to access the IAM Console?**

1. Open your web browser and go to the IAM Console URL: https://iam.console.vngcloud.vn/
2. Log in as a Root User Account or a User Account with access rights. You will need to provide your username/email and password when logging in.&#x20;
3. Once logged in, you will see the IAM Console interface, which provides an overview of your IAM configuration.

**2.Understanding IAM User Accounts & User Groups**&#x20;

**Root User Account**&#x20;

A Root User Account is an entity you first create in GreenNode and use, which by default has full access to all GreenNode products/services and resources in that account.&#x20;

**IAM User Account**&#x20;

IAM User Accounts represent individual identities associated with your Root User Account. Each user has a unique set of security credentials, such as usernames and passwords, or access keys, to authenticate their identity.&#x20;

**IAM User Group**&#x20;

An IAM User Group is a collection of IAM User Accounts that share similar access requirements. Grouping IAM User Accounts simplifies permissions management by granting permissions to a group instead of to each individual IAM User Account. This improves consistency and efficiency in access control.

**How to Create an IAM User Account?**

To create a new IAM user account:&#x20;

1. Go to the IAM Console.&#x20;
2. Click "User account" in the left menu.&#x20;
3. Click "Create a user account."&#x20;
4. Enter the user account details, including username and password.&#x20;
5. Review the settings and click "Create a user account." in the upper right corner.

**How to Create an IAM User Group?**\
To create a new IAM User Group:

1. Access the IAM Console.
2. Click on "Group" in the left menu.
3. Click on "Create new group."
4. Provide a group name and optional description.
5. Attach relevant IAM Policies to the Group to define the group's permissions.
6. Add the User Accounts to be managed into the Group.
7. Review the settings and click on "Create group."

**3.IAM Policy and Access Rights**&#x20;

**IAM Policy**&#x20;

IAM Policies are JSON documents that define resource access rights and rules. These Policies are attached to IAM User Accounts, Groups, or Service Accounts to control the actions they can perform on specific resources. IAM Policies follow the "allow" or "deny" principle, meaning they explicitly grant or deny access to resources and actions.&#x20;

**Access Policy**

IAM access rights define the actions that IAM entities (IAM User Accounts, Groups, and Service Accounts) are allowed or denied to perform on GreenNode resources. These actions include access levels such as viewing lists, reading and writing rights on resources, or managing IAM User Accounts and Groups.

**How to Configure Permissions in IAM Policy?**&#x20;

1. Go to IAM Console. Click "Policy" in the left menu.&#x20;
2. Click "Create a policy." Provide a Policy name and optional description.&#x20;
3. Click "Next step" to continue configuring permissions.&#x20;
4. Select a specific Product/Service in the GreenNode system that needs to be configured.&#x20;
5. Specify the Actions allowed on the product's resources.&#x20;
6. Select the Resources that apply the actions (All resources / Specific resources).&#x20;
7. Provide the Request conditions on the application time.&#x20;
8. Review the settings and click "Create policy."

**How to Assign Permissions to IAM Entities?**&#x20;

1. Create a new IAM Policy or use an existing Policy that fits your access control requirements.&#x20;
2. Attach the Policy to the appropriate IAM User Account, Group, and Service Account.&#x20;
3. Review and validate the assigned Policies to ensure compliance with the principle of least privilege.&#x20;

Remember to follow the principle of least privilege when assigning permissions to IAM entities, granting only the minimum permissions necessary for the IAM User Account, Group, and Service Account to perform their tasks.

Congratulations! You have learned the basics of how to get started with IAM. You can create IAM User Accounts, Groups, and Service Accounts, and assign permissions to them through IAM policies to control access to your cloud resources. Next, we will dive deeper into writing custom IAM Policies for more granular access control.
