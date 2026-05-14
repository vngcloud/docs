# Config timeout

The timeout configuration feature in Load Balancers allows you to specify the maximum duration a connection or request can exist before being closed. This is important for managing resources and ensuring consistent system performance.

#### How Timeouts Work

1. **Timer Starts:** When a connection or request is sent to the Load Balancer, a timer begins to track the allowed duration for that connection.
2. **Timeout Threshold:** If the connection is not completed or the request is not responded to within this timeframe, it is closed.
3. **Resource Management:** Configuring timeouts helps prevent connections or requests from hanging and consuming resources unnecessarily.

#### Why Configure Timeouts?

* **Resource Management:** Timeouts help manage system resources efficiently by ensuring that unnecessary connections or requests do not consume resources.
* **Performance Assurance:** This helps ensure that the Load Balancer operates efficiently and does not get stuck on unresponsive connections or requests.

#### Timeout Configuration Instructions

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer you want to configure.
3. **Go to the Listener Tab:** In the Load Balancer details page, select the "Listener" tab.
4. **Edit Listener:** Click the "Edit" icon next to the listener you want to configure timeouts for.
5. **Advanced Configuration:** In the pop-up window, scroll down to the "Advanced Configuration" section.
6. **Idle Timeout Settings:** Configure the timeout values based on the following attributes:
   * **Client Timeout:**
     * **Explanation:** The maximum time the Load Balancer allows a client to maintain a connection without making any requests. If there is no activity from the client within this period, the connection is closed.
     * **Benefit:** This frees up resources on both the backend server and the Load Balancer, ensuring that unnecessary connections do not consume resources.
   * **Member Timeout:**
     * **Explanation:** The maximum time the Load Balancer allows a member server in the backend server pool to maintain an open connection without receiving data from it. If the member server does not send data within this period, the connection is closed.
     * **Benefit:** This ensures that member servers do not waste resources by maintaining idle connections.
   * **Connection Timeout:**
     * **Explanation:** The maximum time the Load Balancer allows a network connection between itself and a backend server to exist before being closed. This time starts when the connection is established. If there is no activity on the connection (including data transfer) within this period, the connection is closed.
     * **Benefit:** This ensures that unnecessary connections are closed, freeing up resources and ensuring stable network performance.
7. **Save Changes:** Click "Save" in the bottom right corner of the window to finalize your updates.
