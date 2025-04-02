# Access Management

On region HCM04, you can use 4 types of accounts to access vStorage. Details of these 4 types include:

* **Root User Account:** Is the first account [created](https://register.vngcloud.vn/signup) to access VNG Cloud with full access to all resource services on VNG Cloud.
* **IAM User Account, Service Account:** Is an account created from the single Root user account with access rights depending on the access policy set from the Root user account.

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **S3 keys:** Is a pair of s3 keys with access key and secret key integrated by vStorage for compatibility with S3 client tools such as s3cmd, s3 SDK,...

Refer to the table below to get an overview of how accounts work on vStorage:

<table data-full-width="true"><thead><tr><th width="197">Account Type</th><th>Access Channel</th><th>Place of Origin</th><th>Default Permission</th><th>Working with project</th><th>Working with buckets</th></tr></thead><tbody><tr><td>Root User Account</td><td>vStorage Portal</td><td>Initialize for the first time when using the service on VNG Cloud</td><td>Full rights on project and bucket</td><td>Yes</td><td>Yes</td></tr><tr><td>IAM User Account</td><td>vStorage Portal</td><td>IAM Portal</td><td>No access to any resources yet</td><td>Yes, permissions via IAM Policy</td><td>Yes, permissions via Bucket Policy</td></tr><tr><td>Service Account</td><td>vStorage API</td><td>IAM Portal</td><td>No access to any resources yet</td><td>Yes, permissions via IAM Policy</td><td>Yes, permissions via Bucket Policy</td></tr><tr><td>S3 keys</td><td>3rd party software</td><td>vStorage Portal</td><td>Depends on account creation</td><td>No</td><td>Yes, permissions depend on the type of user that created the S3 key</td></tr></tbody></table>
