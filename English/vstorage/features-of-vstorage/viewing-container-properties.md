# Viewing container properties

Once you've created a container and uploaded objects to that container, you can view detailed information about the container and use the features we provide for the container, including ACLs, Lifecycle, CORS, and more.

To view detailed information about a container, you can:

&#x20;Use vStorage Portal

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
2. Choose the **project** containing the **container** you want to view details of.
3. Select the **container** you want to view details of.
4. On the page displaying detailed information about the container, you can view and use the features we provide for the container, including:

* **General Information**: Provides general information about the container, such as Container Name, Total objects, Size, Owner, Creation time, Last modified time, Accessibility, Versioning,&#x20;
* **ACLs**: Provides information on access management (Read/Write/Read+Write) for one or more Root accounts with access permission on the container. For details on how to use this feature, see Access Control Lists (ACLs) for containers.
* **IP range ACLs**: Provides information about IP addresses/Subnets that have access rights to the container. To learn more about using this feature, see Using IP range ACLs for containers.
* **CORS**: Provides information about the allowed access paths to resources in the container. For details on how to use this feature, see Sharing CORS container resources.
* **Lifecycle**: Provides information about the lifecycles set up for the container. For details on how to use this feature, see Using container lifecycle features.

***

&#x20;Use vStorage API

In addition to the traditional management interface portal, we also provide APIs that allows you to integrate vStorage with your user-facing applications and tools using for data storage.

To view container properties via the vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).

***

&#x20;Use 3rd party softwares

vStorage is also compatible with user-side tools using the S3 protocol. You can easily use familiar tools such as Rclone, s3cmd, Cyberduck, and more. Check out 3rd party softwares to learn how to integrate and use these tools.

To view container properties via 3rd party software, please refer to the [3rd Party Softwares](https://docs.vngcloud.vn/display/VSEN/3rd+Party+Softwares).
