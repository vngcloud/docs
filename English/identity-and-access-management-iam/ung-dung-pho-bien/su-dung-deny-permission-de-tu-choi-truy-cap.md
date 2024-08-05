# Use Deny permission to deny access

When there is a need to grant access permissions that allow all actions except for a few specific actions, you need to create a Policy and use Deny Permission to simplify the permission assignment. In this guide, we will instruct you on how to grant permissions allowing&#x20;

* User: System1 to perform all actions of vServer (Full Access), but not to perform the action: Delete on Resource: server, to ensure User: System1 does not delete any servers. The model will be as follows:\
  To set up IAM according to the above model, we will have the following steps:

**Step 1: Create User: System1 if there is no User Account (note that if User: System1 already exists, make sure User: System1 has no permissions or does not have conflicting permissions with the guide)**

**Step 2: Create a Policy named vServerFullAccessExceptDeleteServer that allows access to all Resources of vServer but does not allow Delete Server**

**Step 3: Attach Policy: vServerFullAccessExceptDeleteServer to User: System1**

**Step 4: Log in and check the permissions of User: System1**

Details of the steps are as follows

Step 1: Create User: System1 if there is no User Account (note that if User: System1 already exists, make sure User: System1 has no permissions or does not have conflicting permissions with the guide)\
Proceed to create a User Account by accessing the User Account tab on the IAM management page here, click Create a User Account, fill in the Username and Password information, then click Create User Account

After successfully creating the User Account, it will be listed on the User Account page as below.

Step 2: Create a Policy named vServerFullAccessExceptDeleteServer that allows access to all Resources of vServer but does not allow Delete Server

To create a Policy, go to the Policy tab on the IAM page here, click Create a Policy, name the Policy: vServerFullAccessExceptDeleteServer and click Next step

Click JSON to switch to JSON mode and create the Policy with the provided JSON snippet. Use the JSON snippet below and copy it into the Policy

| `{ "statements": [ { "effect": "allow", "actions": [ "vserver:*" ], "resources": [ "*" ], "condition": {} }, { "effect": "deny", "actions": [ "vserver:DeleteServer" ], "resources": [ "*" ], "condition": {} } ]}` |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Press Create policy to create a Policy

Step 3: Attach Policy: vServerFullAccessExceptDeleteServer to User: System1\
After successfully creating the Policy: vServerFullAccessExceptDeleteServer, you proceed to attach this Policy to User: System1, you can do this in User Account or Policy, here we will guide you in Policy, click on the name of the Policy to go to the Policy detail page

Select the Policy usage tab and press Attach to add User: System1

Select User: System1 and press Add

After adding User: System1 to Policy: vServerFullAccessExceptDeleteServer, you will see the information as below

Step 4: Log in and check the permissions of User: System1

At this point you can log in as User: System1 to check the permissions

Access the vServer here, when not logged into any account you will be redirected to the sign-in page select "Sign-in With IAM User Account"

Enter the root user account email that User: System1 was previously created, the IAM username and password of User: System1, press Sign-in with IAM User Account

At this moment you will see User: System1 will have full rights on the vServer but cannot delete any&#x20;

Resource: server

Successfully access the detail page of web1-server

Successfully turn off the web1-server:

But cannot delete the web1-server

Thus you have completed the authorization allowing User: System1 to perform all actions of the vServer (Full Access), but not allowing the action: Delete on Resource: server, to ensure User: System1 does not delete any servers.
