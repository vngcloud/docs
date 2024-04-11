# CORS for a container

CORS (Cross-Origin Resource Sharing) is a mechanism that allows many different resources on a web page to be requested from a different domain than the domain that served the web page, based on the HTTP protocol. CORS requests are made by adding HTTP headers instructing the web browser on how to use and manage cross-domain content, allowing the retrieval of data from a different page through HTTP requests containing headers specifying CORS.

CORS was created due to the same-origin policy, a security policy implemented in all modern browsers. This policy restricts access to resources from different domains for security reasons. Cross-origin resource sharing (abbreviated as CORS) is a standard for accessing web resources on different domains. CORS allows web scripts to interact more openly with content outside the origin domain, leading to better integration between web services.

Note: Currently, configuring CORS for a container only supports the HTTP protocol, not the S3 protocol. After setting up CORS for a website with a corresponding domain on the container, the website with that domain can make HTTP requests to this container.

To share CORS container resources, you can follow the instructions below:

&#x20;Use vStorage Portal

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/).

2\. Select the **project** and choose the **container** you want to share CORS resources.

3\. Click on ![](https://docs.vngcloud.vn/download/thumbnails/67994125/image2023-3-6\_10-29-22.png?version=1\&modificationDate=1700792972000\&api=v2)or select the icon ![](https://docs.vngcloud.vn/download/thumbnails/67994125/image2023-2-6\_10-20-54.png?version=1\&modificationDate=1700792972000\&api=v2) at the **container** where you want to use the CORS resource sharing feature and click ![](https://docs.vngcloud.vn/download/thumbnails/67994125/image2023-11-24\_9-34-46.png?version=1\&modificationDate=1700793287000\&api=v2).

4\. The **Set CORS Screen** appears. Choose the **Header** and corresponding **Value** for that Header. Click **Update**.

CORS allows configuration based on a specific domain, for example, [https://abc.com.vn](https://abc.com.vn/). Therefore, you need to enter the corresponding domain value in the Value field.

***

&#x20;Use vStorage API

In addition to the traditional management interface portal, we also provide APIs that allows you to integrate vStorage with your user-facing applications and tools using for data storage.

To set ACLS via the vStorage API, please refer to the [API developers](https://docs.vngcloud.vn/display/VSEN/API+developers).
