# Config health check setting

The Health Check Setting feature is crucial for ensuring the stability and availability of your applications on the Application Load Balancer. When enabled, the Load Balancer periodically checks the health of backend servers and automatically adjusts traffic flow to ensure that only healthy servers receive requests from clients.

#### How it Works

1. **Health Check Requests:** The Application Load Balancer periodically sends health check requests to backend servers based on your configured options.
2. **Health Status Evaluation:** If a backend server responds with an incorrect status code or content, the Load Balancer considers it unhealthy and stops sending requests to it.
3. **Traffic Routing:** Client requests are only forwarded to servers deemed healthy.

#### Common Health Check Settings for Application Load Balancers

* **TCP Health Check**
* **HTTP Health Check**

#### Benefits of Configuring Health Checks

* **Increased Availability:** Health checks improve application availability by removing unhealthy servers from service.
* **Optimized Performance:** They help the Load Balancer forward requests to healthy servers, optimizing system performance.
* **Reduced Application Errors:** Continuous monitoring and health checks help minimize application issues and errors.

#### Configuring Health Checks for ALBs

* **Instructions for Configuring TCP Health Checks when Creating a Pool**
* **Instructions for Configuring HTTP Health Checks when Creating a Pool**

## Configuring TCP Health Checks when Creating a Pool

In the "Add Pool" window, scroll down to the "Health Check Settings" section and configure the following:

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

## Configuring HTTP Health Checks when Creating a Pool

In the "Add Pool" window, scroll down to the "Health Check Settings" section and configure the following:

1. **Select Protocol:** Choose "HTTP."
2. **Advanced Configuration:**
   * **Path:**
     * **Explanation:** Specifies the specific URL path on the backend server that the Load Balancer will use for health checks. This allows you to designate a particular resource on the backend server that you want to check.
     * **Example:** If you set the Path to "/health," the Load Balancer will send health check requests to the URL "http://backend-server/health."
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
