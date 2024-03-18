# Sticky Session

As we know HTTP is stateless (the following request does not depend on the previous request result), so to store data between pages, people use session.

The most common example is an authentication token that is stored in the session to confirm the user has logged into the system. User authentication information is stored in the session, this time the session is stored in a certain server and is not synchronized between web servers. This is what causes logged in users to be logged out when their request is forwarded to a different web server than the server receiving their login request.

To solve the above problem can use ways like:

* Use Cluster for web server application, with session stored in one place accessible to all servers.
* Store session information to a common Database or a file system server on the application server.

Building a Cluster system or a Database requires a lot of experience with the system. That's why VNG CLOUD has provided the Sticky Session feature to help transfer all user requests in a session to a certain server, simplifying for users.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802707/image2020-5-12_15-6-14.png?version=1&#x26;modificationDate=1685077021000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


The **Enable Sticky Session** feature is available in the  Pool Settings page, which can be enabled via **ADD POOL** or **EDIT POOL**.
