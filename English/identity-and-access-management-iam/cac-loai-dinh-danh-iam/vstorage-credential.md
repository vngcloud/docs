# vStorage Credential

**vStorage credentials** are a feature that supports vStorage products/services.

vStorage Credentials are key pairs that allow you to create and grant permissions to access vStorage projects/containers. vStorage credentials include 2 main types

* S3 key: is a pair of s3 keys with access key and secret key integrated by vStorage for compatibility with S3 client tools such as s3cmd, s3 SDK,...
* Swift user: is the main supported user/password pair of vStorage.

**vStorage credentials permissions**&#x20;

* When s3 key/swift user is created, by default it will still have full access to vStorage projects/containers (default Restriction by IAM setting is NO), to be able to authorize these key and user pairs, you first need to enable Restriction by IAM to YES When you enable Restriction by IAM to YES, these key and user pairs will be managed and authorized by IAM, so by default the enabled key and user pairs will not have access to any vStorage project/container.&#x20;
* After enabling Restriction by IAM to YES, to be able to authorize you need to attach the keys, users to Service Accounts so that they inherit the permissions on the attached Service Account.&#x20;
* Main features of vStorage credentials Initialize S3 key Initialize Swift user Associate S3 key, Swift user with corresponding Service Account Cancel S3 key, Swift user
