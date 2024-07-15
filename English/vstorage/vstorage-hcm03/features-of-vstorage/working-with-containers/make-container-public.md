# Make container public

After you initialize a container, it will have a private status by default. You can change the container's mode from private to public, allowing anyone to access the container to view, download, and upload all files, objects within the public container. vStorage supports public data access for anonymous users, optionally on a per-container basis. This feature is known as a **Public container**. **Public container** is a feature that allows users to publicly share a container in a cloud computing environment. Users from the internet can access the container through a URL without the need for authentication access with the system. Public access carries inherent security risks, so if your scenario doesn't require that access, we advise against allowing public access for the container. At any time you no longer want to make the container public, you can switch the mode to private for the container.

**Use vStorage Portal**

Before you can switch the container to public mode, you need to set up Access Control Lists (ACLs) for the container, granting access to all users. For details, refer to the Container Access Control Lists (ACLs) section.

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).\
2\. Select the **project** and choose the **container** you want to make public.\
3\. Click icon ![](https://docs.vngcloud.vn/download/thumbnails/67994103/image2023-3-6\_10-20-30.png?version=1\&modificationDate=1700710828000\&api=v2)on the **container** or select icon ![](https://docs.vngcloud.vn/download/thumbnails/67994103/image2023-2-6\_10-20-54.png?version=1\&modificationDate=1700710828000\&api=v2)at the container you want to make public and choose ![](https://docs.vngcloud.vn/download/thumbnails/67994103/image2023-11-23\_10-51-14.png?version=1\&modificationDate=1700711475000\&api=v2).\
4\. The **Make public screen** appears. Click on **Make public.**

After completing these steps, the Public container feature is enabled. Public access is granted to the container and objects through Access Control Lists (ACLs). This setup allows anyone to access all objects within the container with the specified access rights through ACLs. For more information on the Set ACLs feature, see Container Access Control Lists (ACLs).

**Use vStorage API**

In addition to the traditional management interface portal, we also provide APIs that allows you to integrate vStorage with your user-facing applications and tools using for data storage.

To make container public via the vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).
