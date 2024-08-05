# Service accounts

Service Account is an identity that you can create under your Root User account and has specific permissions. It has some similarities with IAM User Account. To clarify, Service Account and IAM User Account are both identities with permission policies that define what that identity can and cannot do with VNG Cloud resources. However, Service Account is used by an application or machine, not a person, to make authorized API calls and access specified resources.

1. **How to Create a Service Account?**&#x20;

To create a new Service Account:&#x20;

1. Go to the IAM Console: https://hcm-3.console.vngcloud.vn/iam/&#x20;
2. Click "Service account" in the left menu.
3. Click "Create service account."&#x20;
4. Enter the Service Account information, including name and optional description.&#x20;
5. Attach the necessary Policies Review the settings and click "Create service account" in the upper right corner.&#x20;
6. Save Client Secret Key information

**2.Assign Permissions to Service Account**&#x20;

To assign Policies to Service Account:&#x20;

1. Go to IAM - Service Account page with URL: https://hcm-3.console.vngcloud.vn/iam/service-accounts&#x20;
2. Log in as Root User Account or User Account with access permission.&#x20;
3. You need to provide username/email and password when logging in.&#x20;
4. Search for Service Account by entering username in search box and selecting correct result in search result.&#x20;
5. By default, you will see "Permission" tab in Service Account detail page.&#x20;
6. Click on "Attach Policies" button, then you will see a pop-up window containing all Policies.&#x20;
7. Search for existing Policies by entering exact name of Policies in search box.&#x20;
8. Select Policies in search result and click "Attach" button in lower right corner of pop-up window.&#x20;
9. Now, your Service Account will have all the permissions contained in the attached Policies.

**3.How to Create Trusted Relationships**&#x20;

Trusted Relationships are a feature that allows for permissions to be shared between different Root User Accounts, allowing for customized and secure access authorizations on separate administrative entities. With this feature, different Root User Accounts can collaborate while maintaining privacy and security boundaries. This feature is especially useful in situations where multiple organizations or teams need to work together on shared resources, ensuring effective collaboration without sacrificing security.
