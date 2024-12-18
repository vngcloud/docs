# Integrate S3 SDK with vStorage

To see instructions for integrating the S3 SDK with vStorage, you can do so via the vStorage Portal by following the instructions below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .
2. Select the Integration folder **.**
3. **Select the S3 SDK** icon .
4. In the **Authentication** section , you need to fill in the necessary information to configure your S3 SDK to integrate with vStorage including:
   1. Select a **Project** from the list of existing projects in the Region you selected earlier. If the list of projects displayed is incomplete, you can select , we will reload the latest list of projects at the time you perform this action.
   2. Select an **Access key** from the list of existing access keys in the project you selected earlier.
   3. Enter the corresponding **Secret key** of the selected **Access key . The access key and secret key pair are created and managed by you through the vIAM system. You can select** [Click here to enter vIAM and manage s3 keys](https://hcm-3.console.vngcloud.vn/iam/vstorage-credentials/s3) so that we can navigate you to the vIAM system and the S3 keys management screens in detail. For more information about S3 keys, see [Initialize vStorage Credentials](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-service-account/khoi-tao-vstorage-credentials) .
5. **Once you've finished selecting your Authentication** configuration , select **Configure S3 SDK to go to the Configuration** screen . You can always come back here to change your **Authorization information, then select Integrate S3 SDK** again to update your usage with your new settings. You can see instructions on how to integrate S3 SDK in different languages ​​by following the steps below:
   1. Choose a Programming **Language** you want to integrate from the list of programming languages ​​we provide, including: Java, Python, Golang, Ruby, C#, NodeJS.
   2. Select a **Library** that you want to communicate with the server APIs.

Below is a list of languages, libraries and their corresponding versions that we provide for you to integrate with vStorage:

<figure><img src="../../../../../.gitbook/assets/image (438).png" alt=""><figcaption></figcaption></figure>

6\. Now the screen with detailed instructions on how to integrate S3 SDK for the languages ​​is displayed. The integration instructions are displayed in 4 sections:

a. **Setup for this guide** : Contains instructions for installation and connection in **the language and library of your choice.**

b. **Write code** : Contains integrated source code for each feature when **Working with containers** and **Working with objects** in **the language** and **library** of your choice.

c. **Build and deployment** : Contains instructions for building and launching the S3 SDK in **the language** and **libraries** of your choice.

d. **Download sample code** : This section allows you to download the entire source code of the tutorial from the 3 sections above according to **the language** and **library** you choose.

You can choose the icon![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs.vngcloud.vn%2Fdownload%2Fthumbnails%2F59805522%2Fimage2023-5-18_13-37-39.png%3Fversion%3D1%26modificationDate%3D1689229600000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=6bf74a47\&sv=2)or![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs.vngcloud.vn%2Fdownload%2Fthumbnails%2F59805522%2Fimage2023-5-18_13-37-55.png%3Fversion%3D1%26modificationDate%3D1689229601000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=c759e6c2\&sv=2)to open or close each of these items. For each step we provide you with sample source code according to the credentials you entered earlier and the language or library you selected, you can choose Copy source code at each feature by selecting the icon![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs.vngcloud.vn%2Fdownload%2Fthumbnails%2F59805522%2Fimage2023-5-18_13-38-42.png%3Fversion%3D1%26modificationDate%3D1689229601000%26api%3Dv2\&width=300\&dpr=4\&quality=100\&sign=195df8dd\&sv=2)at each source code or you can also quickly search for the source code supporting the feature you want by selecting the feature in the **Index** section (right corner of the screen). If you want to download the entire source code for the S3 SDK integration guide for this language, select **Download** in the **Download sample code** section . So you have completed the integration of S3 SDK in one of the languages ​​you want.
