# Config health check setting (NLB)

Health checks are a vital feature of Network Load Balancers (NLBs). They ensure the availability and performance of servers or targets within the target group. Health checks allow the NLB to automatically detect which servers or services are operational and remove any unavailable ones from the Load Balancer.

#### How Health Checks Work

* **Periodic Checks:** The NLB performs periodic health checks on the servers or targets in the pool. These checks can be pings, HTTP GET requests, or other custom checks.
* **Identifying Unavailability:** If a server or target doesn't respond to the health check or returns an error, the NLB considers it unavailable.
* **Removal of Unavailable Servers/Targets:** Once an unavailable server or target is identified, the NLB stops directing traffic to it for a period. This prevents traffic from being sent to non-functioning servers, ensuring service availability.

#### Benefits of Configuring Health Checks for Load Balancers

* **Increased Availability:** Health checks help ensure that only available servers or services receive traffic, increasing service availability and preventing traffic from reaching non-functioning servers.
* **Optimized Performance:** The NLB can automatically adjust load balancing by removing unhealthy servers, optimizing system performance and preventing server overload.
* **Automated Management:** Health checks automate the management of server or service availability, reducing the need for manual intervention.
* **Security:** The NLB can remove unhealthy servers to ensure that traffic is not sent to insecure or compromised servers.

#### Types of NLB Health Check Configurations

* **TCP Health Check: Configuration guide for TCP/Proxy protocol pools.**
* **HTTP/HTTPS Health Check: Configuration guide for TCP/Proxy protocol pools.**
* **PING-UDP Health Check: Configuration guide for UDP protocol pools.**

## 1. Configuring TCP Health Checks for TCP/Proxy Protocol Pools

In the "Add Pool" interface window, go to the "Health Check Settings" section and configure the following:

1. **Select Protocol:** Choose "TCP."
2. **Advanced Configuration:**
   * **Healthy Threshold:**
     * **Explanation:** The number of consecutive successful health checks required for a backend server to be considered healthy.
     * **Example:** If you set the Healthy Threshold to 3, the backend server must respond successfully to 3 consecutive health checks before being considered healthy.
   * **Unhealthy Threshold:**
     * **Explanation:** The number of consecutive failed health checks before a backend server is marked as unhealthy.
     * **Example:** If you set the Unhealthy Threshold to 2, the backend server will be marked as unhealthy if there are 2 consecutive failed health check requests.
   * **Timeout:**
     * **Explanation:** The maximum time allowed for a health check request sent to the backend server before it is considered a failure. If the server does not respond within this time, the health check request is considered failed.
     * **Example:** If you set the Timeout to 5 seconds, and the backend server does not respond within 5 seconds, the health check request will be marked as failed.
   * **Interval:**
     * **Explanation:** The time interval between health checks sent to the backend server. It determines how often the server's health is checked.
     * **Example:** If you set the Interval to 30 seconds, the Load Balancer will send a health check request to the backend server every 30 seconds.

## 2. Configuring HTTP/HTTPS Health Checks for TCP/Proxy Protocol Pools

In the "Add Pool" interface window, go to the "Health Check Settings" section and configure the following:

1. **Select Protocol:** Choose "HTTP" or "HTTPS."
2. **Advanced Configuration:**
   * **Path:**
     * **Explanation:** Specifies the specific URL path on the backend server that the Load Balancer will use for health checks. This allows you to designate a particular resource on the backend server that you want to check.
     * **Example:** If you set the Path to "/health," the Load Balancer will send health check requests to the URL "http://backend-server/health" or "https://backend-server/health" depending on the chosen protocol.
   * **HTTP Method:**
     * **Explanation:** Defines the HTTP method that the Load Balancer uses when sending health check requests to the backend server. This allows you to specify whether the health check should use GET, POST, or PUT.
     * **Example:** If you set the HTTP Method to GET, the Load Balancer will send health check requests using the GET method.
   * **Success Codes:**
     * **Explanation:** The HTTP status code(s) that the backend server must return in its response to be considered healthy. If the response from the backend server has a status code that matches the Success Codes, the health check request is considered successful.
     * **Example:** If you set the Success Codes to 200, the backend server must return a 200 OK status code for the health check to be considered successful.
   * **Healthy Threshold, Unhealthy Threshold, Timeout, and Interval:** These settings have the same explanations and examples as in the TCP Health Check configuration.
   * **Domain Name:**
     * **Explanation:** The domain name or IP address that you use to access the backend server when performing health checks.
     * **Example:** If you set the Domain Name to "backend-server.example.com," the Load Balancer will use this domain name to send health check requests to the backend server.

## 3. Configuring PING-UDP Health Checks for UDP Protocol Pools

In the "Add Pool" interface window, go to the "Health Check Settings" section and configure the following:

* **Select Protocol:** Choose "PING-UDP."
* **Advanced Configuration:**
  * **Healthy Threshold, Unhealthy Threshold, Timeout, and Interval:** These settings have the same explanations and examples as in the TCP Health Check configuration.
