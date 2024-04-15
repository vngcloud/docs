# Create a S3 key

To create an S3 key, follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/]\(https://hcm-3.console.vngcloud.vn/iam/\)) with your Root User Account.
2. Select the **vStorage credentials** menu.
3. Choose **Create an S3 key.**
4. Enter the **Name** for the S3 key you wish to create.
5. Select the **Region** containing your vStorage project.
6. Choose the **vStorage project** for which you want to create the S3 key.
7. Click **Create**.
8. Select **Copy** or **Download** to retrieve the Access Key/Secret Key information you just created.

Note: After creating the S3 key, make sure to **save the Access Key/Secret Key** pair for future use. If you do not store this information immediately, you won't be able to retrieve the Secret Key later.

**Note:** &#x20;

1. When an S3 key is created, by default, its **Restriction by IAM** status is set to **NO**. In this state, you can use this S3 key to access resources within the chosen project during key creation. The vIAM system does not perform permission checks for this S3 key.
2. If you enable the **Restriction by IAM** attribute of the S3 key to **YES**, the key will be managed and subjected to permission checks by the vIAM system. Therefore, to use these S3 keys, you need to **associate them with a Service Account** to inherit the permissions of the linked Service Account. For details, please refer to [Attach S3 Keys and Swift Users to the Service Account](https://docs.vngcloud.vn/display/VSEN/Attach+S3+Keys+and+Swift+Users+to+the+Service+Account).
