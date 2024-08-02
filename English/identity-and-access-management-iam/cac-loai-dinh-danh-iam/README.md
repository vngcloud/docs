# Types of IAM Identifiers

IAM Identities are entities in the Identity and Access Management (IAM) system that represent IAM User Accounts, User Groups, and Service Accounts. IAM Identities are used to securely manage access to resources and services in a cloud environment. Each IAM Identity has a unique set of credentials and associated permissions that define the actions they can perform on specific resources.

#### Root User Account <a href="#iamidentities-rootuseraccount" id="iamidentities-rootuseraccount"></a>

Root User Account is an entity you first create in VNG Cloud and use, by default has full access to all VNG Cloud products/services and resources in that account.

#### User Account <a href="#iamidentities-useraccount" id="iamidentities-useraccount"></a>

IAM User Account is an entity that represents a user interacting with VNG Cloud on the Portal interface. An IAM User Account in VNG Cloud includes login information (username, password) and is denied access by default. IAM User Accounts are not separate accounts; they are users in the same Root User Account and do not need to have a payment method registered with VNG Cloud. Any activities performed by IAM User Accounts in the Root User account will be charged to that Root User account.

If you have employees who need access to VNG Cloud, do not share the Root User account login information with them. Instead, create separate IAM User Accounts in the Root User account and grant different permissions to each IAM User Account. Learn more detailed instructions at:

* [Quản lý User Account](tai-khoan-user-accounts/).

#### User Group <a href="#iamidentities-usergroup" id="iamidentities-usergroup"></a>

IAM User Groups are collections of IAM User Accounts. IAM User Groups simplify permissions management by allowing you to grant, change, and remove access to multiple User Accounts at once. For example, you can create a User Group called "Admins" and assign administrative permissions to that Group. Any IAM User Account in the Group automatically has the permissions assigned to that Group. Learn more at:

* [Quản lý User Group](tai-khoan-user-groups.md)

#### Service Account <a href="#iamidentities-serviceaccount" id="iamidentities-serviceaccount"></a>

Service Account is an identity you can create under your Root User account with specific permissions. Service Account has some similarities to IAM User Account. Both Server Account and User Account are identities with permission policies that define what that identity can and cannot do with VNG Cloud resources. However, Service Accounts are identities used by applications or computers, not people, to make authorized API calls and access specific resources. Learn more detailed instructions at:

* [Quản lý Service Account](../../vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-tai-khoan-service-account.md)

#### vStorage credentials <a href="#iamidentities-vstoragecredentials" id="iamidentities-vstoragecredentials"></a>

vStorage credentials are a feature that is specific to the vStorage product/service. vStorage credentials include key pairs that allow you to create and grant access to vStorage resources. There are two main types of vStorage credentials:&#x20;

* S3 Key: The S3 key includes an access key and secret key that integrates with vStorage to ensure integration with S3 Client tools such as s3cmd and the S3 SDK.&#x20;
* Swift User: Contains user/password information and is the primary authentication method supported by vStorage.

**vStorage credentials access**

1. When S3 keys or Swift users are created, by default they have full access to all vStorage projects/objects (with Restricted by IAM set to NO). To enable proper access control for these key pairs and users, you need to enable Restricted by IAM by setting it to YES.&#x20;
2. Once you enable Restricted by IAM to YES, IAM will manage and grant permissions to these key pairs and users. Therefore, by default, enabled key pairs and users will not have access to any vStorage projects/objects.&#x20;
3. After enabling Restricted by IAM to YES, to grant permissions, you need to associate these key pairs and users to a Service Account so that they inherit the permissions assigned to the attached Service Account. Find more detailed instructions on how to use and apply vStorage credentials on vStorage resources at:

* [Cách hoạt động của vStorage credentials](./#iamidentities-vstoragecredentials)

#### Identity Provider <a href="#iamidentities-identityprovider" id="iamidentities-identityprovider"></a>

Identity Providers are services that allow users to authenticate their identity and access multiple applications and services with a single set of credentials, using authentication protocols to securely exchange identity information and manage access control policies. Our system currently supports SAML2 as the primary authentication protocol, facilitating secure identity exchange between IDPs (Authentication Providers) and VNG Cloud (Service Provider). SAML2 has proven to be effective in enabling single sign-on (SSO) and seamless access to multiple applications and services.

* To integrate with our system using SAML, you can use our SAML entity ID: https://signin.vngcloud.vn/auth/realms/iam
* This URL acts as the endpoint to initiate the SAML authentication process and securely exchange identity information.&#x20;

Find more detailed instructions at:

[Quản lý Identity Providers](thiet-lap-identity-providers.md)
