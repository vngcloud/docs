# Upload objects

An object is the fundamental storage unit in vStorage, representing the raw data and metadata information of a file uploaded to the vStorage system. You can use vStorage Portal, vStorage API, or 3rd party software to upload files to a container, and the details are described below.

To upload a file to vStorage, follow these steps:

&#x20;Use vStorage Portal

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).

2\. Choose the **project** and select the **container** where you want to upload the file. If you want to upload the file to a specific directory, choose that directory.

3\. Click on **Upload**.

The object upload screen will appear.

4\. Now, you can upload the file in two ways:

\- Drag the files from your device into the file upload area.\
\- Select **Choose Files to Upload**, then choose the file you want to upload from your device.

5\. Click **Open**.

6\. Click **Upload**.

At this point, your files are being uploaded, and their status is Uploading. When this status changes to **Success**, it means your file has been successfully uploaded.

During the upload process, you cannot perform other actions on the container. Once the object upload is complete, you can continue to use other features as usual.

All data you upload belongs to you, and VNG Cloud cannot interfere with or recover data deleted or overwritten by user errors. To prevent accidents related to overwriting or accidental deletion, it is recommended to back up container versions using the versioning feature. For details on the versioning feature, refer to Using the [Versioning container](https://docs.vngcloud.vn/display/VSEN/Versioning+container).

***

&#x20;Use vStorage API

In addition to the traditional management interface, we also provide an API that allows you to integrate with your user-facing applications and tools with vStorage for data storage.

To upload an object to a container via the vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).

***

&#x20;Use 3rd party softwares

vStorage is also compatible with user-facing tools using the S3 protocol. You can easily use familiar tools such as Rclone, s3cmd, Cyberduck, and more. Check out the \[3rd party software]\(link\_to\_3rd\_party\_software) section to learn how to integrate and use these tools.

To upload an object to a container via 3rd party software, please refer to the [3rd Party Softwares](https://docs.vngcloud.vn/display/VSEN/3rd+Party+Softwares).
