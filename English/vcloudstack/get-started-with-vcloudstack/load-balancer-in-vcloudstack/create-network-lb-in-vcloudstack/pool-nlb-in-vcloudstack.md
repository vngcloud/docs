# Pool (NLB) in vCloudStack

Pool is an important component in the Load Balancing system, responsible for distributing traffic to backend servers to improve service performance, availability and reliability.

The main goal of a Pool is Load Balancing. The Pool ensures that traffic is distributed evenly and efficiently to the backend servers. This prevents any server from being overloaded while others are idle.

The pool consists of backend servers, called "Pool Members." Pool Members serve requests and responses to users or devices through the Load Balancer.

***

### How to add new Pool <a href="#add-and-updateapool-nlb-1.cachthemmoipool" id="add-and-updateapool-nlb-1.cachthemmoipool"></a>

* Go to the Load Balancers home page.
* At Load Balancers, click to select the Load Balancer that needs to add a new Pool.
* In the Load Balancer details section, select the Pool tab.
* Click the "Add new Pool" button, an interface window appears allowing you to configure Pool information.
* In the new window, configure information such as:
  * Pool Name: Note that the Pool name cannot be changed after initialization.
  * Protocol: TCP / Proxy / UDP
  * [Select load balancing algorithm: See also Pool's algorithm (NLB)](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/pool/pools-algorithm) load balancing algorithms
  * Health Check Settings: Refer to the Health Check NLB settings guide at [Config health check setting (NLB)](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/pool/config-health-check-setting)
  * [Add Pool Member: Refer to Attach Pool Member (NLB)](https://docs.vngcloud.vn/pages/viewpage.action?pageId=64553815) guide
* Click the "Add" button at the bottom right corner of the new add window to complete adding the Pool.

***

### How to update Pool information <a href="#add-and-updateapool-nlb-2.cachcapnhatthongtinpool" id="add-and-updateapool-nlb-2.cachcapnhatthongtinpool"></a>

* Go to Load Balancers.
* At Load Balancer, click to select the Load Balancer to configure.
* In the Load Balancer details section, select the Pool tab.
* In the Pool list, hover over the Pool you want to edit and click the Edit icon.
* A pop-up window allows editing of the Pool, the information is allowed to be updated
  * Load Balancing Algorithm
  * Advanced health check configuration
* Click the "Save" button at the bottom right corner of the editing window to complete the Pool update.

***

### Pool Member (NLB) <a href="#pool-member-nlb" id="pool-member-nlb"></a>

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

***

### Configure health check (NLB) <a href="#cau-hinh-health-check-nlb" id="cau-hinh-health-check-nlb"></a>

Health Check is an important feature of Network Load Balancer (NLB) used to ensure the availability and performance of servers or objects in the cluster. Health Check allows NLB to automatically detect which servers or services are up and down along with automatically removing unavailable servers or services from the Load Balancer.

**How it works**

* Periodic health checks: NLB will perform periodic health checks on the hosts or objects in the pool. These checks can be Ping, HTTP GET requests, or other custom checks.
* Identify server/object unavailable: If a server or object does not respond to a health check or returns an error, NLB considers the server or object as unavailable.
* Eliminate Unavailable Servers/Instances: Once a server or object is determined to be unavailable, NLB stops redirecting traffic to that server for a period of time. This prevents traffic from being sent to the inactive server, ensuring service availability.

**Benefits of setting up Health check for Load Balancer**

* Increased Availability: Health Check helps ensure that only available servers or services receive traffic. This increases service availability and prevents inactive servers from receiving traffic.
* Optimize performance: NLB can automatically adjust load balancing by eliminating inactive servers. This helps optimize system performance and prevent server overload.
* Automated Management: Health Check helps automatically manage the availability of servers or services, minimizing manual intervention.
* Security: NLB can eliminate inactive servers to ensure that traffic is not sent to insecure or inactive servers.

**Types of NLB Health check configuration**

* Instructions for configuring Health Check TCP when initializing TCP/Proxy protocol pool.
* Instructions for configuring Health Check HTTP/HTTPS when initializing TCP/Proxy protocol Pool.
* Instructions for configuring Health Check PING-UDP when initializing UDP protocol Pool.

**1. Instructions for configuring Health Check TCP when initializing TCP/Proxy protocol pool**

In the "Add Pool" interface window, scroll to the "Health Check Settings" section and proceed to set the following information:

**1/ Select TCP protocol.**

**2/ Advanced configuration settings:**

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

**2. Instructions for configuring Health Check HTTP/HTTPS when initializing TCP/Proxy protocol pool**

In the "Add Pool" interface window, scroll to the "Health Check Settings" section and proceed to set the following information:

**1/ Select HTTP protocol.**

**2/ Advanced configuration settings:**

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

**3. Instructions for configuring Health Check PING-UDP when initializing UDP protocol Pool**

In the "Add Pool" interface window, scroll to the "Health Check Settings" section and proceed to set the following information:

**1/ Select HTTP protocol.**

**2/ Advanced configuration settings:**

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

***

### Pool's algorithm (NLB) <a href="#pools-algorithm-nlb" id="pools-algorithm-nlb"></a>

Load balancing or "Load Balancing" is one of the main features of VNG CLOUD's Load Balancer (vLB) service. It is the process of receiving customer requests at the Listener and distributing them to a number of Members (servers) according to established algorithms. Thanks to this feature, the user's service is increased in processing capacity by creating multiple or a cluster of servers behind the LB. The Load Balancing algorithm will determine which Member (server) is selected when balancing the load. VNG CLOUD's Load Balancer provides three types of Load Balancing algorithms as follows:

* **Round Robin**
* **Least Connection**
* **Source IP**

**1. Round Robin**

Round Robin is an algorithm that selects Members (servers) in order. Accordingly, the Load Balancer will start from Member (server) number 1 in its list corresponding to the first request. Then, it will move down the list in order and start again at the top when it reaches the last Member (server).

**2. Least Connection**

Requests will be routed to the server with the least active connections in the system at the moment. This algorithm is considered a dynamic algorithm, because it has to count the number of active connections of the server. **How it works** For example: We have 5 clients sending connections to 2 servers, then when there is a request from the 6th client, how will the request be coordinated?

* Case 1: If no client disconnects, client 6 will be sent to Server 2 because the connection ratio between the two Servers is 3:2. See the illustration below.
* Case 2: If client 1 & 3 disconnect before client 6 sends a request, then when sending a request, client 6 will be sent to Server 1 because the connection ratio between the two Servers is 1:2. See the illustration below.

**3. Source IP**

This algorithm combines the source and destination IP addresses of the client and server to create a unique hash key. This key is used to assign the client to a specific server, and it can be regenerated if the session times out or disconnects for some reason. The client's request is then routed to the same server it used before. This is a method to ensure that the user connects to the same server. For example, to retain items in a shopping cart between sessions.
