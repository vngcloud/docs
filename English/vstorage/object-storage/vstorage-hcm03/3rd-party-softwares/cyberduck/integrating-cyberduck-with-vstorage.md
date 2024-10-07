# Integrating Cyberduck with vStorage

To view detailed instructions on integrating the Cyberduck tool with vStorage, please follow the steps below via the vStorage Portal:

1. Log in to https://vstorage.console.vngcloud.vn.
2. Select the **Integration** menu.
3. Choose the **Cyberduck** icon.
4. In the **Permission** section, you need to enter the configuration information for Cyberduck to integrate with vStorage, including:
   1. Select a **Region** containing the project you want to access data to from the list of Regions we provide.
   2. Choose a **Project** from the list of existing projects in the selected Region. If the project list is not complete, you can press the button to reload the latest project list.
   3. Choose an **Access key** from the list of access keys belonging to the project you selected earlier.
   4. Enter the **Secret key** corresponding to the selected **Access key**. The access key and secret key pair are managed through the vIAM system. You can click on Click here to visit vIAM and manage S3 keys to be directed to the vIAM system and view detailed S3 key management screens. For more information about S3 keys, please see \[Initializing vStorage Credentials]\(#).
5. After completing the **Permission configuration**, click **Integrate Cyberduck** to go to the **Configuration** screen. You can come back here to change the **Permission information**, then click **Integrate Cyberduck** again to update usage according to your new settings. You can also view the installation and configuration guide for Cyberduck right on this screen. For more details, please refer to \[Integrate vStorage]\(#).
6. Click **Download configuration file** to download the configuration file.

***

#### **Continue with the following steps to complete the integration of S3cmd with vStorage:** <a href="#integratingcyberduckwithvstorage-continuewiththefollowingstepstocompletetheintegrationofs3cmdwithvst" id="integratingcyberduckwithvstorage-continuewiththefollowingstepstocompletetheintegrationofs3cmdwithvst"></a>

1. Download the **Cyberduck** tool [https://cyberduck.io/download/](https://cyberduck.io/download/).
2. Open the **Cyberduck** application\*\*.\*\*
3. Choose **Open Connection** or **Bookmark + New Bookmark**.

<figure><img src="../../../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

4. Enter the connection information, including:

* **Protocol**: VNG HCM01 - AWS4. When you select this method, the Server, Port, and URL information will be automatically recorded and displayed.
* **Access key**: Enter the S3 access key you created from vIAM, which is also the access key information obtained from step 4 above.
* **Secret key**: Enter the S3 access key you created from vIAM, which is also the access key information obtained from step 4 above.

<figure><img src="../../../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

5\. Choose **Connect**.

6\. Now, Cyberduck has successfully connected to vStorage. You can now use Cyberduck to access vStorage, refer to the guide at \[Using Cyberduck Tool]\(#).

<figure><img src="../../../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
