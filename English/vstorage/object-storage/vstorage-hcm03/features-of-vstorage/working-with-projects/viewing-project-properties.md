# Viewing project properties

After creating a project and performing actions on that project, you can view and use the properties for the project, including general project information, access members, created S3 key pairs, action history, as well as information connecting the project to S3.

To view properties for a project, you can:

&#x20;Use vStorage Portal

1\. Log in to [https://vstorage.console.vngcloud.vn/storage](https://vstorage.console.vngcloud.vn/storage).

2\. Select the icon ![image2023-2-1\_14-25-3.png](https://docs.vngcloud.vn/download/attachments/49648432/image2023-2-1\_14-25-3.png?version=1\&modificationDate=1675236304000\&api=v2) at the **project** you want to view details for.

3\. On the page displaying detailed **project** **information**, you can view and use the properties for the project.

* **Information**: Provides general information about the project such as Total Quota, Total Bandwidth, Total Used Capacity, Total number of requests to the project, Total download count, Total upload count, Project type, Account URL, Temp URL key. You can view detailed changes in traffic, used capacity over desired periods by selecting Details in these information sections.
* **Members**: Provides information about members who have been granted access to the project from the old vStorage Portal. We only support the Add Member feature on the old vStorage Portal. Now you can grant access permissions to users from the vIAM access control system provided by GreenNode. See more at: Access control.
* **IP range ACLs**: Provides information about the IP/ Subnet that has been granted access to the project. See more at: Using IP range ACLs project feature.
* **S3 keys**: Provides information about the S3 key pairs initialized for the project from the old vStorage Portal. We only support the Initialize S3 keys feature on the old vStorage Portal. Now you can initialize S3 key pairs from the vIAM access control system provided by GreenNode. See more at: Access control.
* **History**: Provides information about the history of actions taken on the project, including the type of action, action status, time the action occurred, and a detailed description of the action if available.
* **Connection Information**: Provides commands and configuration files to connect the project to S3.

***

&#x20;Use vStorage API

In addition to the traditional management interface portal, we also provide APIs that allow you to integrate vStorage with your user-facing applications and tools for data storage.

To view information about a project through the vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).

