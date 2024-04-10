# Versioning container

Versioning is a term used to refer to a specific release or iteration of software, documentation, or other data. We provide you with versioning functionality to work with multiple versions of stored data. Versioning is a feature that supports storing multiple historical versions of objects within a container. You can use versioning to preserve, access, and restore all versions of stored objects in your container. When versioning is enabled, instead of completely deleting an object from the system when uploading or deleting it, we move deleted or overwritten objects to a versioning container. From there, you can easily restore accidentally deleted objects or download previous versions of data when needed.



&#x20;Use vStorage Portal

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).

2\. Select the **project** and choose the **container** for which you want to enable versioning.

3\. Click ![](https://docs.vngcloud.vn/download/thumbnails/67994094/image2023-3-6\_10-15-7.png?version=1\&modificationDate=1700710529000\&api=v2)or select the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994094/image2023-2-6\_10-19-45.png?version=1\&modificationDate=1700710529000\&api=v2) at the **container** and choose ![](https://docs.vngcloud.vn/download/thumbnails/67994094/image2023-11-23\_10-37-0.png?version=1\&modificationDate=1700710621000\&api=v2)at the container where you want to enable versioning.

4\. The **Enable Container versioning** screen will appear. Enter the **Container version name**.

Once a container is created, you cannot change its name. For more information on naming containers, please refer to [Containers naming rule](https://docs.vngcloud.vn/display/VSEN/Containers+naming+rule).

5\. Click **Enable versioning.**

After completing the described 5 steps, the container versioning feature is now enabled. If you have multiple containers in one project, and all containers need to use the versioning feature, you should give unique names to the versioning containers and not create more than one versioning container for a single container.

To download a versioned object, refer to [Download objects](https://docs.vngcloud.vn/display/VSEN/Download+objects).

***

&#x20;Use vStorage API

In addition to the traditional management interface portal, we also provide APIs that allows you to integrate vStorage with your user-facing applications and tools using for data storage.

To enable container versioning via the vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).
