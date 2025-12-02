# Listener

Listeners are a crucial component in directing traffic to backend servers within a Load Balancer. They allow you to configure how the Load Balancer listens for and routes traffic to specific applications or services running on those backend servers.

## How Listeners Work

1. **Listening for Traffic:** A listener continuously monitors incoming traffic to the Load Balancer from users or devices.
2. **Routing Based on Configuration:** The listener directs traffic to the appropriate backend servers based on its configuration settings.
3. **Identifying Traffic:** Listeners typically use information such as the port number and protocol (e.g., HTTP, HTTPS, TCP) to determine how to route traffic.

## Key Features of Listeners

* **Add HTTP Listener:** Create a listener to handle incoming HTTP traffic on port 80 (or a custom port).
* **Add HTTPS Listener:** Create a listener to handle secure HTTPS traffic on port 443 (or a custom port). This requires an SSL/TLS certificate for encryption.
* **Update & Delete a Listener:** Modify existing listener settings or remove listeners that are no longer needed.
* **Listener Policies:** Define rules and conditions that determine how traffic is routed to different target groups based on specific criteria (e.g., URL paths, headers, or query strings).
* **Client Certificate Authentication:** Configure the listener to require client-side SSL/TLS certificates for authentication, adding an extra layer of security.
* **IP Whitelisting:** Restrict access to the Load Balancer by specifying a list of allowed IP addresses or CIDR blocks.
* **Timeout Configuration:** Set timeouts for idle connections and request processing to prevent resource exhaustion and improve the responsiveness of your applications.

## Example: HTTPS Listener Configuration

Let's say you want to create an HTTPS listener for a web application running on your backend servers. Here's a simplified configuration:

* **Protocol:** HTTPS
* **Port:** 443
* **Default Action:** Forward to Target Group (your group of backend web servers)
* **SSL Certificate:** Select the appropriate SSL/TLS certificate from your VNG Cloud account.

With this configuration, the listener will listen for HTTPS traffic on port 443, decrypt the traffic using the provided SSL certificate, and then forward the decrypted traffic to the healthy backend servers in your target group.

<br>

<br>
