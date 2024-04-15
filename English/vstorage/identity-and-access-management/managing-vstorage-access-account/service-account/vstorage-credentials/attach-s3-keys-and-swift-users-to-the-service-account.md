# Attach S3 Keys and Swift Users to the Service Account

After you created the desired S3 keys and Swift users and set up **Restriction by IAM to YES**, the next step is to associate these credentials with the Service Account. Follow the instructions below:

1. Log in to [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/]\(https://hcm-3.console.vngcloud.vn/iam/\)) using your Root User Account.
2. Navigate to the vStorage credentials menu.
   1. For S3 keys: Select the S3 tab and ensure the toggle is switched on ![](https://docs.vngcloud.vn/download/thumbnails/69468389/image2023-6-30\_9-44-16.png?version=1\&modificationDate=1703473020000\&api=v2) to successfully enable IAM control.
3.
   1. For Swift users: Select the Swift tab and ensure the toggle is switched on ![](https://docs.vngcloud.vn/download/thumbnails/69468389/image2023-6-30\_9-44-16.png?version=1\&modificationDate=1703473020000\&api=v2) to successfully enable IAM control.
4. Go to the **Service Account** section.
5. Choose the specific **Service Account** where you want to link S3 keys and Swift users.
6. Select **Security credential**.
7. Under **vStorage credential**, click **Attach**.
8. Choose the **S3** **keys** and **Swift users** you want to link to the selected Service Account. The vIAM system supports linking multiple S3 keys and Swift users to one Service Account. However, each S3 key or Swift user can only be linked to one Service Account.

After completing these steps, you can now use the Service Account to access vStorage resources. For more information, please refer to [Access Permissions and Working Through Service Account](https://docs.vngcloud.vn/display/VSEN/Access+Permissions+and+Working+Through+Service+Account).
