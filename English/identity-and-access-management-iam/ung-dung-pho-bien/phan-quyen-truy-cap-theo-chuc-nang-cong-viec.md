# Access control by job function

When assigning access rights to resources, companies often allocate permissions based on the job functions of team members. There are two main job functions in an IT company: System Administrator and Developer. This guide will explain how to grant permissions for the two job function groups to access vServer and vStorage products.

First, the access rights of the two job function groups will be defined as follows:

* System Administrator: responsible for managing all resources on the Cloud, so they should be granted full permissions for vServer and vStorage, corresponding to the managed policies that have been pre-created by VNG Cloud: vServerFullAccess, vStorageFullAccess.
* Developer: only needs to view the resources on the Cloud, so they only require read-only access for vServer and vStorage, corresponding to the managed policies that have been pre-created by VNG Cloud: vServerReadOnlyAccess, vStorageReadOnlyAccess.

To manage the allocation of permissions for many members in the company more easily, we will also organize two User Groups named: SystemAdmin and Developer, with members having the same job function grouped into the corresponding User Groups to benefit from the permissions granted to those User Groups. Managing through User Groups will allow you to flexibly change permissions when necessary or when team members change job functions.

With the organization as above, we will have a detailed statistical table as follows:

| **Function**         | **User Group** | **Permission**                                            | **Description**                          |
| -------------------- | -------------- | --------------------------------------------------------- | ---------------------------------------- |
| System Administrator | SystemAdmin    | <p>vServerFullAccess</p><p>vStorageFullAccess</p>         | Đầy đủ quyền trên vServer, vStorage      |
| Developer            | Developer      | <p>vServerReadOnlyAccess</p><p>vStorageReadOnlyAccess</p> | Chỉ xem thông tin trên vServer, vStorage |

Tương ứng ta sẽ có mô hình tổ chức như bên dưới:

<figure><img src="../../.gitbook/assets/iam-jobs-function.drawio (4).png" alt=""><figcaption></figcaption></figure>

**To set up IAM according to the above model, we will have the following steps:**&#x20;

Step 1: Create User Groups (SystemAdmin, Developer) and attach the corresponding managed policies

&#x20;Step 2: Create User Accounts (System1, System2, Developer1, Developer2) and attach them to the corresponding User Groups&#x20;

Step 3: Log in to the User Accounts to check the rights&#x20;

Detailed instructions for the steps&#x20;

Step 1: Create User Groups (SystemAdmin, Developer) and attach the corresponding managed policies Access the Group tab on the IAM management page here, click "Create a Group" and fill in the group name information as SystemAdmin, click Next step to go to the Policy attachment step

Search and attach 2 managed policies vServerFullAccess and vStorageFullAccess to group: SystemAdmin, then click Create Group to create&#x20;

Follow the steps above when creating group: Developer, select managed policy vServerReadOnlyAccess and vStorageReadOnlyAccess&#x20;

Thus you have completed creating 2 User Groups: SystemAdmin and Developer with full rights as defined

**Step 2: Create User Accounts (System1, System2, Developer1, Developer2) and attach them to the corresponding User Groups**

Create User Accounts by accessing the User Account tab on the IAM management page here, click Create a User Account, fill in the Username and Password information, then click Create User Account (note that for a brief guide here we create 4 user accounts with the same password, we recommend that you create separate user accounts with different passwords, or change the password when using):&#x20;

After successfully creating User Accounts, they will be listed on the User Account page as below To add Users: System1, System2, Developer1, Developer2 to Group: SystemAdmin, Developer you can do it for each User Account or Group, here we will guide you to add User Accounts in Group, you go to the Group tab and click on the name of the Group to go to the Group details, as here is Group: SystemAdmin&#x20;

Select the User tab Click Add Users, a popup will appear, you select User: System1, System2 and Click Add: To add User: Developer1, Developer2 to Group: Developer, you do the same steps as above:&#x20;

So you have completed creating User Accounts and adding them to the corresponding Group, now the User Accounts will inherit all the rights that the Group has.

**Step 3: Log in to User Accounts to check permissions**\
At this point, you can log into the User Accounts to check permissions. Here we will attempt to log in to 2 Users: System1, Developer1 to perform some actions on the vServer to check permissions.

Access the vServer here; when not logged into any account, you will be redirected to the sign-in page, select "Sign-in With IAM User Account."

Fill in the root user account email that was created previously by the IAM user, the IAM username, and password, then click Sign-in with IAM User Account.

At this point, you will see User: System1 has full rights on the vServer, you can perform actions such as creating a new Server or changing Server information to check permissions; for example, below is User: System1 successfully starting a Server.

Follow the same steps to log in to User: Developer1; at this point, you will see User: Developer1 only has permission to view the vServer information and cannot interact with or change the Server. For example, below is User: Developer1 trying to start a Server but being denied.

Thus, you have completed the process of assigning access rights according to job functions. Now, to grant permissions to new members, you just need to create a User Account and add it to a Group. To change permissions, you just need to change the Policy in the Groups, which makes managing access to resources on VNG Cloud much easier.
