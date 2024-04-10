# Make container private

vStorage supports the default Private container mode for each container. This mode is used when you need to switch from Public container mode to Private container mode. The feature to switch from Public container mode to Private container mode is called **Private container**. **Private container** is a feature that allows users to stop publicly sharing a container in the cloud computing environment. You will not be able to access the container via a URL without access authentication.

&#x20;Use vStorage Portal

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).

2\. Select the **project** and choose the **container** you want to switch to private mode.

3\. Click ![](https://docs.vngcloud.vn/download/thumbnails/67994111/image2023-3-6\_10-24-4.png?version=1\&modificationDate=1700711635000\&api=v2) or click on the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994111/image2023-2-6\_10-20-54.png?version=1\&modificationDate=1700711635000\&api=v2)at the container you want to modify using the Private container feature and choose ![](https://docs.vngcloud.vn/download/thumbnails/67994111/image2023-11-23\_10-57-55.png?version=1\&modificationDate=1700711876000\&api=v2).

4\. The **Make private** screen will appear. Click on **Make private.**

After completing these 4 steps, the Private container feature will be activated. Private access is granted to the container and objects through the Access Control List (ACLs). This setting restricts access to all objects within the container to individuals with specific access rights as defined in the Access Control List (ACLs).

***

&#x20;Use vStorage API

In addition to the traditional management interface, we also provide an API that allows you to integrate with your user-facing applications and tools using vStorage for data storage.

To switch a container to private mode via vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).
