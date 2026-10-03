# Access Management via IAM

Access management is an essential element of security that determines who can access certain data, applications, and resources, and under what conditions.

Access control policies rely mainly on techniques such as authentication and authorization, allowing organizations to clearly verify that users are who they claim to be and are granted the appropriate level of access based on user information, roles, and other factors.

Through IAM, GreenNode users, specifically on the vConsole website, can proactively grant or be granted access/action permissions for each specific feature.

To learn more, users should understand:

* **What IAM is and how to use it:** See the guide here
* **Access IAM at**: [https://iam.console.greennode.ai/](https://iam.console.greennode.ai/)

Once you understand how vIAM works and how to use it, you can access vIAM to grant permissions for vConsole features as follows

#### **How to grant vConsole feature permissions via vIAM** <a href="#accessmanagementviaiam-howtograntvconsolefeaturepermissionsviaviam" id="accessmanagementviaiam-howtograntvconsolefeaturepermissionsviaviam"></a>

***

* Step 1: Go to the IAM website [here](https://iam.console.greennode.ai/)
* Step 2: Create a **Policy**
  * 2.1: Select the vConsole product
  * 2.2: Select the feature groups that are allowed or denied access for each functional page in vConsole

| Access level | Usage Report                                                         | Billing History                                                  | Payment History | Credit History | Other Features                                                    |
| ------------ | -------------------------------------------------------------------- | ---------------------------------------------------------------- | --------------- | -------------- | ----------------------------------------------------------------- |
| List         | ListUsages                                                           | ListBillings                                                     | ListPayments    | List Credit    | <p><br></p>                                                       |
| Read         | <p>ExportUsages</p><p>GetTrafficUsages</p><p>ExportTrafficUsages</p> | <p>ExportBillings</p><p>GetBillingStatistic</p><p>GetBilling</p> | ExportPayments  | ExportCredits  | <p>GetUserInfo</p><p>ResultBackBuyCredit</p><p>GetUserBalance</p> |
| Write        | <p><br></p>                                                          | <p><br></p>                                                      | <p><br></p>     | <p><br></p>    | BuyCredit                                                         |

* Step 3: The Policy is created successfully
* Step 4: Create a **User Account** / **Group Permissions & Users**
  * If you create Group Permissions, remember to add the User Account to the newly created Group
* Step 5: Attach the newly created Policy to the Group Permission / User Account
* Step 6: You have now completed granting vConsole feature permissions to the user in the IAM system. The IAM user can log in to [https://dashboard.console.greennode.ai/](https://dashboard.console.greennode.ai/) with the provided username and password, then access and use the features they have been granted permission to.
