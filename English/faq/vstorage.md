# vStorage

### \[vStorage] What is a Token?

A Token is a string of characters used for authentication in requests performed on the vStorage system using the HTTP protocol. It is transmitted within each request in the form of a Restful API with the following header: "X-Auth-Token: gAAAAABjsYvUCXdVOkJ…".

### \[vStorage] What is the purpose of obtaining a token?

Client tools, SDKs, Restful APIs obtain tokens for reuse, which helps requests originating from user client tools, SDKs, Restful APIs to be faster than having to obtain a new token each time a request is made.

### \[vStorage] What are the permissions and validity period of a token?

The Token represents the Username/Password across the entire vStorage project, therefore having full permissions on the project and is valid for 1 hour. After each hour, you need to obtain a new token to continue using the vStorage service.

### \[vStorage] How can I recover a project from the vStorage service?

Please refer to the documentation at the [Renew a Project ](../vstorage/features-of-vstorage/working-with-projects/renew-a-project.md)Link.

### \[vStorage] I can't download objects from the vStorage storage service, it reports error 400.

When downloading objects from the vStorage storage service, if you encounter an error with HTTP status code 400, please check the accuracy of the URI (object path) of the object on vStorage, the parameters passed in the header/params in the object download request. Additionally, please check the URI encoding/decoding when uploading files to the vStorage service and downloading objects. Ensure consistent use of encoding/decoding methods for URIs. If the error persists, please provide accurate information on how you are trying to download the object so we can investigate and assist.

Regarding URI encoding/decoding, you can refer to the following links:

[https://www.urlencoder.io/java/](https://www.urlencoder.io/java/)&#x20;

[https://www.urlencoder.io/php/](https://www.urlencoder.io/php/)

### \[vStorage] I'm using vStorage and I find the website limiting. Can I use a tool to connect to storage for file upload and folder creation?

Currently, vStorage is compatible with user-side tools such as:

* SDK S3 AWS
* SDK SWIFT
* GUI-based user tools: Cyberduck, S3 Browser
* CLI-based user tools: Swift CLI, Rclone, S3cmd, Duplicity

&#x20;Please refer to the documentation on working with [3rd party softwares](../vstorage/3rd-party-softwares/) for more details.

### \[vStorage] Why do I see my project missing when I check vStorage?

Please double-check if you are in the correct region where you initialized the project. If it's a different region, you may not see the project created in that region.

### \[vStorage] Why do I get an "Unauthorized" error when accessing my uploaded storage file?

Please check if you have made the container public. If not, access the project containing the container you want to upload files to, then switch the container to public mode as instructed in the [Make Container Public](../vstorage/features-of-vstorage/working-with-containers/make-container-public.md) and[ Make Container Private](../vstorage/features-of-vstorage/working-with-containers/make-container-private.md) guides.

### \[vStorage] How can I connect vCDN and vStorage?

Please configure the connection on the vCDN using the S3 Origin protocol as instructed in the [vCDN](../vcdn/) guide.

### \[vStorage] How can I delete unused storage?

Please access the administration page and delete the projects that are no longer needed. If your account is prepaid and the project still has usage time remaining, when you delete the project, you will be refunded the unused amount based on the actual number of days you did not use the project on the project's storage cycle that you initially purchased. This refunded amount will be added to your credit wallet balance. For details, refer to the [Delete a Project ](../vstorage/features-of-vstorage/working-with-projects/delete-a-project.md)guide.

### \[vStorage] When I upload files to my storage, I get an error and can't view MP4 files. Files under 10MB can be viewed.

There could be various reasons for this error, but the quickest solution is to delete the problematic file and then upload the desired files again.

### \[vStorage] I've just created storage on vngcloud, how do I upload files or folders?

Please refer to the upload file guide at [Upload Objects](../vstorage/features-of-vstorage/working-with-directories-and-objects/upload-objects.md) and the folder operation guide at [Create Folder](../vstorage/features-of-vstorage/working-with-directories-and-objects/working-with-directories.md).

### \[vStorage] Accessing the API reports a 404 error.

There could be many reasons for a 404 error, and one possible cause is an incorrect Auth-URL. Please double-check your Auth-URL.

### \[vStorage] What support does vStorage offer for controlling access to resources?

Currently, vStorage supports access control management through:

* Root user account on the vStorage service. See [Root User Accoun](../vstorage/identity-and-access-management/managing-vstorage-access-account/root-user-account.md)t for details.
* IAM user account on the vStorage service. See[ Identity and Access Management](../vstorage/identity-and-access-management/) for details.

IAM (limits access to vStorage through the vIAM system according to specified policies), IP range ACLs (limits access to vStorage projects or containers from certain IP addresses defined through IP/Subnet lists set in metadata at project or container level, or both levels), and vStorage Credentials (allows you to create key pairs that you can use through 3rd party software to access vStorage projects/containers). See [Identity and Access Management](../vstorage/identity-and-access-management/) for details.

### \[vStorage] Can I grant permissions on each directory, each object, or do I have to grant permissions on all objects within a container?

You can grant permissions at the object/directory/container levels through the vStorage IAM feature. See [Access Permissions and Woking thourgh IAM](../vstorage/identity-and-access-management/managing-access-to-vstorage-resources/access-permissions-and-working-through-iam/) for details.

### \[vStorage] Can I mount vStorage as a hard drive on vServer for use as a data volume?

You can use 3rd party software like Rclone/S3cmd to set up vStorage mount for use as a network drive. See the guides[ here](../vstorage/usecase/migrate-data/rclone-mount-vstorage-to-window-server.md) or [here](../vstorage/usecase/migrate-data/rclone-mount-vstorage-to-local-drive-on-linux-skip-to-end-of-metadata.md) if you are using Linux.

### \[vStorage] Where can I view actual monthly traffic and requests? Is real-time support available?

You can view traffic and request information as per the instructions in [Viewing Project Properties](../vstorage/features-of-vstorage/working-with-projects/viewing-project-properties.md).

### \[vStorage] What types of traffic are considered international traffic in the vStorage service?

Traffic leaving the territory of Vietnam is considered international traffic. You can view traffic information as per the instructions in[ Viewing Project Properties.](../vstorage/features-of-vstorage/working-with-projects/viewing-project-properties.md)

### \[vStorage] How are vStorage request fees calculated?

For Silver/Archive storage classes, request fees are incurred when you interact with objects. When these request volumes exceed the free tier (predefined by us and displayed on the interface when you [create a project](../vstorage/features-of-vstorage/working-with-projects/create-a-project.md)), the excess request volumes will be accumulated and billed as additional charges on a bill for exceeding the limit at the end of the month. Request-based actions include:

* GET: Used to retrieve information from the server based on the provided URL. For example, retrieving metadata of account lists, containers, objects, or retrieving the content of objects.
* HEAD: Similar to GET but the response does not include a body, only HTTP headers. For example, Content-Type, Accept-Encoding, Accept-Charset.
* POST: Sending metadata information, object content (data) to the server. For example, uploading a file to the server.
* PUT: Overwriting all information of the object with what is sent to the server. For example, overwriting the content of an object previously uploaded to the server.
* DELETE: Deleting the object from the server. For example, deleting an object previously uploaded to vStorage.&#x20;

You can also refer to our billing guide at [Billing management](../billing-management/) on VNG Cloud for more details.
