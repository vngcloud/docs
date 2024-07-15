# Managing Access to vStorage Resources

#### Overview <a href="#managingaccesstovstorageresources-overview" id="managingaccesstovstorageresources-overview"></a>

To access and work with resources from the vStorage service, you need to:

1. Have an account provided by the vStorage service (vStorage account).
2. Configure access permissions for the vStorage account to work with resources.
3. Accessing and Working with vStorage Resources Using a vStorage Account

#### vStorage Account <a href="#managingaccesstovstorageresources-vstorageaccount" id="managingaccesstovstorageresources-vstorageaccount"></a>

If you don't have a vStorage account, please refer to the Access Management documentation for information on the types of accounts supported by the vStorage service and how to allocate these account types.

#### Configuring Access Permissions for vStorage Account <a href="#managingaccesstovstorageresources-configuringaccesspermissionsforvstorageaccount" id="managingaccesstovstorageresources-configuringaccesspermissionsforvstorageaccount"></a>

When you create a container within projects to store data on vStorage, it's essential to control who has access to your containers and objects, as well as the permissions they should have. Additionally, you should decide whether you want to apply access permissions using individual authorization features on vStorage or use a unified access permission feature through the Identity and Access Management (vIAM) system.

* **Access Permissions and Working with Resources via vStorage**: Public Mode Switch Container: Control access to individual containers/objects using features such as Public Mode Switch Container, Private Mode Switch Container, ACLs Container Access Permissions, CORS Container Sharing, and Object Sharing.
* **Access Permissions and Working with Resources via vIAM**: Use the vIAM system to grant simultaneous access permissions to all objects in a container, containers in a project, or groups of objects and containers with a common name prefix.

You can also use both of the above permission mechanisms simultaneously to grant access permissions to resources (containers, objects). However, when using both mechanisms, vStorage access permissions take precedence over vIAM access permissions. Using both permission mechanisms simultaneously can lead to ambiguity and lack of clarity in resource access management, posing security risks. Therefore, it's recommended to use only one of the permission mechanisms for a resource to avoid security risks associated with permission leaks.

When granting access permissions to storage resources on vStorage, you decide who will receive permissions, what resources they will have permissions for, and specific actions you want to allow for those resources. The following sections provide an overview of vStorage resources and the best methods to control access to them.

For details on how to configure access permissions and work with vStorage resources, please refer to the following topics:

* Access Permissions and Working via vStorage
* Access Permissions and Working via IAM

Accessing and Working with vStorage Resources Using a vStorage Account

To access your resources (project, container, object, report, etc.) on the vStorage storage service, you can use vStorage accounts, including Root User Account, IAM User Account, and Service Account, to access resources through various user interfaces (access channels): vStorage Portal, vStorage API, Swift Rest API, S3 Rest API, and 3rd-party software.

| No | User type         | Channel                                                          | Note                                                                                                                                                                                        |
| -- | ----------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | Root User Account | vStorage Portal                                                  | You cannot use this account to access vStorage service resources through channels other than vStorage Portal.                                                                               |
| 2  | IAM User Account  | vStorage Portal                                                  | You cannot use this account to access vStorage service resources through channels other than vStorage Portal.                                                                               |
| 3  | Service Account   | vStorage API, Swift/ s3 client tool, Swift Rest API, S3 Rest API | You cannot use this account to access resources through the vStorage Portal. Additionally, you can use this account to integrate with the vStorage service from your software applications. |