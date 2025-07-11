# Access control by job function

When decentralizing access to resources, companies will often decentralize permissions based on the job functions of members. There are two main types of job functions in an IT company: **System Administrator** and **Developer** . This manual will guide you on how to assign permissions to two functional groups to access vServer and vStorage products.

First, the access rights of the above two groups of job functions will be defined as follows:

* **System Administrator** : responsible for managing all resources on the Cloud, should be granted full vServer rights, vStorage will correspond to the managed policies already created by VNG Cloud: vServerFullAccess, vStorageFullAccess
* **Developer** : only needs to view resources on the Cloud, so just grant read-only permission to vServer, vStorage will correspond to the managed policies already created by VNG Cloud: vServerReadOnlyAccess, vStorageReadOnlyAccess.

To make it easier to manage decentralization for many members in the company, we will organize **2 more User Groups with the names: SystemAdmin and Developer** , with members with the same job function being attached. Corresponding User Groups to enjoy the rights granted to User Groups. Managing with User Groups will help you flexibly change permissions when necessary, or when members change job functions.tr

With the above organization, we will have a detailed statistical table as follows:

| **Job function**     | **User Group** | **Permission**                                            | **Describe**                                  |
| -------------------- | -------------- | --------------------------------------------------------- | --------------------------------------------- |
| System Administrator | SystemAdmin    | <p>vServerFullAccess</p><p>vStorageFullAccess</p>         | Full rights on vServer, vStorage              |
| Developer            | Developer      | <p>vServerReadOnlyAccess</p><p>vStorageReadOnlyAccess</p> | Only view information on vServer and vStorage |

Correspondingly, we will have an organizational model as below:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FnHc8l6Jg1zfiM3QU0Ndf%252Fiam-jobs-function.drawio%2520%284%29.png%3Falt%3Dmedia%26token%3Ded896107-cbfe-47d2-b9d5-07dce14f3d1e&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=161f5764&#x26;sv=1" alt=""><figcaption></figcaption></figure>

To set up IAM according to the above model, we will have the following steps:

**Step 1** : Create User Groups (SystemAdmin, Developer) and attach corresponding managed policies

**Step 2** : Create User Account (System1, System2, Developer1, Developer2) and attach to the corresponding User Groups

**Step 3** : Log in to User Accounts to check permissions

Detailed step-by-step instructions

**Step 1: Create User Groups (SystemAdmin, Developer) and attach corresponding managed policies**

