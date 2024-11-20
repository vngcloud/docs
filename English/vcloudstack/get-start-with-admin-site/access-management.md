# Access Management

This article guides you on how to add users and grant permissions to use the vCloudStack service:

* [Add multiple users with Identity Provider (Azure AD)](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcloudstack/quan-tri-voi-admin-site/quan-ly-truy-cap#id-1-them-nhieu-user-voi-identity-provider-azure-a-d)
* [Add a user using vCloudStack](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcloudstack/quan-tri-voi-admin-site/quan-ly-truy-cap#id-2-them-mot-user-su-dung-vcloudstack)
* [User authorization for vCloudStack](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcloudstack/quan-tri-voi-admin-site/quan-ly-truy-cap#id-3-phan-quyen-user-su-dung-vcloudstack)

***

### 1/ Add multiple users with Identity Provider (Azure AD) <a href="#id-1-them-nhieu-user-voi-identity-provider-azure-a-d" id="id-1-them-nhieu-user-voi-identity-provider-azure-a-d"></a>

To add more Users to use the vCloudStack service system, the administrator needs to perform the following steps:

**Step 1:** Administrator accesses VNG Cloud homepage ( [dashboard.console.vngcloud.vn](https://dashboard.console.vngcloud.vn/) )

**Step 2:** Select to go to **IAM Portal** page of IAM;

**Step 3:** In the left navigation bar, select **Identity Provider** ;

**Step 4:** To create a Single-Sign-On integration service, synchronize user information to log in to vCloudStack, click "Add an Identity Provider"

**Step 5:** Fill in the required information fields to create the synchronization service:

* **Provider Name** : Enter the name of the service that synchronizes the login information;
* **Provider Type:** Select **SAML**
* **Vendor:** Select **Azure AD**
* **Login URL** : Fill in **the Login URL link from Microsoft Entra ID** (formerly Azure Active Directory)

{% hint style="info" %}


_Notes on how to get the Login URL link at Microsoft Entra ID:_

* To create a link, the admin must go to [portal.azure.com](https://portal.azure.com/#home) with the Microsoft Entra ID app.
* Create "New Application" in the Enterprise Application section, select the option "Integrate any other application you don't find in the gallery (Non-gallery)" to support Single-Sign-On with SAML.
* Add users who want to use vCloudstack in Users/Group section in the app
* Go to Single-Sign-On, select SAML method and from there get **Login URL link** .
{% endhint %}

**Step 5:** After filling in the Login URL link information, click **Save** ;

**Step 6** : The system will generate:

* Entity URL;
* Reply URL;
* Login URL;

Admin uses the Entity URL and Reply URL just created, then returns to the **Microsoft Entra ID app,** pastes the Entity URL and Reply URL at "Setup Single-Sign-On with SAML" and confirms (admin can test the synchronization after filling in the URLs).

**Step 7:** When the synchronization test is successful, the Admin can use the Login URL sent to the User to access and authenticate by Azure. If the authentication is successful, the User can be redirected to the vCloudStack User Site screen.

{% hint style="info" %}
**Note:** After successfully accessing the User Page, the user may not be authorized to use the vCloudStack service because the user function has not been authorized. Admin needs to authorize [the user to use vCloudStack](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcloudstack/quan-tri-voi-admin-site/quan-ly-truy-cap#id-3-phan-quyen-user-su-dung-vcloudstack) according to the instructions below.
{% endhint %}

***

### 2/ Add a user using vCloudStack <a href="#id-2-them-mot-user-su-dung-vcloudstack" id="id-2-them-mot-user-su-dung-vcloudstack"></a>

To add 01 user to use the vCloudStack service system, the administrator needs to perform the following steps:

**Step 1:** Administrator accesses VNG Cloud homepage ( [dashboard.console.vngcloud.vn](https://dashboard.console.vngcloud.vn/) )

**Step 2:** Select to go to **IAM Portal** page of IAM;

**Step 3:** In the left navigation bar, select **User Account,** the screen displays a list of IAM users ;

**Step 4:** To create more users, click **Create an user Account** ;

**Step 5:** Fill in the login name "Account User";

**Step 6:** Enter the password you want to set for the User Account (or click auto generate to have the system automatically generate the password);

**Step 7:** Click " **Create User Account** " to confirm creating more users.

{% hint style="info" %}


**Note:**

* After successfully accessing the User Page, the user may not be authorized to use the vCloudStack service because the user function has not been authorized. Admin needs to authorize [the user to use vCloudStack](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcloudstack/quan-tri-voi-admin-site/quan-ly-truy-cap#id-3-phan-quyen-user-su-dung-vcloudstack) according to the instructions below.
* For users who create accounts on the User account screen, they can only [assign](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vcloudstack/quan-tri-voi-admin-site/quan-ly-truy-cap#id-3-phan-quyen-user-su-dung-vcloudstack) authorization policies in step 8 - method 2.
{% endhint %}

***

### 3/ User authorization to use vCloudStack <a href="#id-3-phan-quyen-user-su-dung-vcloudstack" id="id-3-phan-quyen-user-su-dung-vcloudstack"></a>

To authorize ( **Policy** ) for Users to use the vCloudStack service system in the User Site and Admin Site portal, the administrator needs to perform the following steps:

**Step 1:** Administrator accesses VNG Cloud homepage ( [dashboard.console.vngcloud.vn](https://dashboard.console.vngcloud.vn/) )

**Step 2:** Select to go to **IAM Portal** page of IAM;

**Step 3:** In the left navigation bar, select **Policy** ;

**Step 4:** At the Policy list screen, to create a policy for users using vCloudStack, click the " **Create a Policy** " button;

**Step 5:** Fill in the Policy name and description to identify the Policy set for the user, then click **Next** ;

**Step 6:** Admin configures **policy** according to Product, Action, Resource, Condition.

**Step 7:** Click **Create Policy** to complete policy creation

{% hint style="info" %}


**Note:**

* If you want to grant permissions to users to use functions on the User Site screen: select Product _`vcloudstack`_;
* If you want to grant permissions to users to use functions on the Admin Site screen: select Product _`vcloudstack-admin`_;
{% endhint %}

**Step 8:** After creating a policy, there are 2 ways to assign the policy to the user:

* **Method 1: On the Policy** list screen
  * Select the policy you want to assign to the user;
  * Select the **Policy usage** tab ;
  * Press the **"Attach** " button;
  * Select Users, then click **Add** to add the selected users.
* **Method 2:** On the User Account screen
  * Select the user to whom the newly created policy should be applied;
  * In the **Permission** tab , display the policies applied to this user;
  * To add applicable policies, click " **Attach Policies** ";
  * Select the Policies, then click **Attach** to apply the policy to the user.
