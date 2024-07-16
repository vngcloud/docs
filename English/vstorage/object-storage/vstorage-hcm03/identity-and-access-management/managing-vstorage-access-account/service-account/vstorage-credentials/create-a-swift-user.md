# Create a Swift user

To create a Swift user, follow the steps below:

1\. Log in to [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/]\(https://hcm-3.console.vngcloud.vn/iam/\)) with your Root User Account.\
2\. Choose the **vStorage credentials** directory.\
3\. Select **Swift** from the list.\
4\. Click on **Create a Swift user**.\
5\. Choose the **Region** containing your project on vStorage.\
6\. Select the **vStorage project** for which you want to create the Swift user.\
7\. Click **Create**.\
8\. Choose **Copy** or **Download** to retrieve the Username/Password information you just created.

Note: After pressing the Create Swift user button, make sure to **save the Username/Password** pair for future use. If you don't store this information immediately, you won't be able to retrieve the Password for this Swift user later.

**Note:**&#x20;

1. When a Swift user is created, the default state of the Restriction by IAM property for this Swift user is set to NO (**Restriction by IAM = NO**). In this state, you can use this Swift user to access resources within the selected project when creating the Swift user. The vIAM system will not perform permission checks for this Swift user.
2. If you enable the Restriction by IAM property for this Swift user, setting it to YES (**Restriction by IAM = YES**), the Swift user will be managed and have permissions checked by the vIAM system. Therefore, to use these Swift users, you need to **associate them to a Service Account** to inherit the permissions on the associated Service Account. For detailed information, please refer to [Attach S3 Keys and Swift Users to the Service Account](https://docs.vngcloud.vn/display/VSEN/Attach+S3+Keys+and+Swift+Users+to+the+Service+Account).
