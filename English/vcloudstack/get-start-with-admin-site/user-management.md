# User Management

### Overview <a href="#tong-quan" id="tong-quan"></a>

Managing users accessing and using the network system is extremely sensitive and secure, this is even more important for internal systems provided to the company's employees.

Therefore, the User Management screen will fully describe the information of the users who are using and operating vCloudStack, including the following information:

* **User ID** : user ID on vCloudStack;
* **Email** : user email;
* **Status** : User activity status:
  * " _Active_ " is the state where the user is active and operating on vCloudStack;
  * " _Inactive_ " is the state in which the user is temporarily suspended (deactive) from using vCloudStack;
* **Roles** : user roles on vCloudStack;
* **Created at** : Date new user was added;
* **Updated at** : date user information was updated.

As a user administrator, this interface allows you to perform the following functions:

* Invite New User
* Set usage limit (Limit Quota)
* Deactivate user account

Details of the functions are described below.

***

### Invite new user to vCloudStack (Invite User) <a href="#moi-nguoi-dung-moi-vao-vcloudstack-invite-user" id="moi-nguoi-dung-moi-vao-vcloudstack-invite-user"></a>

Follow these steps:

Step 1: Administrator accesses Admin Site in vCloudStack;

Step 2: Select the User Administration screen;

Step 3: Click on the "Invite User" button;

Step 4: Fill in the email of the user you want to invite to use vCloudStack;

Step 5: Select the Roles of the invited user;

Step 6: Click the invite button to confirm inviting the new user.

{% hint style="info" %}


**Note:**

* The account (Email) of the user invited to vCloudStack must be the account previously registered to GreenNode.
* The default role for inviting users to use vCloudStack is "User". With this role, users can access vCloudStack User Site to create and operate. If they want to access vCloudstack Admin Site, the administrator must select the role of Admin or higher.
{% endhint %}

***

### Set resource usage limits (Limit quota) <a href="#thiet-lap-gioi-han-su-dung-tai-nguyen-limit-quota" id="thiet-lap-gioi-han-su-dung-tai-nguyen-limit-quota"></a>

Follow these steps:

Step 1: Administrator accesses Admin Site in vCloudStack;

Step 2: Select the User Administration screen;

Step 3: Find the user account you want to set usage limits for, in the Action column, select "Edit quota"

Step 4: The administrator changes the limit value in the "Current limit" column to change the usage limit depending on the limit criteria.

Step 5: Click Save to save the set usage limit.

{% hint style="info" %}


**Note:**

* Only users who have accessed the vCloudStack User site to activate the vCloudStack account can set resource usage limits for administrators.
* Only applies to users whose status is Active
{% endhint %}

***

### Deactivate user account <a href="#tam-ngung-tai-khoan-nguoi-dung-deactive" id="tam-ngung-tai-khoan-nguoi-dung-deactive"></a>

Follow these steps:

Step 1: Administrator accesses Admin Site in vCloudStack;

Step 2: Select the User Administration screen;

Step 3: Find the user account you want to temporarily suspend using vCloudStack, in the Action column, select "Deactive".

Step 4: A pop-up screen asks for confirmation of temporary suspension, select the Deactive button to confirm.

{% hint style="info" %}


**Note:**

* After the user account is deactivated, the status will be Inactive;
* Inactive user accounts will not be allowed to access the vCloudStack User Site and Admin Site.
{% endhint %}
