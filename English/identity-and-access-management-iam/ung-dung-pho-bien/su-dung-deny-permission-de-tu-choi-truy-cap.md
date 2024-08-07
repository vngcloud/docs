# Use Deny permission to deny access

When you need to decentralize access to allow all actions except a few specific actions, you need to create a Policy and use Deny Permission to simplify decentralization. In this tutorial, we will guide you **to grant permissions to User: System1 to perform all vServer actions (Full Access), but not to allow action:Delete on Resource:server** , **to ensure User: System1 Do not delete any servers** . The model will look like below:

To set up IAM according to the above model, we will have the following steps:

**Step 1** : Create User: System1 if you do not have a User Account (note that if you already have User: System1, make sure User: System1 does not have any rights or does not have rights that overlap with the instructions)

**Step 2** : Create a Policy with the name vServerFullAccessExceptDeleteServer that allows access to the entire vServer Resource, but does not allow Delete Server

**Step 3** : Attach Policy: vServerFullAccessExceptDeleteServer to User: System1

**Step 4** : Log in and check the rights of User: System1

Detailed steps are as follows

**Step 1: Create User: System1 if you do not have a User Account (note that if you already have User: System1, make sure User: System1 does not have any rights or does not have rights that overlap with the instructions)**

Create a User Account by accessing the User Account tab on the IAM management page here [,](https://hcm-3.console.vngcloud.vn/iam/user-accounts) clicking **Create a User Account,** filling in Username and Password information, then clicking **Create User Account**

After successfully creating a User Account, it will be listed on the User Account page as below

**Step 2: Create a Policy with the name vServerFullAccessExceptDeleteServer that allows access to all resources of vServer, but does not allow Delete Server**

To create a Policy, go to the Policy tab on the IAM page here [,](https://hcm-3.console.vngcloud.vn/iam/policies) click **Create a Policy** , **name** the Policy: **vServerFullAccessExceptDeleteServer** and click **Next step**

Click JSON to switch to JSON mode and create a Policy with the available JSON segment

Use the JSON snippet below and copy it into Policy

| `{ "statements": [ { "effect": "allow", "actions": [ "vserver:*" ], "resources": [ "*" ], "condition": {} }, { "effect": "deny", "actions": [ "vserver:DeleteServer" ], "resources": [ "*" ], "condition": {} } ]}` |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Click **Create policy** to create Policy

**Step 3** : Attach Policy: vServerFullAccessExceptDeleteServer to User: System1

After successfully creating Policy: vServerFullAccessExceptDeleteServer, you proceed to attach this Policy to User: System1, you can do it in User Account or Policy, here we will guide in Policy, **click on the name of the Policy** to go to the details page. Policy details:

**Select the Policy usage tab** and **click Attach** to add User: System1

**Select User: System1** and **click Add**

After adding User: System1 to Policy: vServerFullAccessExceptDeleteServer, you will see information like below

**Step 4** : Log in and check the rights of User: System1

Now you can log in to User: System1 to check permissions

Access vServer here [,](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) without logging into any account you will be redirected to the sign-in page, select " **Sign-in With IAM User Account** "

Fill in the root user email account information that User: System1 was previously created, IAM username and password information of User: System1, click **Sign-in with IAM User Account**

At this point you will see that User: System1 will have full rights on vServer but cannot delete any Resource: server

Accessed web1-server's detail page successfully

Successfully shutdown web1-server:

But the server web1-server cannot be deleted

So you have completed the authorization allowing User: System1 to perform all vServer actions (Full Access), but not allowing action:Delete to be performed on Resource:server, to ensure User: System1 is not deleted. any servers.
