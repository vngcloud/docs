# Access Permissions and Working Through Service Account

To access your resources on the vStorage storage service, you can use various channels such as vStorage Portal, vStorage API, Swift Rest API, S3 Rest API, and 3rd party softwares. For the vStorage API, Swift Rest API, S3 Rest API, or 3rd party softwares, you will use a Service Account to access. If you don't have a Service Account, please refer to Service Account.

* To use the Service Account to access vStorage resources through vStorage API, S3 Rest API, Swift Rest API, see details in [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).
* To use the Service Account to access vStorage resources through 3rd party softwares, see details in [3rd Party Softwares](https://docs.vngcloud.vn/display/VSEN/3rd+Party+Softwares).

#### Below is an example illustrating the use of a Service Account to access vStorage resources through the S3cmd tool: <a href="#accesspermissionsandworkingthroughserviceaccount-belowisanexampleillustratingtheuseofaserviceaccount" id="accesspermissionsandworkingthroughserviceaccount-belowisanexampleillustratingtheuseofaserviceaccount"></a>

1. To create an S3 key, follow the instructions at Create S3 key.
2. If the S3 key you just created has the status **Restriction by vIAM = ON**, then proceed to create a Service Account following the instructions at Create Service Account, Create a policy for the Service Account, Link the Service Account to the corresponding policy. Otherwise, if the S3 key has the status **Restriction by vIAM = OFF**, proceed to step 4.
3. Link the S3 key to the Service Account following the instructions at Link S3 key, Swift user with the corresponding Service Account.
4. Integrate this S3 key with the S3cmd application. Details are as follows:
   1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
   2. Select the **Integration** menu.
   3. Select the **S3cmd** icon.
   4. In the **Permission** section, you need to provide the necessary information to configure your S3cmd to integrate with vStorage, including:
      1. Select a **Region** that contains the project you want to access data in from the list of Regions we provide.
      2. Select a **Project** from the list of existing projects in the previously selected Region. If the project list is not complete, you can choose , and we will reload the latest project list at the time you perform this action.
      3. Select an **Access key** that you just created in step 1 above.
      4. Enter the corresponding **Secret key** of the selected Access key. The access key and secret key pair is created and managed by you through the vIAM system. You can choose Click here to go to vIAM and manage s3 keys to be directed to the vIAM system and details of the S3 keys management screens.
   5. After completing the Permission configuration, select **Configure S3cmd** to go to the Configuration screen. You can always come back here to change your Permission information, then select Configure S3cmd to update the usage according to your new parameters. You can see instructions on how to install and configure S3cmd right on this screen.
   6. Press **Download** configuration file to your personal computer. The downloaded file will be named s3cnf.s3cfg.

***

#### If you are using the Windows operating system, continue with the following steps to complete the integration of S3cmd with vStorage: <a href="#accesspermissionsandworkingthroughserviceaccount-ifyouareusingthewindowsoperatingsystem-continuewith" id="accesspermissionsandworkingthroughserviceaccount-ifyouareusingthewindowsoperatingsystem-continuewith"></a>

1. Save the downloaded configuration file **s3cnf.s3cfg** to the directory **C:\Users\\\[User]\AppData\Roaming.**
2. Rename the file from **s3cnf.s3cfg** to **s3cmd.ini**.
3. Download and install **Python** following the instructions at [https://www.python.org/](https://www.python.org/) on your personal computer.
4. Download the **S3cmd** application as instructed at [https://s3tools.org/download](https://s3tools.org/download) to your personal computer.
5. **Extract** the downloaded **S3cmd** application file.
6. Open **Command Prompt** on your computer or press the **Windows + R** key combination, then enter **cmd** and press **Enter**.
7. In **Command Prompt**, **navigate** to the **s3cmd** folder you just **extracted**. The syntax for navigating to the folder is as follows: cd \<path to the s3cmd folder>
8. Now, you can use commands to retrieve a **list of containers**, **upload objects**, as well as perform other operations as specified in 3rd party softwares.

For more information on how to integrate and use other tools, please refer to [3rd Party Softwares](https://docs.vngcloud.vn/display/VSEN/3rd+Party+Softwares).
