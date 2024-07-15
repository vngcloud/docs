# Rename an object

You can also rename an object that you have uploaded to a container. To rename an object, follow the instructions below:

&#x20;Use vStorage Portal

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).

2\. Choose the **project**, **container**, and then select the **object** you want to rename.

3\. Click ![](https://docs.vngcloud.vn/download/thumbnails/67994238/image2023-3-6\_10-56-24.png?version=1\&modificationDate=1701071086000\&api=v2)or select the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994238/image2023-2-6\_10-20-54.png?version=1\&modificationDate=1701071087000\&api=v2) at the **object** you want to rename and choose ![](https://docs.vngcloud.vn/download/thumbnails/67994238/image2023-11-27\_14-46-51.png?version=1\&modificationDate=1701071214000\&api=v2).

4\. Enter the new name for the object. The object name should adhere to the description of the [Objects naming rule](https://docs.vngcloud.vn/display/VSEN/Objects+naming+rule).

When renaming an object, you should avoid changing the file type part (for example, abc.pdf, where .pdf is the file type) in the object name. Changing this extension part of the object's name may alter the content type of the object, leading to errors when downloading the object to your personal device.

***

&#x20;Use vStorage API

In addition to the traditional management interface, we also provide an API that allows you to integrate with your user-facing applications and tools with vStorage for data storage.

To rename an object via vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).

***

&#x20;Use 3rd party softwares

vStorage is also compatible with user-side tools using the S3 protocol. You can easily use familiar tools such as Rclone, s3cmd, Cyberduck, etc.&#x20;

To rename an object via 3rd party software, please refer to the [3rd Party Softwares](https://docs.vngcloud.vn/display/VSEN/3rd+Party+Softwares).
