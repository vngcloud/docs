# Integrating S3 SDK with vStorage

To view the integration guide for the S3 SDK tool with vStorage, you can follow the steps below through the vStorage Portal:

1. Log in to https://vstorage.console.vngcloud.vn.
2. Select the **Integration** menu.
3. Choose the **S3 SDK** icon.
4. In the **Permission** section, you need to provide the necessary information to configure your S3 SDK for integration with vStorage, including:
   1. Select a **Region** that contains the project you want to access data to from the list of Regions provided.
   2. Choose a **Project** from the list of existing projects in the selected Region. If the project list is not complete, you can choose to reload the latest project list at the time you perform this action.
   3. Select an **Access key** from the list of existing access keys belonging to the previously selected project.
   4. Enter the corresponding **Secret key** of the selected **Access key**. The access key and secret key are created and managed through the vIAM system. You can click \[here]\([https://vstorage.console.vngcloud.vn/docs/vIAM/s3keys](https://vstorage.console.vngcloud.vn/docs/vIAM/s3keys)) to go to vIAM and manage S3 keys, which provides details on managing S3 keys. For more information about S3 keys, see \[Initializing vStorage Credentials]\([https://vstorage.console.vngcloud.vn/docs/vStorageCredentials](https://vstorage.console.vngcloud.vn/docs/vStorageCredentials)).
5. After completing the configuration in the **Permission** section, select **Integrate S3 SDK** to go to the **Configuration screen**. You can always come back here to change your Permission information, then select Integrate S3 SDK again to update the usage according to your new parameters. You can view the guide on how to integrate the S3 SDK with various programming languages using the following steps:
   1. Choose a **Programming Language** you want to integrate from the list of programming languages we provide, including Java, Python, Golang, Ruby, C#, NodeJS.
   2. Select a **Library** you want to use to communicate with the server's APIs.

Here is the list of programming languages, libraries, and corresponding versions that we provide for you to integrate with vStorage:

| No        | Programming Language        | Library | Versions support              |
| --------- | --------------------------- | ------- | ----------------------------- |
| 1         | Java                        | AWS SDK | Java 8 và AWS SDK 1.11.163    |
| MinIO SDK | Java 8 và MinIO 8.5.2       |         |                               |
| 2         | Python                      | AWS SDK | Python 3.8 và Boto3 1.26.110  |
| MinIO SDK | Python 3.8 và Minio 7.1.14  |         |                               |
| 3         | Golang                      | AWS SDK | Go 1.17.10                    |
| MinIO SDK | Go 1.17.10                  |         |                               |
| 4         | Ruby                        | AWS SDK | Ruby 2.7.0                    |
| 5         | C#                          | AWS SDK | .Net 7.0 và AWS SDK 3.7.4     |
| MinIO SDK | .Net 7.0 và Minio 4.0.7     |         |                               |
| 6         | NodeJS                      | AWS SDK | Node 16.15.0                  |
| MinIO SDK | Node 16.15.0                |         |                               |

6\. Now the detailed integration guide for S3 SDK for various programming languages is displayed. The integration guide is divided into four sections:

a. **Setup for this Guide**: Contains instructions for installation and connection based on the selected language and library.

b. **Write Code**: Includes integration source code for each feature when working with vStorage containers and objects in the chosen language and library.

c. **Build and Deployment**: Provides instructions for building and running the S3 SDK in the selected language and library.

d. **Download Sample Code**: A section where you can choose to download the entire source code of the guide from the three sections above, based on your selected language and library.

You can select the icon or to expand or collapse each section. For each step, we provide sample code based on the authentication information you entered earlier and the language or library you selected. You can copy the source code for each feature by selecting the icon at each source code snippet, or you can quickly find source code supporting the desired feature by selecting the feature in the Index section (top right of the screen). If you want to download the entire source code for the S3 SDK integration guide for this language, select Download in the Download Sample Code section. With this, you have completed the integration of S3 SDK using the language of your choice.
