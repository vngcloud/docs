# Integrating S3cmd with vStorage

To view the guide on integrating the S3cmd tool with vStorage, you can follow the steps below using the vStorage Portal:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
2. Select the **Integration** directory.
3. Choose the **S3cmd** icon.
4. In the **Permission** section, fill in the necessary information to configure your S3cmd for integration with vStorage:
   1. Choose a **Region** that contains the project you want to access data to from the list of Regions we provide.
   2. Choose a **Project** from the list of existing projects in the previously selected Region. If the project list is not complete, you can choose to reload the latest project list at the time you perform this action.
   3. Choose an **Access key** from the list of existing access keys belonging to the previously selected project.
   4. Enter the corresponding **Secret key** for the selected Access key. The access key and secret key are created and managed through the vIAM system. You can click here to go to vIAM and manage S3 keys, where we will guide you to the vIAM system and details of the S3 keys management screens. For more information about S3 keys, see Initializing vStorage Credentials.
5. After completing the permission configuration, select **Configure S3cmd** to move to the **Configuration screen**. You can always come back here to change your permission information, then select Configure S3cmd again to update your usage according to your new parameters. You can see installation and configuration instructions for S3cmd right on this screen. For more details, refer to: Integration with vStorage.
6. Choose **Download** the configuration file.

#### If you are using the Windows operating system, continue with the following steps to complete the integration of S3cmd with vStorage: <a href="#integratings3cmdwithvstorage-ifyouareusingthewindowsoperatingsystem-continuewiththefollowingstepstoc" id="integratings3cmdwithvstorage-ifyouareusingthewindowsoperatingsystem-continuewiththefollowingstepstoc"></a>

1. Save the downloaded configuration file **s3cnf.s3cfg** to the **C:\Users\\\[User]\AppData\Roaming directory.**
2. Rename the file from **s3cnf.s3cfg** to **s3cmd.ini**.
3. Download and install **Python** from \[[https://www.python.org/\](https://www.python.org/)](https://www.python.org/]\(https://www.python.org/\)) on your personal computer.
4. Download the **S3cmd** application from \[[https://s3tools.org/download\](https://s3tools.org/download)](https://s3tools.org/download]\(https://s3tools.org/download\)) to your personal computer.
5. **Extract** the downloaded **S3cmd** application file.
6. Open the **Command Prompt** on your computer or press the **Windows + R** key combination, then enter **cmd** and press **Enter**.
7. In the **Command Prompt**, **navigate** to the **s3cmd** directory you just **extracted.** The syntax for navigating to the directory is: cd \<path to the s3cmd directory>.
8. At this point, you can use commands to get a **list of containers, upload objects**, and perform other operations in 3rd party software.
