# Load Balancing Algorithms

Load balancing or "Load balancing" is one of the main features of the Load Balancer (LB) service of VNG CLOUD. It is the process of taking client requests at Listener and distributing them to some Member (server) according to established algorithms. Thanks to this feature, the user's service is increased in processing capacity by creating many or a cluster of servers behind the LB.

The Load Balancing algorithm determines which Member (server) is selected for load balancing. Load Balancer of VNG CLOUD provides three types of Load Balancing algorithms and advanced Weight features capable of handling according to the configuration of each Member (server)  with many different purposes for users:

**1. Round Robin**

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59802720/image2020-5-24_22-18-14.png?version=1&#x26;modificationDate=1685081357000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Round Robin is an algorithm for selecting members (servers) in sequence. Accordingly, the Load Balancer will start from Member (server) number 1 in its list corresponding to the first request. It will then move down the list in order and start again at the top when it reaches the last Member (server).

**2. Least Connection**

Requests will be redirected to the server with the fewest active connections in the system at the moment. This algorithm is considered a dynamic algorithm, because it has to count the number of active connections of the server.

For example:

We have 6 client requests to the LB that are load balancing for the 2 servers below.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802720/image2020-5-24_22-19-20.png?version=1&#x26;modificationDate=1685081357000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Step 1: All 6 clients send requests and divide equally between 2 servers.

Step 2: Assuming client 1 and 3 disconnect before client 6 sends the request, then client 6's request will be forwarded to server 1.

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59802720/image2020-5-24_22-25-23.png?version=1&#x26;modificationDate=1685081357000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


**3. Source IP**

This algorithm combines the source and destination IP addresses of the client and server to generate a unique hash key. This key is used to assign the client to a specific server, and it can be regenerated if the session is timeout or disconnected for some reason. The client's request is then still routed to the same server it used before. This is a method to ensure that users will connect to the same server. For example, to retain cart items between sessions.

**Tính năng Weight**

Weight or "Weight" is capable of handling according to the configuration of each target Member (server). Each server is evaluated with an integer (weight value – default value is 1). A server with twice the capacity of another server will be numbered twice as large and receive twice as many requests from the Load Balancer. This feature will often combine with the above algorithms to create many uses for Customers.

For example: Server 1 has 5 times the processing capacity of Server 2. We will type "Weight = 5" for server 1 and "Weight = 1" for server 2.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802720/image2020-5-24_22-34-57.png?version=1&#x26;modificationDate=1685081357000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
