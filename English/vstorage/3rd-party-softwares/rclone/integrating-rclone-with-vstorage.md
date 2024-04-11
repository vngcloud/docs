# Integrating Rclone with vStorage

To view the instructions for integrating Rclone with vStorage, you can follow the steps below on the vStorage Portal:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
2. Select the **Integration** menu.
3. Choose the **Rclone** icon.
4. In the **Permission** section, fill in the necessary information to configure your Rclone for integration with vStorage, including:
   1. Select a **Protocol** for integrating Rclone with vStorage. Currently, we support 2 protocols: S3 or HTTPS.
   2. Choose a **Region** that contains the project you want to access data to from the list of Regions we provide.
   3. Select a **Project** from the list of existing projects in the chosen Region. If the project list is not complete, you can choose to refresh the list with the provided option.
   4. Choose an **Access key** from the list of access keys associated with the previously chosen project.
   5. Enter the corresponding **Secret key** for the selected **Access key**. The access key and secret key are created and managed through the vIAM system. You can click here to visit vIAM and manage S3 keys, and see the screens for managing S3 keys for more information. For details on S3 keys, refer to Initializing vStorage Credentials.
5. After completing the permission **configuration**, select **Configure Rclone** to move to the Configuration screen. You can always come back here to change your permission information, then select Configure Rclone again to update the usage according to your new parameters. You can see the instructions on how to install and configure Rclone right on this screen. For more details, refer to Integration with vStorage.
