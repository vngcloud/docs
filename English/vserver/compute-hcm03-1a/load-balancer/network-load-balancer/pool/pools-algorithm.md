# Pool's algorithm

Load balancing is one of the key features of VNG Cloud's Load Balancer (vLB) service. It is the process of receiving client requests at the listener and distributing them across multiple members (servers) according to established algorithms. This feature allows you to increase the processing capacity of your services by creating multiple or a cluster of servers behind the Load Balancer.

The load balancing algorithm determines which member (server) is chosen for each incoming request. VNG Cloud's Load Balancer offers three types of load balancing algorithms:

1.  **Round Robin**

    Round Robin is a simple algorithm that selects members (servers) in a sequential order. The Load Balancer starts with the first member in its list for the first request, then moves down the list in order, starting again at the top when it reaches the last member. ![](<../../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)
2.  **Least Connections**

    Requests are directed to the server with the fewest active connections at the current time. This algorithm is considered dynamic, as it constantly tracks the number of active connections on each server.

    **How it Works (Example):**

    Imagine you have 5 clients connected to 2 servers. When a 6th client sends a request:

    * **Scenario 1: No Disconnections:** If no clients have disconnected, client 6 will be sent to Server 2 because the connection ratio between the two servers is 3:2. ![](<../../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)
    * **Scenario 2: Disconnections:** If clients 1 and 3 disconnect before client 6 sends a request, client 6 will be sent to Server 1 because the connection ratio is now 1:2. ![](<../../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)
3.  **Source IP**

    This algorithm combines the source and destination IP addresses of the client and server to create a unique hash key. This key is used to assign the client to a specific server, and it can be recreated if the session times out or is disconnected for any reason. This ensures that the client's requests are consistently directed to the same server, which is useful for maintaining things like shopping cart items across sessions.

<figure><img src="../../../../../.gitbook/assets/image (227).png" alt=""><figcaption></figcaption></figure>
