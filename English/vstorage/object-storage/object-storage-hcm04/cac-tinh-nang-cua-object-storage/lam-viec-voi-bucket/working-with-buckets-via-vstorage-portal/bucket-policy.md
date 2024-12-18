# Bucket Policy

## Overview <a href="#tong-quan" id="tong-quan"></a>

**The vStorage Bucket Policy** feature is a powerful tool for managing access to your buckets through JSON rules. It gives you granular control over the actions that an IAM User (coming soon), another vStorage account, or external sources can perform on your bucket and the objects within it. Here are the basic instructions for configuring Bucket Policy:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .
2. Select the icon ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F2Ye0SwJ9LL3dubdbJhKn%252Fimage.png%3Falt%3Dmedia%26token%3Dcee711e0-ec36-4c9d-ab5f-c8537e348626\&width=33\&dpr=4\&quality=100\&sign=d8575ee1\&sv=2)in **the project** containing **the bucket** you want to grant permissions to.
3. If you want to delegate bucket permissions to a **Root User Account** or another **IAM User Account** or **Service Account** , you need to know the **vStorage User ID** of the user you want to delegate permissions to:
   1. For **Root User Account : you can get vStorage User ID** information right on the **project** information page as shown below.

<figure><img src="../../../../../../.gitbook/assets/image (423).png" alt=""><figcaption></figcaption></figure>

b. For **IAM User Account** and **Service Account : you can get vStorage User ID** information in **Identity and Access Management**

<figure><img src="../../../../../../.gitbook/assets/image (424).png" alt=""><figcaption></figcaption></figure>

4. Continue to select **the Bucket** you want to perform authorization.
5. **Select the Action** icon and select **Configure policy.**

<figure><img src="../../../../../../.gitbook/assets/image (41) (1).png" alt=""><figcaption></figcaption></figure>

4\. Here, you can choose the configuration for each **Statement** on the left or directly edit the JSON file in the right column. Specifically, the structure of a Bucket Policy includes:

* **Version** : Specifies the version of the Bucket Policy (recommended `"2012-10-17"`).
* **Statement** : Each policy will have one or more **Statements** (specific purposes of the policy).
  * **Effect** : `Allow`or `Deny`access.
  * **Principal** : The object to which access is granted (IAM User (coming soon), specific vStorage account).
  * **Action** : Actions allowed on the bucket, for example: `s3:GetObject`(view object), `s3:PutObject`(upload object), `s3:DeleteObject`(delete object),…
  * **Resource** : Specific buckets and objects affected by the policy (using ARN to identify resources).
  * **Condition** : (Optional) Specific condition that restricts access.

<figure><img src="../../../../../../.gitbook/assets/image (42) (1).png" alt=""><figcaption></figcaption></figure>

4\. Select **Save** to save the Bucket Policy configuration.

***

## Example <a href="#vi-du-minh-hoa" id="vi-du-minh-hoa"></a>

### **Example 1: Grant public-read permission to the entire bucket** <a href="#vi-du-1-cap-quyen-public-read-chi-doc-cho-toan-bo-bucket" id="vi-du-1-cap-quyen-public-read-chi-doc-cho-toan-bo-bucket"></a>

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

_Grant everyone ( `*`) read permission ( `s3:GetObject`) to all objects in the bucket._

***

### **Example 2: Grant only a specific vStorage User permission to upload and delete objects** <a href="#vi-du-2-chi-cap-quyen-cho-mot-vstorage-user-cu-the-tai-len-va-xoa-object" id="vi-du-2-chi-cap-quyen-cho-mot-vstorage-user-cu-the-tai-len-va-xoa-object"></a>

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { "AWS": "arn:aws:iam:::user/vStorage user ID" },
      "Action": ["s3:PutObject", "s3:DeleteObject"],
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

_Only users with vStorage user IDs in the file are allowed to upload ( `s3:PutObject`) and delete ( `s3:DeleteObject`) objects._

***

### **Example 3: Block all vStorage Users (except Root User Account) from acting on buckets and objects** <a href="#vi-du-3-chan-tat-ca-vstorage-user-tru-root-user-account-action-vao-bucket-va-object" id="vi-du-3-chan-tat-ca-vstorage-user-tru-root-user-account-action-vao-bucket-va-object"></a>

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Principal": "*",
      "Action": [
        "s3:*"
      ],
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ]
    }
  ]
}
```

_Do not allow anyone other than the Root User to work with buckets and objects._

### **Example 4: Only grant permission to users using IP address 10.0.0.1 to be able to take action to get object information** <a href="#vi-du-4-chi-cap-quyen-cho-nguoi-dung-su-dung-dia-chi-ip-10.0.0.1-moi-co-the-action-lay-thong-tin-obj" id="vi-du-4-chi-cap-quyen-cho-nguoi-dung-su-dung-dia-chi-ip-10.0.0.1-moi-co-the-action-lay-thong-tin-obj"></a>

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Principal": "*",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ],
      "Condition": {
        "NotIpAddress": {
          "aws:SourceIp": "10.0.0.1"
        }
      }
    }
  ]
}
```

_Only users with IP address 10.0.0.1 can get object information_

### **Example 5: Add multiple statements in a JSON file** <a href="#vi-du-5-them-nhieu-statement-trong-mot-file-json" id="vi-du-5-them-nhieu-statement-trong-mot-file-json"></a>

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ]
    },
    {
      "Effect": "Allow",
      "Principal": { "AWS": "arn:aws:iam:::user/vStorage user ID" },
      "Action": ["s3:PutObject", "s3:DeleteObject"],
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ]
    },
    {
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:PutBucketEncryption",
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ]
    }
  ]
}
```

_Allow all users to GetObject + allow only 1 vStorage user in the file to PutObject and DeleteObject + Disallow all users to perform PutBucketEncryption_

{% hint style="info" %}
**Attention:**

* **Check public permissions** : Some Bucket Policies may result in public access rights. You should check carefully to ensure data security.
* **Bucket Policy and ACL** : Ensure that the permissions in the Bucket Policy do not conflict with **the Access Control List (ACL)** of the bucket or object.
{% endhint %}
