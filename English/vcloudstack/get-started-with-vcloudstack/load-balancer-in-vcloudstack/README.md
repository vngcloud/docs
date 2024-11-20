# Load Balancer in vCloudStack

To distribute network traffic to multiple VM servers, as well as ensure efficient resource utilization and increase application availability. vCloudStack provides Load Balancer service by distributing traffic based on defined rules and algorithms, Load Balancer improves performance and is a reliable tool for user applications, preventing any single member server from becoming overloaded.

The model for Load Balancer to work in vCloudStack includes the following components:

* **Layer :** Supports 2 main types, including:
  * _Application Load Balancer:_ Application layer Load Balancer routes traffic based on HTTP/HTTPS requests, allowing for analysis of application-level data such as HTTP Headers and Cookies. Ideal for web applications with complex routing requirements or content-based routing needs.
  * _Network Load Balancer:_ A transport-layer Load Balancer that uses TCP and UDP to distribute traffic among multiple servers based on IP address and port number, ideal for applications that require high reliability and availability.
* **Scheme** : only apply scheme is Internal:
  * _Internal:_ Internal Load Balancer routes traffic from the client's internal network to server clusters, helping to distribute requests efficiently within the internal network.
* **Load Balancer:** Supports the deployment of 2 Load Balancer models including Application LB and Network LB, each Load Balancer includes main components such as:
  * **Listener:** A listener is a component that monitors and listens for incoming connection requests. It is responsible for receiving traffic on a specific port and protocol, and then forwarding or routing that traffic to valid hosts based on defined rules and configuration.
    * **Policy** : For Application Load Balancer, Policy acts as a set of rules/conditions to distribute requests to backend servers
  * **Pool** : A pool represents a group of servers and handles incoming traffic. The pool is responsible for load balancing requests across its members, ensuring efficient distribution and utilization of resources.
    * **Pool Member:** A Pool Memeber acts as a member server in the Pool.
    * **Health Check:** Health Check setting is a set of rules, through which the Load Balancer monitors the health of its Pools and Pool Members.
