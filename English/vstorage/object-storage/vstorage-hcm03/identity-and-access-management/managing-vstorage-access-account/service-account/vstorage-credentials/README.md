# vStorage Credentials

vStorage Credentials are key pairs that allow you to create and grant access to vStorage projects/containers. vStorage credentials consist of two main types:

* **S3 Key:** This is a pair of S3 keys with an access key and a secret key integrated into vStorage to be compatible with S3 client tools like s3cmd, S3 SDK, etc.
* **Swift User:** This is a user/password pair directly supported by vStorage.

**Permissions of vStorage Credentials:**

* When S3 keys/Swift users are created, by default, they have full access to vStorage projects/containers (with Restriction by IAM set to NO). To control and manage the permissions for these key pairs and users, you need to first enable the Restriction by IAM property to YES.
* Once you enable Restriction by IAM to YES, these key pairs and users will be managed and permissioned by IAM. Consequently, by default, the enabled key pairs and users won't have access to any vStorage project/container.
* After enabling Restriction by IAM to YES, to grant permissions, you need to associate these keys and users with Service Accounts to inherit the permissions assigned to the linked Service Account.
