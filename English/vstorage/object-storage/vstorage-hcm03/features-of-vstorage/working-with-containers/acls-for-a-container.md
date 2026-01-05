# ACLs for a container

Access Control Lists (ACLs) is a feature of vStorage that allows the system to set access permissions (Read, Write, Read and Write) to a container and the objects within that container for one or more Root user accounts within the vStorage system.

You can grant Read, Write, or Read and Write permissions to one or all other Root user accounts (Root user accounts granted access through ACLs must be valid accounts within our GreenNode system).

* For Read permission: you can download objects from the granted container.
* For Write permission: you can upload and download objects from the granted container.

To set up access control ACLs, you can follow the instructions below:

&#x20;Use vStorage Portal

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).

2\. Choose the **project** and select the **container** for which you want to set ACLs.

3\. Click ![](https://docs.vngcloud.vn/download/thumbnails/67994117/image2023-3-6\_10-26-12.png?version=1\&modificationDate=1700712062000\&api=v2) or select the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994117/image2023-2-6\_10-20-54.png?version=1\&modificationDate=1700712062000\&api=v2) at the container and choose ![](https://docs.vngcloud.vn/download/thumbnails/67994117/image2023-11-23\_11-4-6.png?version=1\&modificationDate=1700712246000\&api=v2).

4\. The **ACLs Screen** will be displayed. In the **Access for other accounts** section, enter the email address or phone number of the Root user account to which you want to grant additional rights. The email or phone number you enter must be associated with a registered GreenNode account. If the email or phone number is not registered, access rights will not be added for this container.

5\. Select the corresponding access rights for the entered Root user account. The access rights provided include ContainerAdmin, ContainerViewer, ContainerReader, and ContainerEditor. Click **Update**.

6\. If you want all users to have access to the container with the same rights, follow similar steps in the **Public Access** section.

After completing the 7 steps described above, you have set up ACL access rights for the selected users. If there are access issues, you can adjust the access information of these Root user accounts to lower access rights.

***

&#x20;Use vStorage API

In addition to the traditional management interface, we also provide an API that allows you to integrate with your user-facing applications and tools using vStorage for data storage.

To set up access control ACLs via vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).
