# Integrate S3cmd with vStorage

To see the instructions for integrating the S3cmd tool with vStorage, you can do it via the vStorage Portal following the instructions below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .
2. Select the Integration folder **.**
3. **Select the S3cmd** icon .
4. In the **Authentication** section , you need to fill in the necessary information to configure your S3cmd to integrate with vStorage including:
   1. Select a **Project** from the list of existing projects in the Region you selected earlier. If the list of projects displayed is incomplete, you can select , we will reload the latest list of projects at the time you perform this action.
   2. Select an **Access key** from the list of existing access keys in the project you selected earlier.
   3. Enter the corresponding **Secret key** of the selected **Access key . The access key and secret key pair are created and managed by you through the vIAM system. You can select** [Click here to enter vIAM and manage s3 keys](https://iam.console.vngcloud.vn/vstorage-credentials/s3) so that we can navigate you to the vIAM system and the S3 keys management screens in detail. For more information about S3 keys, see [Initialize vStorage Credentials](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials) .
5. After you have finished selecting the **Authentication** configuration , select **Configure S3cmd to go to the Configuration** screen . You can always come back here to change your **Authorization information, then select Configure S3cmd** again to update the usage according to your new parameters. You can see the instructions on how to install and configure S3cmd right on this screen. For more details, please refer to: [vStorage Integration.](https://vstorage.console.vngcloud.vn/integration/integration)
6. Select **Download Configuration file.**

**If you are using Windows operating system, continue following the steps below to complete the S3cmd integration with vStorage:**

1. Save the downloaded **s3cnf.s3cfg** configuration file to the **C:\Users\\\[User]\AppData\Roaming folder.**
2. Rename the file from **s3cnf.s3cfg** to **s3cmd.ini**
3. Download and install **Python** according to the instructions at [https://www.python.org/](https://www.python.org/) on your personal computer.
4. **Download the S3cmd** application according to the instructions at [https://s3tools.org/download](https://s3tools.org/download) to your personal computer.
5. **Extract** the downloaded **S3cmd** application file .
6. Open **Command Prompt on your computer or press Windows + R** key combination then type **cmd** and press **Enter.**
7. In **Command Prompt** , point to the **s3cmd** folder you just **extracted . The syntax for pointing** to the folder is as follows: cd \<path to the s3cmd folder>
8. At this point, you can use syntax to get **a list of buckets, upload objects** , and perform other operations on [3rd party softwares](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/3rd-party-softwares) .

<figure><img src="../../../../../.gitbook/assets/image (425).png" alt=""><figcaption></figcaption></figure>
