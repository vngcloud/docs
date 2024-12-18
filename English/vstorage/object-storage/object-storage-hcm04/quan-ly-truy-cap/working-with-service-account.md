# Working with Service Account

## **Overview** <a href="#tong-quan" id="tong-quan"></a>

**Service Account** is an identity that you can create in your account that has specific permissions. Service Account has some similarities to IAM users. Service Account and IAM User Account are both identities with Policies that define what the identity can and cannot do with VNG Cloud resources. However, Service Account is an identity used by an application or a machine, not a person, to make authorized API calls and access specified resources.

***

## Create a Service Account <a href="#khoi-tao-service-account" id="khoi-tao-service-account"></a>

To create a Service Account, follow the steps below:

1. Log in to [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/) with Root User Account.
2. Select **Service Account** .
3. Select **Create a Service Account.**
4. In the **Add information** section , enter **the Name** you want. The Service Account name must be from 1 (minimum) to 50 (maximum) characters long and can only include uppercase letters, lowercase letters (az, AZ), numbers (0-9), periods (.), underscores (\_), hyphens (-) and spaces ( ). The Service Account name should not contain sensitive information (e.g. IP address, login password, etc.) and the Service Account name must be unique on a VNG Cloud account until the Service Account is deleted. For example, the following Service Account name is valid: SA\_Client\_tool\_01.
5. In the Trusted relationship field, enter Account Root IS if you want to add association information between the Service Account and the Root User Account.
6. Select **Next step** .
7. In the **Add permission** section , you can:
   1. Select 1 or more policies that you have to associate with the Service Account. The vIAM system supports you to assign multiple policies to a Service Account. If these policies contain independent permissions, they will complement each other (ie the permission list is merged). On the contrary, if these policies contain conflicting permissions, you will not be able to access the corresponding resources according to this permission list (ie the permission list is merged and when conflicting, they will cancel each other out).
   2. If the policy list does not have the policy you want, you can continue with the steps below and we accept policy creation after creating the Service Account.
8. Select **Copy** to copy the Secret key. You must collect this information to access vStorage using the Service Account.
9. Select **Download** to download this secret key and store it on your local device.
10. Select **Back to list** to return to the screen containing the Service Account list.

After you complete the 10 steps above, a Service Account has been created.

<figure><img src="../../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

***

## Assign permissions to work with the project to the Service Account <a href="#phan-quyen-lam-viec-voi-project-vstorage-api-cho-service-account" id="phan-quyen-lam-viec-voi-project-vstorage-api-cho-service-account"></a>

### Create an IAM Policy <a href="#khoi-tao-iam-policy" id="khoi-tao-iam-policy"></a>

To initialize a policy used to access vStorage resources, follow the steps below:

1. Log in to [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/) with Root User Account.
2. **Select the Policy** folder .
3. Select **Create a Policy** .
4. Enter **Name** and **Description** if given for Policy.
5. Select **Next step** .
6. Select **Product as&#x20;**<mark style="background-color:blue;">**vstorage-hcm04**</mark> .
7. Select **Actions** :
   1. Select **Allow permissions** : by default, the vIAM system will always be on, which means allowing permissions to be applied to the policy. If you turn this mode off, the system will deny (reverse) the corresponding permissions.
      1. **Allow permissions** : allow access according to the selected action.
      2. **Deny permissions** : deny access according to the selected action.
   2. Select <mark style="background-color:blue;">**All vstorage-hcm04 actions**</mark> if you want to create a policy that has the right to perform all actions on vStorage. Or you can select some specific actions that you want to authorize for the Service Account.
8. Select **Resources** : select **All resources.**
9. Select **Request conditions:** enter special conditions for the policy if any.

<figure><img src="../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

### Attach IAM Policy to Service Account <a href="#attach-iam-policy-vao-service-account" id="attach-iam-policy-vao-service-account"></a>

Once you have created the desired Service Account and Policy, you will need to link the Service Account to the policy as per the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/) with Root User Account.
2. Select the Service Account folder **.**
3. Select **the Service Account** you want to assign permissions to.
4. Select **Attach policies** .
5. Select the **policies** you want. The vIAM system supports you to assign multiple policies to a Service Account. If these policies contain independent permissions, they will complement each other (ie the permission list is merged). On the contrary, if these policies contain conflicting permissions, you will not be able to access the corresponding resources according to this permission list (ie the permission list is merged and when conflicting, they will cancel each other out).
6. Select **Attach** .

<figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

***

## Assign permissions to work with bucket/object to the Service Account <a href="#phan-quyen-lam-viec-voi-bucket-object-cho-service-account" id="phan-quyen-lam-viec-voi-bucket-object-cho-service-account"></a>

To grant access to bucket/object for Service Account, you need to grant permission via Bucket Policy, specifically the steps are as follows:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .
2. Select icon![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F2Ye0SwJ9LL3dubdbJhKn%252Fimage.png%3Falt%3Dmedia%26token%3Dcee711e0-ec36-4c9d-ab5f-c8537e348626\&width=300\&dpr=4\&quality=100\&sign=d8575ee1\&sv=2)in the project containing the bucket you want to grant permissions to.
3. In the **Identity and Access Management** section , copy the **vStorage User ID** information in the **List of Service Account** section .

<figure><img src="../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

1. Continue to select **the Bucket** you want to assign permissions to the Service Account.
2. **Select the Action** icon and select **Configure policy.**

<figure><img src="../../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

1. Here, you can choose the configuration for each **Statement** on the left or directly edit the JSON file in the right column. Specifically, the structure of a Bucket Policy includes:

* **Version** : Specifies the version of the Bucket Policy (recommended `"2012-10-17"`).
* **Statement** : Each policy will have one or more **Statements** (specific purposes of the policy).
  * **Effect** : `Allow`or `Deny`access.
  * **Principal** : The object granted access, which is the IAM vStorage User ID information you copied above
  * **Action** : Actions allowed on the bucket, for example: `s3:GetObject`(view object), `s3:PutObject`(upload object), `s3:DeleteObject`(delete object),…
  * **Resource** : Specific buckets and objects affected by the policy (using ARN to identify resources).
  * **Condition** : (Optional) Specific condition that restricts access.

5\. Select **Save** to save the Bucket Policy configuration.

<figure><img src="../../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

***

## Work with vStorage API via Service Account <a href="#thuc-hien-lam-viec-voi-vstorage-api-thong-qua-service-account" id="thuc-hien-lam-viec-voi-vstorage-api-thong-qua-service-account"></a>

Follow the steps below to work with vStorage via Service Account

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .
2. Select the Integration folder **.**
3. **Select the vStorage API** icon .
4. In the **Authentication** section , you need to fill in the necessary information to configure your vStorage API including:
   1. Enter **the Client ID** . A **Client ID** is a string of characters used by the Service API to identify your application, and is also used to construct the "authorization URL" displayed to the user. You can create and manage **Client IDs** through the vIAM system. **The Client ID** is automatically generated when you create a new **Service Account** .
   2. Enter **the Client Secret** corresponding to **the Client ID** you just entered. The Client ID and Client Secret pair are created and managed by you through the vIAM system. You can select [Click here to manage your Client ID.](https://hcm-3.console.vngcloud.vn/iam/service-accounts) so we can navigate you to the vIAM system and in detail the Service Account management screens.
5. Once you've finished selecting your **authentication** configuration , select **Authentication** to go to the Configuration screen **. Here you can use the vStorage APIs directly, or you can use the API via Postman** . You can always come back here to change your **Authorization** information , then select **Authentication** again to update the S3 Rest API list with your new parameters.

For details, please refer to [https://docs.api.vngcloud.vn/service-docs/vstorage-api.html](https://docs.api.vngcloud.vn/service-docs/vstorage-api.html) .

<figure><img src="../../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

***

## Delete Service Account <a href="#xoa-service-account" id="xoa-service-account"></a>

To cancel (delete) a previously created Service Account, follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/) with Root User Account.
2. Select **Service Account** .
3. On the list of existing Service Accounts, select one or more Service Accounts that you want to cancel (delete).
4. Select **Delete** .

Once the Service Account is successfully cancelled, you will no longer be able to use this Service Account to access vStorage. Be careful when cancelling (deleting) a Service Account as you will not be able to recover this deleted account.
