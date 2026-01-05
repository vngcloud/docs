# Service Account

A Service Account is an identity that you can create within your account with specific permissions. It shares some similarities with IAM User Accounts. Both Service Accounts and IAM User Accounts are identities with policies that determine what the identity can and cannot do with GreenNode resources. However, a Service Account is an identity used by an application or a machine, rather than a human, to execute authorized API calls and access designated resources. For more information about Service Accounts, please refer to [https://documentation.vngcloud.vn/docs/vstorage/service-account.html](https://documentation.vngcloud.vn/docs/vstorage/service-account.html).

To access and work with vStorage resources using a Service Account, in addition to the Service Account, you need to create **vStorage Credentials**. These credentials consist of S3 keys and Swift user account pairs, which are attached to that Service Account.
