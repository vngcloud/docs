# Pool in vCloudstack

Pool is an important component in the Load Balancing system, responsible for distributing traffic to backend servers to improve service performance, availability and reliability.

The main goal of a Pool is Load Balancing. The Pool ensures that traffic is distributed evenly and efficiently to the backend servers. This prevents any server from being overloaded while others are idle.

The pool consists of backend servers, called "Pool Members." Pool Members serve requests and responses to users or devices through the Load Balancer.

***

### How to add new Pool <a href="#add-and-updateapool-1.cachthemmoipool" id="add-and-updateapool-1.cachthemmoipool"></a>

* Go to Load Balancers;
* At Load Balancer, click to select the Load Balancer that needs to add a new Pool.
* In the Load Balancer details section, select the Pool tab.
* Click the "Add new Pool" button, an interface window appears allowing you to configure Pool information.
* In the new window, configure information such as:
  * Pool Name: Note that the Pool name cannot be changed after initialization.
  * HTTP protocol
  * Select load balancing algorithm: See more load balancing algorithms [Pool's algorithm](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/pool/pools-algorithm)
  * Enable/Enable Stick Session: See [Enable sticky session for more information.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/pool/enable-sticky-session)
  * Enable/Enable TLS Encryption: See [Enable TLS encryption for more information.](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/pool/enable-tls-encryption)
  * Health Check Settings: Refer to the instructions for installing Health Check for TCP/HTTP protocol at [Config health check setting](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/pool/config-health-check-setting)
  * [Add Pool Member: Refer to the Attach pool members](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/pool/pool-members/attach-pool-members) guide
* Click the "Add" button at the bottom right corner of the new add window to complete adding the Pool.

***

### How to update Pool information <a href="#add-and-updateapool-2.cachcapnhatthongtinpool" id="add-and-updateapool-2.cachcapnhatthongtinpool"></a>

* Go to the Load Balancer homepage;
* On the Load Balancer homepage, click on the Load Balancer that needs to be configured.
* In the Load Balancer details section, select the Pool tab.
* In the Pool list, hover over the Pool you want to edit and click the Edit icon.
* A pop-up window allows editing of the Pool, the information is allowed to be updated
  * Load Balancing Algorithm
  * Advanced health check configuration
* Click the "Save" button at the bottom right corner of the editing window to complete the Pool update.

***

### Pool Members <a href="#pool-members" id="pool-members"></a>

Pool Members are members of a group of servers (Pool) on the Load Balancer, and they are responsible for serving requests from users or other devices through the Load Balancer. Here is an explanation of how Pool Members work and their important properties:

**Weight**

* **Explanation** : Weight determines the priority of each Pool Member in processing requests. Members with high weight will receive more requests than Members with low weight.
* **For example** : If you have two Members with weights 3 and 1, Member with weight 3 will receive about 75% of requests, while Member with weight 1 will only receive about 25%.

**Port**

* **Explanation** : The port that the Member will listen on to process incoming requests. This port is usually related to the specific service the Member provides.
* **For example** : If you have a web application running on Member, you can use port 80 for HTTP and port 443 for HTTPS.

**Monitor Port**

* **Explanation** : This is the Port that the Load Balancer uses to check the health of the Member. The Load Balancer will send test requests to this Port to ensure that the Member is operating properly. If no Monitor Port is specified, the default Monitor Port = Port used to receive incoming requests.
* **For example** : If you want to check the health of a web server, you can use port 80 or 443 to check for availability.

**Backup Role**

* **Explanation** : This attribute defines the role of a Member in a Pool. There are two main roles: Primary and Backup. The Primary Member receives official requests from users, while the Backup Member receives requests only when the Primary Member is unavailable.
* **For example** : If you have two Members in a Pool, Member A has the Primary role and Member B has the Backup role, the request will be sent to Member A first. If Member A is unavailable, the Load Balancer will route the request to Member B.

In general, this mechanism allows you to customize how the Load Balancer distributes traffic among the Members in a Pool. By using weights, you can weigh the distribution of traffic. At the same time, the Backup role helps ensure system availability and reliability when the Primary Member fails.

### Attach pool members <a href="#attach-pool-members" id="attach-pool-members"></a>

Use this document as a guide on how to add Members to a Pool on a Load Balancer. Basically, the admin interface supports adding Members to a Pool in two ways:

* **Via Instance** (Members are specific virtual machines or servers)
* **Via IP address** (Members are Public IP addresses or IP addresses belonging to the subnet of the Load Balancer)

**1. Attach/Update Member is available servers**

* Go to Load Balancers​
* In Load Balancers, click to select the Load Balancer that needs to be configured. In the Load Balancer details section, select the Pool tab. In the Pool list section, click to select the Pool that needs to attach/edit Member.
* In the Pool details section on the left, scroll down to Member Information, click the "Edit Pool members / Edit Pool member" button.
* In the "Edit Pool Member" interface window, the "Available instances" section will display a list of available backend servers belonging to the Load Balancer subnet.
* Select an available server from the list.
* Fill in information about Weight, Port, Monitor Port and Backup role parameters.
* Click the "Attach" button to add the backend server as a Pool Member.
* Review the Pool Member list under "Attach server & instances".
* Click the "Save" button to complete editing the Pool Member.

**2. Attach/Update Member is IP address**

In addition to attaching Pool members through backend servers, users can also attach IP addresses as Pool Members, refer to the instructions below to do the attachment.

* Go to Load Balancers;​
* In Load Balancers, click to select the Load Balancer that needs to be configured. In the Load Balancer details section, select the Pool tab. In the Pool list section, click to select the Pool that needs to attach/edit Member.
* In the Pool details section on the left, scroll down to Member Information, click the "Edit Pool members / Edit Pool member" button.
*   In the "Edit Pool Member" interface window, in the "Custom Instances / Custom Instances" section, attach the IP address to the Pool according to the following instructions:

    1/ Enter IP address: IP addresses must be Public IP or belong to Load Balancer subnet

    2/ Click the Add button to add IP addresses to the Custom Instance list

    3/ Select the IP Address to attach from the Custom Instance list

    4/ Fill in information about Weight, Port, Monitor Port and Backup role parameters.

    5/ Press the "Attach" button

    6/ Review the Pool Member list in the "Attached server & instances" section.

    7/ Click the "Save" button to complete editing Pool Member.

***

### Config health check settings <a href="#config-health-check-setting" id="config-health-check-setting"></a>

The Health Check Setting feature is an important factor in ensuring the stability and availability of applications on the Application Load Balancer. When this feature is enabled, the Load Balancer will perform a health check on the backend servers and automatically adjust the traffic flow to ensure that only healthy servers are serving requests from clients. For Application Load Balancer

**How it works**

* The Application Load Balancer will periodically send health check requests to the backend servers, via configured options.
* If the backend server responds with an incorrect status code or content, the Load Balancer considers that server unhealthy and stops sending requests to it.
* Requests from clients will only be forwarded to servers that are considered healthy.
* Common Health Check settings for Application Load Balancer: Health Check TCP and Health Check HTTP

**Benefits of setting up Health check for Load Balancer**

* Increase Availability: Health Check Setting helps improve application availability by removing inactive servers from service.
* Performance Optimization: It helps Load Balancer forward requests to well-performing servers, optimizing system performance.
* Minimize Application Errors: Regular monitoring and health checks help minimize application failures and errors.

**Types of ALB Health check configuration**

* Instructions for configuring Health Check TCP when initializing Pool.
* Instructions for configuring Health Check HTTP when initializing Pool.

**1. Instructions for configuring Health Check TCP when initializing Pool**

In the "Add Pool" interface window, scroll to the "Health Check Settings" section and proceed to set the following information:

1/ Select TCP protocol.

2/ Advanced configuration settings:

* **Healthy Threshold**
  * Explanation: Health Threshold is the number of consecutive health checks that must succeed for a backend server to be considered healthy.
  * For example, if you set the Health Threshold to 3, the backend server must respond successfully to 3 consecutive health checks before it is considered healthy.
* **Unhealthy threshold**
  * Explanation: Unhealthy Threshold is the number of consecutive health checks that must fail before a backend server is marked as unhealthy.
  * For example, if you set Unhealthy Threshold to 2, the backend server will be marked as unhealthy if 2 consecutive health check requests fail.
* **Timeout**
  * Explanation: Timeout is the maximum time a health check request can be sent to the backend server before it is considered a failure. If the server does not respond within this time, the check request will be considered a failure.
  * For example, if you set Timeout to 5 seconds, and the backend server does not respond within 5 seconds, the test request will be marked as failed.
* **Interval**
  * Explanation: Interval is the time interval between health checks sent to the backend server. It determines how often the server health checks.
  * For example, if you set Interval to 30 seconds, the Load Balancer will send a health check request to the backend server every 30 seconds.

**2. Instructions for configuring Health Check HTTP when initializing Pool**

In the "Add Pool" interface window, scroll to the "Health Check Settings" section and proceed to set the following information:

1/ Select HTTP protocol.

2/ Advanced configuration settings:

* **Path / Path**
  * Explanation: Path specifies the specific path URL on the backend server that the Load Balancer will perform health checks on. Through this attribute, you can specify a specific resource on the backend server that you want to check.
  * For example, if you set Path to "/health", the Load Balancer will send health check requests to the URL " [http://backend-server/health](http://backend-server/health) ".
* **HTTP Method / HTTP Method**
  * Explanation: HTTP Method specifies the HTTP method that the Load Balancer uses when sending a health check request to the backend server. This allows you to specify whether the health check should use GET, POST, or PUT.
  * For example, if you set HTTP Method to GET, Load Balancer will send health check request using GET method.
* **Success Code**
  * Explanation: Success Code is the HTTP status code that the backend server must return in response to be considered healthy. If the response from the backend server has a status code that matches the Success Code, then the health check request is considered successful.
  * For example, if you set the Success Code to 200, the backend server must return a 200 OK status code for the health check to be considered successful.
* **Healthy Threshold**
  * Explanation: Health Threshold is the number of consecutive health checks that must succeed for a backend server to be considered healthy.
  * For example, if you set the Health Threshold to 3, the backend server must respond successfully to 3 consecutive health checks before it is considered healthy.
* **Unhealthy threshold**
  * Explanation: Unhealthy Threshold is the number of consecutive health checks that must fail before a backend server is marked as unhealthy.
  * For example, if you set Unhealthy Threshold to 2, the backend server will be marked as unhealthy if 2 consecutive health check requests fail.
* **Timeout**
  * Explanation: Timeout is the maximum time a health check request can be sent to the backend server before it is considered a failure. If the server does not respond within this time, the check request will be considered a failure.
  * For example, if you set Timeout to 5 seconds, and the backend server does not respond within 5 seconds, the test request will be marked as failed.
* **Interval**
  * Explanation: Interval is the time interval between health checks sent to the backend server. It determines how often the server health checks.
  * For example, if you set Interval to 30 seconds, the Load Balancer will send a health check request to the backend server every 30 seconds.
* **Domain Name**
  * Explanation: The domain name is the domain name or IP address that you use to access the backend server when performing a health check.
  * For example, if you set the Domain Name as " [backend-server.example.com](http://backend-server.example.com/) ", the Load Balancer will use this domain name to send health check requests to the backend server.

***

### Enable sticky session <a href="#enable-sticky-session" id="enable-sticky-session"></a>

As we know HTTP is Stateless (the next request does not depend on the previous request result), so to store data between pages, people use sessions. The most common example is the authentication token saved in the session to confirm that the user has logged into the system. The user's authentication information is saved in the session, at this time the Session is stored in a server and is not synchronized between web servers. This is the reason why logged in users are logged out when their request is redirected to a different web server than the server that received their login request.

**To solve the above problem, you can use the following method:**

* Use Cluster for web server applications, with sessions stored in one place accessible to all servers.
* Store session information in a shared database or a file system server on the application server.
* Disadvantage: Building a Cluster system or a Database requires a lot of experience with the system.

That's why vCloudStack provides the **Sticky Session** feature to transfer all user requests in a session to a specific server, simplifying it for users.

**1. Introducing the Enable Sticky Session feature**

**The Enable Sticky Session** feature is an important part of the Load Balancer, allowing you to maintain client sessions persistence on your application. When this feature is enabled, the Load Balancer will ensure that requests from the same client will always be forwarded to the same backend server over a certain period of time. How it **works**

* When a client connects to your application through the Load Balancer, the Load Balancer tracks information to identify that client (usually based on information in cookies or IP address).
* Subsequent requests from the same client will be forwarded to the same backend server within a predefined interval.
* This helps ensure that client state and information are maintained consistently throughout the session.

**Benefits of Enabling Sticky Session**

* **Enhanced Customer Experience** : Sticky Session improves end-user experience by maintaining persistent session state, preventing data loss or re-logins.
* **Status Request Application Support** : Status request applications or online shopping carts benefit from this feature.

**2. Instructions to enable/disable Sticky Session feature**

* Go to Load Balancer.​
* At Load Balancer, click to select the Load Balancer to configure.
* In the Load Balancer details section, select the Pool tab.
* In the Pool list, hover over the Pool you want to edit and click the Edit icon.
* A pop-up window allows editing of the Pool.
* In the Pool information section, find the check box Enable sticky session/Enable sticky session, check/uncheck to enable/disable the Sticky Session feature.
* Click the "Save" button at the bottom right corner of the editing window to complete the editing.

***

### Enable TLS encryption <a href="#enable-tls-encryption" id="enable-tls-encryption"></a>

**The Enable TLS Encryption** feature is an important element of network security, allowing you to protect data transmitted from the Load Balancer to the backend server. When this feature is enabled, the transmitted data will be encrypted and protected during the entire transfer. **How it works**

* When a client connects to the Load Balancer and requests to access your website or application, the data transmitted between the client and the Load Balancer is encrypted using a secure protocol, TLS (Transport Layer Security), before it is forwarded to the backend server.
* The backend server also needs to support TLS to be able to decrypt data sent from the Load Balancer.
* This process ensures that the transmitted data cannot be intercepted or understood in case it is intercepted en route.

**Benefits of enabling TLS Encryption**

* **High Security** : TLS Encryption ensures a high level of security for your data, helping to prevent man-in-the-middle attacks and data theft.
* **Secure Integration** : It allows you to provide a secure experience to your customers by protecting their personal and account information as data is transmitted to the Load Balancer.
* **Reliability** : TLS Encryption provides reliability in data transmission over the network, helping to ensure that data is not lost or modified during transmission from the Load Balancer to the backend server.
* **Enable Self-signed Certificate** : TLS Encryption supports both HTTP and HTTPS. For HTTPS, when enabled, the Load Balancer will not verify the correctness of the SSL/TLS Certificate. This allows you to use self-signed certificates on member servers.

**Instructions for enabling TLS Encryption**

* Go to Load Balancer.​
* On the Load Balancer homepage, click on the Load Balancer that needs to be configured.
* In the Load Balancer details section, select the Pool tab.
* In the Pool list, hover over the Pool you want to edit and click the Edit icon.
* A pop-up window allows editing of the Pool.
* In the Pool information section, find the Enable TLS Encryption check box, check/uncheck to enable/disable TLS encryption feature.
* Click the "Save" button at the bottom right corner of the editing window to complete the editing.

***

### Pool's algorithm <a href="#pools-algorithm" id="pools-algorithm"></a>

Load balancing or "Load Balancing" is one of the main features of VNG CLOUD's Load Balancer (vLB) service. It is the process of receiving customer requests at the Listener and distributing them to a number of Members (servers) according to established algorithms. Thanks to this feature, the user's service is increased in processing capacity by creating multiple or a cluster of servers behind the LB. The Load Balancing algorithm will determine which Member (server) is selected when balancing the load. VNG CLOUD's Load Balancer provides three types of Load Balancing algorithms as follows:

* **Round Robin**
* **Least Connection**
* **Source IP**

**1. Round Robin**

Round Robin is an algorithm that selects Members (servers) in order. Accordingly, the Load Balancer will start from Member (server) number 1 in its list corresponding to the first request. Then, it will move down the list in order and start again at the top when it reaches the last Member (server).

**2. Least Connection**

Requests will be routed to the server with the least active connections in the system at the moment. This algorithm is considered a dynamic algorithm, because it has to count the number of active connections of the server. **How it works** For example: We have 5 clients sending connections to 2 servers, then when there is a request from the 6th client, how will the request be coordinated?

* Case 1: If no client disconnects, client 6 will be sent to Server 2 because the connection ratio between the two Servers is 3:2. See the illustration below.
* Case 2: If client 1 & 3 disconnect before client 6 sends the request, then when sending the request, client 6 will be sent to Server 1 because the connection ratio between the two Servers is 1:2. See the illustration below

**3. Source IP**

This algorithm combines the source and destination IP addresses of the client and server to create a unique hash key. This key is used to assign the client to a specific server, and it can be regenerated if the session times out or disconnects for some reason. The client's request is then routed to the same server it used before. This is a method to ensure that the user connects to the same server. For example, to retain items in a shopping cart between sessions.
