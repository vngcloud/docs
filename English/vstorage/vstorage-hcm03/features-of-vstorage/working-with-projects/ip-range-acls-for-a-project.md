# IP Range ACLs for a project

IP Range ACLs is a feature that allows users to proactively activate a safety mode at the internet network level - limiting access to vStorage projects or containers from specific IP addresses determined through a list of IP/Subnet settings configured in metadata at the project or container level, or both.

Currently, vStorage only supports the IP Range ACLs feature for IPv4 and does not yet support IPv6. All references related to IP below will be understood as IPv4.

The IP Range ACLs feature supports both S3 and HTTP protocols.

To set up IP Range ACLs for a project, you can do so through the vStorage Portal using the instructions below:

&#x20;Use vStorage Portal

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).
2. Select the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994065/image2023-5-9\_13-12-33.png?version=1\&modificationDate=1700622740000\&api=v2) in the **project** you want to set up IP Range ACLs for.
3. Choose the **IP Range ACLs** section.
4. Select **Set IP Range ACLs**.
5. By default, the project you choose will have the access status set to **All IP/Subnets**. If you want to limit the number of IP addresses/Subnets that can access your resources, choose a **Specific IP/Subnets**. To know the number of IP/Subnets you can set up for a project, please refer to Resource Limits.
6. If you choose a **Specific IP/Subnets**, enter the IP address or Subnet (CIDR) (for example, 125.212.100.101 or 125.212.100.0/24) and then select **Add**. Refer to IP address and CIDR for details ([https://en.wikipedia.org/wiki/Classless\_Inter-Domain\_Routing](https://en.wikipedia.org/wiki/Classless\_Inter-Domain\_Routing)).
7. The added **IP/Subnets** are displayed in the list. If you want to remove this **IP/Subnets** from the list, select ![](https://docs.vngcloud.vn/download/thumbnails/67994065/image2023-5-9\_13-17-46.png?version=1\&modificationDate=1700622741000\&api=v2) .
8. Select **Update**.

After completing the 8 steps above, you have successfully set up IP Range ACLs for a project. Now, if you use the **Portal IP address** or an IP from the added IP/Subnet list for the project, you will have access to all resources of that project (including the project itself and the containers within that project).

If you want to disable IP Range ACLs for your project, meaning any user can access resources without considering the IP address, choose **All IP/Subnets** when setting up IP Range ACLs.

After setting up IP Range ACLs, S3/HTTP requests (including TempURL requests) to the project from invalid IP/Subnets will be denied with a 403 error code.
