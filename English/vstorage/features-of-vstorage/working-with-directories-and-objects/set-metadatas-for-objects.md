# Set metadatas for objects

Metadata is a type of extended information for a file (Object) that you have uploaded to the vStorage system. They can include common details such as name, creation date, size, file type (.doc, .pptx...) or properties that you are allowed to declare additionally to perform your specific tasks in application development.

To set up metadata for an object, you can follow the instructions below:

&#x20;Use vStorage Portal

\


1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).

2\. Choose the **project** and **container**, then select the **objects** for which you want to set up metadata.

3\. Click ![](https://docs.vngcloud.vn/download/thumbnails/67994253/image2023-3-6\_11-0-2.png?version=1\&modificationDate=1701073582000\&api=v2)or select the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994253/image2023-2-6\_10-20-54.png?version=1\&modificationDate=1701073582000\&api=v2) at the object you want to set up metadata for and choose ![](https://docs.vngcloud.vn/download/thumbnails/67994253/image2023-3-6\_11-0-24.png?version=1\&modificationDate=1701073582000\&api=v2)**.**

The set up **Metadata** screen will appear.

4\. We provide you with two methods to set up metadata:

\- **Default Key**: Select a key from the list of available keys that we provide.\
\- **Custom Key**: Create a custom key according to your needs with the prefix X-Object-Meta-Vng-.

5\. Enter the corresponding **Value** for the selected or created **Key**. Click **Add** and then choose **Update**.

After completing these 5 steps, metadata has been successfully set up for your object.

Currently, we support 8 types of default metadata keys, including: X-Robots-Tag, Cache-Control, X-Delete-At, Content-Disposition, Content-Encoding, Expires, Content-Language, Content-Type.

We have a limit on the total number of characters for all metadata of an object (see the section [Objects naming rule](https://docs.vngcloud.vn/display/VSEN/Objects+naming+rule)), so we encourage you to carefully consider which metadata to set for an object and the total number of metadata that can be set for that object.

***

&#x20;Use vStorage API

In addition to the traditional management interface, we also provide an API that allows you to integrate with your user-facing applications and tools using vStorage for data storage.

To set metadatas for objects through vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).

***

&#x20;Use 3rd party softwares

vStorage is also compatible with user-side tools using the S3 protocol. You can easily use familiar tools such as Rclone, s3cmd, Cyberduck, and more.

To set metadatas for objects through 3rd party software, please refer to the [3rd Party Softwares](https://docs.vngcloud.vn/display/VSEN/3rd+Party+Softwares).
