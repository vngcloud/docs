# Delete a container

You have created a container and uploaded/downloaded objects in that container. Currently, your business needs have changed, and you no longer require the created container. You can delete the container using the following methods:

To delete a container, you can:

&#x20;Use vStorage Portal

1\. Log in to https://vstorage.console.vngcloud.vn

2\. Choose the **project** and select the **container** you want to delete.

3\. Click ![](https://docs.vngcloud.vn/download/thumbnails/67994177/image2023-3-6\_10-38-41.png?version=1\&modificationDate=1701052447000\&api=v2)on the container or select the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994177/image2023-2-6\_10-20-54.png?version=1\&modificationDate=1701052448000\&api=v2) at the **container** you want to delete and choose ![](https://docs.vngcloud.vn/download/thumbnails/67994177/image2023-11-27\_9-36-22.png?version=1\&modificationDate=1701052584000\&api=v2).

After selecting Delete, the system will automatically navigate to the main screen. If you no longer see the container in the list, you have successfully deleted it. The container is now permanently removed from the system, and you cannot recover the container or any objects stored within it. Therefore, make sure to check your data before performing this action. If the container has versioning enabled, when you delete the container, all objects within the container will be transitioned into a version within the versioning-enabled container. You cannot delete container segments when deleting the parent container.

For more information about container segments, refer to the [Containers overview](https://docs.vngcloud.vn/display/VSEN/Containers+overview).

***

&#x20;Use vStorage API

In addition to the traditional management interface, we also provide an API that allows you to integrate with your user-facing applications and tools using vStorage for data storage.

To delete a container through the vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).

***

&#x20;Use 3rd party softwares

vStorage is also compatible with user-facing tools that use the S3 protocol. You can easily use familiar tools such as Rclone, s3cmd, Cyberduck, and others. Refer to the 3rd party softwares section to learn how to integrate and use these tools.

To delete a container using 3rd party software, please refer to the [3rd Party Softwares](https://docs.vngcloud.vn/display/VSEN/3rd+Party+Softwares).
