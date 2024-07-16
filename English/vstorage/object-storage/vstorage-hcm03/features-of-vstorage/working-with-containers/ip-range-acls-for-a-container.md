# IP Range ACLs for a container

IP Range ACLs is a feature that allows users to proactively activate a safety mode at the internet network level, limiting access to a project or vStorage container from specified IP addresses or subnets through the IP/ Subnet list set up in metadata at the project or container level, or both.

Currently, vStorage only supports the IP Range ACLs feature for IPv4 and does not support IPv6. All references to IP below are to be understood as IPv4.

The IP Range ACLs feature supports both the S3 and HTTP protocols.

&#x20;Use vStorage Portal

To set up IP Range ACLs for a container, you can follow the instructions below via the vStorage Portal:

1\. Log in to https://vstorage.console.vngcloud.vn.\
2\. Choose the **project** and then select ![](https://docs.vngcloud.vn/download/thumbnails/67994184/image2023-5-24\_9-5-19.png?version=1\&modificationDate=1701052880000\&api=v2)at the container which you want to set up IP Range ACLs.\
3\. In the IP Range ACLs section, choose **Set IP Range ACLs**. To find out the number of IP/ Subnet you can set up for a container, please refer to Resource Limits.\
4\. By default, the selected container will have the access status set to **All IP/Subnets**. If you want to limit the number of IP addresses that can access your resources, choose **Specific IP/Subnets**.\
5\. If you choose **Specific IP/Subnets**, enter the **IP address** or **Subnet** (CIDR) (e.g., 125.212.100.101 or 125.212.100.0/24) and then choose **Add**. For more details, refer to IP address and CIDR ([https://en.wikipedia.org/wiki/Classless\_Inter-Domain\_Routing](https://en.wikipedia.org/wiki/Classless\_Inter-Domain\_Routing))

6\. The added **IP/Subnet** will be displayed in the list. If you want to remove this **IP/Subnet** from the list, choose ![](https://docs.vngcloud.vn/download/thumbnails/67994184/image2023-5-9\_13-17-46.png?version=1\&modificationDate=1701052880000\&api=v2)**.**\
7\. Choose **Update**.

After completing the 7 steps above, you have successfully set up IP Range ACLs for a container. If you use the Portal IP address or an IP within the IP/ Subnet list added to the container, you will have access to all resources of the container (including the container and the directories and objects within that container). **The container will inherit the IP range ACLs of the project to which it belongs.**

If you want to disable the IP Range ACLs for your container, meaning that all users have access to resources without considering IP addresses, choose **All IP/Subnets** when setting up IP Range ACLs.

After setting up IP Range ACLs, S3/ HTTP requests (including TempURL requests) to the container from invalid IP/ Subnet will be denied with a 403 error code.
