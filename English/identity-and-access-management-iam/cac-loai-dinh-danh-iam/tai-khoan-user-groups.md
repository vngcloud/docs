# User Groups

**Managing User Groups**&#x20;

An IAM User Group is a collection of IAM User Accounts. IAM User Groups simplify permissions management by allowing you to grant, change, and remove permissions to multiple IAM User Accounts at once. For example, you can create an IAM User Group called "Administrators" and grant administrative permissions to that group. Any IAM User Account in the group automatically has the permissions assigned to the group.

**How to create an IAM User Group?**&#x20;

To create a new IAM User Group:&#x20;

1. Go to IAM Console: https://hcm-3.console.vngcloud.vn/iam/&#x20;
2. Click "Group" in the left menu.&#x20;
3. Click "Create a group".&#x20;
4. Provide a group name and optional description.&#x20;
5. Assign relevant IAM Policies to the group to define the group's permissions.
6. Review the settings and click "Create group".

**How to assign Permissions to IAM User Group?**&#x20;

You can assign Policies to a Group while creating a new IAM User Group, or assign Policies to an existing IAM User Group. To assign Policies to an existing Group:&#x20;

1. Go to IAM Console - Groups page with URL: https://hcm-3.console.vngcloud.vn/iam/user-groups&#x20;
2. Log in as a Root User Account or a User Account with access rights.&#x20;
3. You need to provide a username/email and password when logging in.&#x20;
4. Search for an IAM User Group by entering its name in the search box and selecting the correct IAM User Group in the search results.&#x20;
5. By default, you will see the "Permission" tab on the IAM User Group details page.&#x20;
6. Click the "Attach Policies" button, then you will see a window appear containing all Policies.&#x20;
7. Search for the Policies you want to assign by typing the exact name of the Policies in the search box.&#x20;
8. Select the Policies you want to assign from the search results and click the "Attach" button in the lower right corner of the popup.&#x20;
9. Now, your IAM User Group will have all the permissions contained in the assigned Policies and ensure that all IAM User Accounts in the Groups inherit all these Permissions.

**3.How to assign an IAM User Account to an IAM User Group?**&#x20;

You can assign an IAM User Account to an IAM User Group while creating a new IAM User Group, or assign an IAM User Account to an existing IAM User Group. To assign an IAM User Account to an existing IAM User Group:&#x20;

1. Go to IAM Console - Groups page with the URL: https://hcm-3.console.vngcloud.vn/iam/user-groups&#x20;
2. Log in as a Root User Account or a User Account with access rights.&#x20;
3. You need to provide a username/email and password when logging in.&#x20;
4. Search for an IAM User Group by entering its name in the search box and selecting the correct IAM User Group from the search results.&#x20;
5. Click on the "User" tab on the IAM User Group details page.&#x20;
6. Click on the "Add user" button, then you will see a window appear containing all your IAM User Accounts.&#x20;
7. Select IAM User Account and click the "Add" button in the bottom right corner of the popup.&#x20;
8. Now, your IAM User Accounts will inherit all Group Permissions.

**4. Delete IAM User Group?**&#x20;

You can delete IAM User Group by doing the following 2 options:&#x20;

1. Delete multiple IAM User Groups at once:&#x20;

* Go to IAM Console with Root account or IAM User Account granted access Click "Group" in the left menu.&#x20;
* Select the IAM User Group you want to delete (a "Delete" button will be enabled in the upper right corner when you select at least one group).&#x20;
* Click the "Delete" button, a confirmation window will appear to make sure you don't delete the wrong Group, then click the "Confirm" button to complete the process.

2. Delete an IAM User Group: We recommend you to access the details of the IAM User Group and then delete it to make sure you don't delete the wrong Group.

{% hint style="info" %}
**Note**

*   Remember that once you confirm deletion of an IAM User Group, that Group cannot be restored.

    Review and assign new Policies to the IAM User Accounts that belong to the deleted IAM User Groups, to ensure that the IAM User Accounts continue to function properly.
{% endhint %}