Access the Group tab on the IAM management page here [,](https://iam.console.vngcloud.vn/user-groups) click " **Create a Group** " and fill in the group name information as SystemAdmin, click **Next step** to go to the step of attaching Policy

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F9axpZLMVuHOAkD9OGqTw%252Fimage2023-7-12_13-11-7.png%3Falt%3Dmedia%26token%3D7e5d947f-e891-4cdd-b6c1-e25269a1dbc3&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6790712f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Search and attach 2 managed policies, vServerFullAccess and vStorageFullAccess, to the group: SystemAdmin, then click **Create Group** to create

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F2Oqb5lupxifmQ44LhCPu%252Fimage2023-7-12_13-14-33.png%3Falt%3Dmedia%26token%3D2823d8e9-7cae-42b1-aba7-c48e04a65a75&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=394da2c2&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Follow the same steps above when creating a group: Developer, select managed policy as vServerReadOnlyAccess and vStorageReadOnlyAccess

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FbNWXf5P3RTV7GwnciWHp%252Fimage2023-7-12_13-18-8.png%3Falt%3Dmedia%26token%3Dbf74548d-18ac-4134-ab02-b9ee26d5bb69&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4799c99f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

So you have completed creating 2 User Groups: SystemAdmin and Developer with full rights as defined

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FS8qj2ZrITxz30NzckQCL%252Fimage2023-7-12_13-19-30.png%3Falt%3Dmedia%26token%3Dbf7d3adb-8000-4d9f-ba8b-627d36230d14&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=5632cdbe&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 2: Create User Account (System1, System2, Developer1, Developer2) and attach to the corresponding User Groups**

Proceed to create User Accounts by accessing the User Account tab on the IAM management page here [,](https://iam.console.vngcloud.vn/user-accounts) clicking **Create a User Account,** filling in Username and Password information, then clicking **Create User Account** (note for brief instructions in Here we create 4 user accounts with the same password. We recommend that you create separate user accounts with different passwords, or change passwords when using):

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FhQn5iGMR9fKuaAE51E3N%252Fimage2023-7-12_13-23-4.png%3Falt%3Dmedia%26token%3D1ba45d7b-23f3-4829-b870-75bd559125ab&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=f0d06792&#x26;sv=1" alt=""><figcaption></figcaption></figure>

After successfully creating User Accounts, they will be listed on the User Account page as below

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FegTcEVJWM6wwCnI0ewFu%252Fimage2023-7-12_13-33-2.png%3Falt%3Dmedia%26token%3Dca580abf-63cc-4ac0-a465-b1c88cc49efc&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=2a88017d&#x26;sv=1" alt=""><figcaption></figcaption></figure>

To add Users: System1, System2, Developer1, Developer2 to Group: SystemAdmin, Developer, you can do it in each User Account or Group, here we will guide you to add User Account in Group, go to Group tab and click on **the name. of Group** to enter the details of the Group, as here is Group: SystemAdmin

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FVDt1a7AtnBsGyZNUgyXP%252Fimage2023-7-12_13-37-11.png%3Falt%3Dmedia%26token%3D2902d02a-2e73-4b91-bd51-5e814881222b&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c7800951&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Select **the User tab**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FxvjGtuTgTpNwGYqYRaML%252Fimage2023-7-12_13-37-52.png%3Falt%3Dmedia%26token%3D8526c44b-6759-498c-825c-dad41bc4cfa1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ec699302&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Click Add **Users** , a popup will appear, select User: System1, System2 and click **Add:**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F1PTfYNPVnys8QSVkoARG%252Fimage2023-7-12_13-40-25.png%3Falt%3Dmedia%26token%3D60b71ede-b031-4bd5-aa44-ecc02b6945d1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=89753dc2&#x26;sv=1" alt=""><figcaption></figcaption></figure>

To add User: Developer1, Developer2 to Group: Developer, follow the same steps as above:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FG2EQgogxEGHMzQnEf9n8%252Fimage2023-7-12_13-42-39.png%3Falt%3Dmedia%26token%3D69c19684-f385-4f58-8a3d-837ee8d2f7a7&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d4068db2&#x26;sv=1" alt=""><figcaption></figcaption></figure>

So you have completed creating User Accounts and adding them to the corresponding Group, at this point the User Accounts will fully inherit the rights that the Group has.

**Step 3: Log in to User Accounts to check permissions**

Now you can log in to User Accounts to check permissions. Here we will try to log in to 2 Users: System1, Developer1 to perform some operations on vServer to check permissions.

Access vServer here [,](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) without logging into any account you will be redirected to the sign-in page, select " **Sign-in With IAM User Account** "

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FmdQBYNKxdAq8QadoBSVK%252Fimage2023-7-12_13-48-49.png%3Falt%3Dmedia%26token%3De4634074-71dd-445f-9294-2830aa32f2da&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=de5bb399&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Fill in the root user email account information where the IAM user was previously created, IAM username and password information, click **Sign-in with IAM User Account**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FhmeKrb8FqzH0gRPEQKid%252Fimage2023-7-12_13-50-7.png%3Falt%3Dmedia%26token%3D119a561a-1759-430a-bcff-74fe8a4660e4&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=a9a95265&#x26;sv=1" alt=""><figcaption></figcaption></figure>

At this point you will see that User: System1 has full rights on vServer. You can create a new Server or change Server information to check permissions. For example, below is User: System1 successfully starting a Server.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F3dgUltnzToZ4DxrYoWZx%252Fimage2023-7-12_13-56-36.png%3Falt%3Dmedia%26token%3D10474333-bff3-4446-b1a7-82fba54b8de5&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d153aa22&#x26;sv=1" alt=""><figcaption></figcaption></figure>

Do the same steps above to log in to User: Developer1, now you will see that User: Developer1 only has the right to view vServer information, cannot interactively change the Server, for example below is User: Developer1 wanting to start 1 Server but refused execution

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F9V1YygxlEK2F7lmGmVuk%252Fimage2023-7-12_13-59-54.png%3Falt%3Dmedia%26token%3Dbfe340bd-1858-4da2-a534-c0a006d73d4f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=bade6e2a&#x26;sv=1" alt=""><figcaption></figcaption></figure>

So you have completed assigning access rights according to job functions. Now to grant permissions to new members, you just need to create a User Account and add it to the Group. To change permissions, you just need to change the Policy. at Groups makes it easier to manage access to resources on VNG Cloud.
