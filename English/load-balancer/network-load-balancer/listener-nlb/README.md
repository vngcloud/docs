# Listener (NLB)

Listeners are a crucial component in directing traffic to backend servers within a Network Load Balancer. They allow you to configure how the Load Balancer listens for and routes traffic to specific applications or services running on those backend servers.

#### How Listeners Work

1. **Listening for Traffic:** A listener continuously monitors incoming traffic to the Load Balancer from users or devices.
2. **Routing Based on Configuration:** The listener directs traffic to the appropriate backend servers based on its configuration settings.
3. **Identifying Traffic:** Listeners typically use information such as the port number and protocol (e.g., TCP, UDP) to determine how to route traffic.

#### Key Features of Listeners

* **Add TCP Listener:** Create a listener to handle incoming TCP traffic on a specified port (e.g., port 80 for HTTP or a custom port).
* **Add UDP Listener:** Create a listener to handle incoming UDP traffic on a specified port (e.g., port 53 for DNS or a custom port).
* **Update & Delete a Listener (NLB):** Modify existing listener settings or remove listeners that are no longer needed.
* **IP Whitelisting (NLB):** Restrict access to the Load Balancer by specifying a list of allowed IP addresses or CIDR blocks.
* **Timeout Configuration (NLB):** Set timeouts for idle connections and request processing to prevent resource exhaustion and improve the responsiveness of your applications.

#### Example: TCP Listener Configuration

Let's say you want to create a TCP listener for an application running on your backend servers using port 8080. Here's a simplified configuration:

* **Protocol:** TCP
* **Port:** 8080
* **Default Action:** Forward to Target Group (your group of backend servers)

With this configuration, the listener will listen for TCP traffic on port 8080 and forward it to the healthy backend servers in your target group.
