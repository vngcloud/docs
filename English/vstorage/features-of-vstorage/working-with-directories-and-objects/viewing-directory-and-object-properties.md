# Viewing directory and object properties

After you have created a directory and uploaded an object to the container or uploaded an object to the directory, you can view the information of that object/directory and use the features we provide for the object/directory, including moving, copying, renaming objects, etc.

To view the information of an object/directory, you can:

&#x20;Use vStorage Portal

1\. Log in to https://vstorage.console.vngcloud.vn.

2\. Select the **project**, then choose the **container** containing the **object/directory** you want to view detailed information.

3\. On the page displaying the list of objects/directories, you can view information for each object/directory in the data table, including:

* **Name**: Name of the object/directory.
* **Size**: For objects, we display the size of the uploaded object. For directories, this information is not applicable.
* **Storage class**: Storage class on the container containing the object/directory.
* **Last modified**: The most recent modification time of the object/directory.

4\. You can click on the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994200/image2023-7-13\_12-22-47.png?version=1\&modificationDate=1701054161000\&api=v2) at the object/directory you want to view in detail. When you select:

* **Object**: The screen displays detailed information for the selected object, including **Name, Size, Content type, Last modified, Path, Checksum information, Version information.**
* **Directory**: The screen displays detailed information for the selected directory, including **Name, Content type, Path, Version information.**

&#x20;Use vStorage API

In addition to the traditional management interface, we also provide an API that allows you to integrate with your user-facing applications and tools using vStorage for data storage.

To view information about an object/directory through the vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).

***

&#x20;Use 3rd party softwares

vStorage is also compatible with user-facing tools that use the S3 protocol. You can easily use familiar tools such as Rclone, s3cmd, Cyberduck, and more. Please refer to the 3rd party softwares documentation to learn how to integrate and use these tools.

To view information about an object/directory through 3rd party software, please refer to the [3rd Party Softwares](https://docs.vngcloud.vn/display/VSEN/3rd+Party+Softwares).
