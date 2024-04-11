# Set tags for objects

Tag is a label attached to an object for the purpose of identification, classification, or providing additional relevant information about the object. In vStorage, when you upload objects, we support tagging for one or more of these objects.

To set up tags for objects, you can follow the instructions below:

&#x20;Use vStorage Portal

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).

2\. Choose the **project**, **container**, and then select the **objects** for which you want to set up tags.

3\. Click ![](https://docs.vngcloud.vn/download/thumbnails/67994245/image2023-3-6\_10-57-38.png?version=1\&modificationDate=1701073082000\&api=v2)or select the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994245/image2023-2-6\_10-20-54.png?version=1\&modificationDate=1701073083000\&api=v2)at the object you want to set tag and choose ![](https://docs.vngcloud.vn/download/attachments/67994245/image2023-3-6\_10-58-34.png?version=1\&modificationDate=1701073083000\&api=v2)

The set up **Tags** screen will appear.

4\. Enter the tags you want to assign to the selected object; labels are separated by commas (,). Click **Add**, then **Update**.

After completing these four steps, tags have been successfully set up for your object. We have a maximum character limit for all tags of an object, and it should not exceed (see the section on object scope and limits). Therefore, we encourage you to carefully consider which tags to assign to an object, as well as the total number of tags that can be assigned to that object.

***

&#x20;Use vStorage API

In addition to the traditional management interface, we also provide an API that allows you to integrate with your user-facing applications and tools using vStorage for data storage.

To set up tags for an object via the vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).

***

&#x20;Use 3rd party softwares

vStorage is also compatible with user-side tools using the S3 protocol. You can easily use familiar tools like Rclone, s3cmd, Cyberduck, etc.

To set up tags for an object via the 3rd party software, please refer to the [3rd Party Softwares](https://docs.vngcloud.vn/display/VSEN/3rd+Party+Softwares).
